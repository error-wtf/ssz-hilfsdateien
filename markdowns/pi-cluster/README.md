# pi-cluster

**HPC Pi Computation Suite + Cluster Benchmark Tool**

*Target: PHYSnet Cluster, Universität Hamburg*

[![License: Anti-Capitalist](https://img.shields.io/badge/License-Anti--Capitalist%20v1.4-blue.svg)](LICENSE)

---

## What is pi-cluster?

**pi-cluster** is a high-performance computing tool that does two things:

1. **Computes π** using the Chudnovsky algorithm with arbitrary precision (GMP), optional CUDA GPU acceleration, and MPI multi-node distribution
2. **Benchmarks and diagnoses HPC clusters** — hardware detection, memory/disk/CPU benchmarks, Slurm awareness, and system validation

It is designed specifically for the **PHYSnet cluster** at Universität Hamburg (12,812 cores, 45.5 TB RAM, 539 nodes, 42 GPGPUs) but works on any Linux system.

### Why?

- **For researchers:** Compute π to arbitrary precision on a single node or across the cluster
- **For admins:** Validate cluster health, benchmark nodes, test scratch I/O
- **For teaching:** Demonstrate HPC concepts (MPI, CUDA, Slurm, checkpointing) with a real computation
- **For records:** Architecture designed to scale toward trillion-digit computations

---

## Quick Start

### Local build (no MPI, no CUDA)

```bash
git clone https://github.com/error-wtf/pi-cluster.git
cd pi-cluster
mkdir build && cd build
cmake .. -DBUILD_CUDA=OFF -DBUILD_MPI=OFF
make -j$(nproc)

# Detect your hardware
./pi-cluster detect

# Run benchmarks
./pi-cluster bench

# Check system readiness
./pi-cluster doctor

# Compute 10,000 digits of pi
./pi-cluster run -d 10000 -b cpu -v
```

### PHYSnet build (with MPI)

```bash
module load gcc gmp    # adjust to PHYSnet modules
mkdir build && cd build
cmake .. -DBUILD_MPI=ON -DBUILD_CUDA=OFF
make -j$(nproc)

# Submit single-node job
sbatch scripts/slurm/pi-single-node.sbatch

# Submit 8-node MPI job
sbatch scripts/slurm/pi-8nodes.sbatch
```

### Full hybrid build (MPI + CUDA)

```bash
module load gcc gmp cuda mpi
mkdir build && cd build
cmake .. -DBUILD_MPI=ON -DBUILD_CUDA=ON
make -j$(nproc)
```

---

## CLI Commands

| Command | Description |
|---------|-------------|
| `pi-cluster detect` | Probe hardware: CPU, RAM, NUMA, GPU, scratch, Slurm |
| `pi-cluster bench` | Run microbenchmarks: CPU throughput, memory BW, disk I/O |
| `pi-cluster doctor` | Check system readiness (OK / WARN / FAIL) |
| `pi-cluster estimate -d N` | Estimate resources needed for N digits |
| `pi-cluster run -d N` | Compute π with N decimal digits |
| `pi-cluster resume -c path` | Resume from checkpoint |

### Run options

```
-d, --digits <N>      Number of decimal digits
-b, --backend <B>     Backend: auto, cpu, hybrid, mpi, mpi-hybrid
-o, --output <file>   Output file (default: pi.txt)
--chunk <N>           Checkpoint interval (default: 1000 terms)
--scratch <path>      Override scratch directory
--dry-run             Show execution plan without running
--confirm             Required for runs >10M digits
--max-ram <F>         Max RAM fraction (default: 0.70)
--json                Machine-readable JSON output
-v, --verbose         Show progress bar and detailed output
```

---

## Architecture

```
pi-cluster/
├── src/
│   ├── core/          # Chudnovsky + Binary Splitting (GMP, MPI-distributed)
│   ├── cpu/           │   ├── cuda/          # CUDA hybrid: Tier 1 GPU double, Tier 2 gpu_multiply_mpz in BS merge
│   ├── mpi/           # MPI: rank discovery, hierarchical tree-reduce, BSNode merge
│   ├── detect/        # Hardware detection: CPU, RAM, NUMA, GPU, Scratch, Slurm
│   ├── bench/         # Benchmarks: CPU, memory, seq+random disk, GPU, MPI + calibration
│   ├── progress/      # Progress: ETA, throughput, chunk/merge stats, JSON telemetry
│   ├── storage/       # Chunk persistence (atomic+checksum), checkpoint/resume, scratch
│   ├── cli/           # Main CLI with subcommands
│   └── util/          # Guardrails (safe paths, resource limits, signals), formatting
├── include/picluster/ # Public headers
├── tests/             # Unit, integration, smoke tests
├── scripts/slurm/     # Slurm job templates (1, 8, 64 nodes)
├── configs/           # YAML configs for local and PHYSnet
└── docs/              # Architecture, PHYSnet guide, benchmarking
```

### Execution Modes

| Mode | Nodes | Backend | Use case |
|------|-------|---------|----------|
| **local-validate** | 1 (laptop) | cpu | Quick test, demo, teaching |
| **physnet-single** | 1 (cluster) | cpu or hybrid | Moderate computation, benchmarking |
| **physnet-cluster** | 8–64+ | mpi or mpi-hybrid | Large-scale computation |

### Backend Selection

| Backend | Description |
|---------|-------------|
| `auto` | Conservative auto-detect: prefers CPU/MPI, uses binary splitting >50K digits, GPU only if detected and small |
| `cpu` | GMP arbitrary precision, single-node |
| `hybrid` | GPU Chudnovsky (≤700 digits) + CPU for higher precision |
| `mpi` | Multi-node CPU via MPI |
| `mpi-hybrid` | Multi-node with optional GPU per node |

**GPU/CUDA policy:** CUDA is **optional**. The CPU path is always the primary production path. GPU acceleration is available for benchmarking and moderate-precision runs. The build never fails if CUDA is absent.

---

## Origin

This project is a complete rewrite of [CALCULATION_OF_NUMBER_PI](https://github.com/error-wtf/CALCULATION_OF_NUMBER_PI), restructured for HPC cluster deployment.

### What was kept from the original:
- Chudnovsky algorithm (CPU + GMP)
- CUDA hybrid approach (GPU kernel for term computation)
- Resource detection heuristics (RAM, disk, VRAM)
- BBP validation method

### What is new:
- Modular C++ architecture with clean separation of concerns
- CMake build system with optional CUDA/MPI
- Full hardware detection (CPU, NUMA, GPU, Scratch, Slurm)
- Microbenchmark suite
- Phase-based progress tracking with ETA and JSON telemetry
- Checkpoint/resume support
- MPI multi-node with hierarchical tree-reduce merge (GMP serialize/deserialize)
- Slurm job templates for PHYSnet
- Doctor/estimate commands for pre-flight checks

---

## Implementation Status

| Component | Status | What's real | What's not yet |
|-----------|--------|-------------|----------------|
| Hardware detection | ✅ Production | CPU, RAM, NUMA, GPU, Scratch, Slurm | — |
| Chudnovsky CPU (GMP) | ✅ Production | Arbitrary precision, `compute_partial_sum()` per chunk range | — |
| Binary splitting | ✅ Production | Real GMP product tree P/Q/T, auto-selected >50K digits, MPI-distributed tree-reduce across ranks | — |
| Chunk computation | ✅ Production | Real partial sums per chunk, persisted to scratch with atomic writes + checksums + metadata | — |
| MPI merge | ✅ Production | Hierarchical tree-reduce: O(log N) pairwise steps with GMP serialize/deserialize | — |
| Guardrails | ✅ Production | Feasibility check, `--dry-run`, `--confirm` gate, disk watermark → `exit(2)` with checkpoint | — |
| Signal handling | ✅ Production | SIGINT/SIGTERM → real `chunks.json` checkpoint save | — |
| Checkpoint/Resume | ✅ Production | Chunk plan saved as JSON; `resume` parses status, auto-recomputes only incomplete chunks | — |
| CLI | ✅ Production | detect, bench, doctor, estimate, run, resume | — |
| Progress tracker | ✅ Production | Phase-based, ETA, throughput, chunk stats (C:done/total R:restored F:failed), merge level, JSON export | — |
| Benchmarks (CPU/Mem/IO) | ✅ Production | CPU throughput, memory bandwidth, sequential disk I/O, 4K random read IOPS | — |
| GPU benchmarks | ✅ Implemented | H2D bandwidth (64 MB), FMA kernel (1M threads) | Requires `BUILD_CUDA=ON` |
| MPI benchmarks | ✅ Implemented | Ping-pong latency (10K iters), Allreduce bandwidth (8 MB) | Requires `BUILD_MPI=ON` |
| CUDA hybrid | ✅ Implemented | Tier 1: GPU double ≤700 digits. Tier 2: binary splitting + gpu_multiply_mpz (GMP limb ↔ GPU NTT end-to-end) | — |
| BBP validation | ✅ Production | Double-precision cross-check | — |

---

## PHYSnet Notes

- **Scheduler:** Slurm
- **Modules:** Use `module avail` to find available compilers/libraries
- **Scratch:** Use `$SLURM_TMPDIR` for node-local temporary storage
- **GPU:** 42 GPGPUs available; request via `--gres=gpu:N`

See [docs/physnet.md](docs/physnet.md) for detailed PHYSnet integration guide.

---

## License

[Anti-Capitalist Software License v1.4](LICENSE)

© 2024–2026 Lino Casu
