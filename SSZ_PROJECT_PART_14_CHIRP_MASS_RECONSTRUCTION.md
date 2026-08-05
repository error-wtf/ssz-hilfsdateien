# ChatGPT Project SSZ Compilation — Part 14 / 17
## Category: CHIRP MASS RECONSTRUCTION

This is compiled ChatGPT Project file 14 of 17. It contains verbatim transcripts of all unique markdown documents related to this specific physical or experimental domain, sorted alphabetically by repository and path. Old historical duplicate folders have been actively deduplicated.

- **Total Files Compiled (Deduplicated):** 6
- **Total Verbatim Lines:** 661



# =========================================================================
# FILE: pi-cluster/AGENTS.md
# =========================================================================

# AGENTS.md — pi-cluster

## Project Identity
- **Name:** pi-cluster
- **Purpose:** HPC Pi computation suite + cluster benchmark/diagnostic tool
- **Target:** PHYSnet Cluster, Universität Hamburg (12,812 cores, 45.5 TB RAM, 539 nodes, 42 GPGPUs)
- **Origin:** Rewrite of error-wtf/CALCULATION_OF_NUMBER_PI
- **License:** Anti-Capitalist Software License v1.4

## Architecture
- CPU-first, MPI-capable, CUDA optional
- Chudnovsky algorithm (Binary Splitting path planned)
- Modular: core / cpu / cuda / mpi / storage / detect / bench / progress
- Three execution modes: local-validate, physnet-single-node, physnet-cluster

## Key Rules
- PHYSnet compatibility has priority over GPU maximization
- CUDA is optional — never a hard dependency
- No fake performance claims
- No invented PHYSnet internals — autodetect or mark as TODO
- CPU-only path must always work
- Checkpointing mandatory for long runs
- All benchmarks must produce machine-readable output

## Build
```bash
mkdir build && cd build
cmake .. -DBUILD_CUDA=OFF -DBUILD_MPI=OFF  # minimal local build
cmake .. -DBUILD_MPI=ON                      # PHYSnet CPU+MPI
cmake .. -DBUILD_CUDA=ON -DBUILD_MPI=ON      # full hybrid
make -j$(nproc)
```

## CLI
```
pi-cluster detect          # hardware probe
pi-cluster bench           # microbenchmarks
pi-cluster doctor          # system readiness check
pi-cluster estimate -d 1e9 # resource estimation
pi-cluster run -d 1000000  # compute pi
pi-cluster resume -c path  # resume from checkpoint
```


# =========================================================================
# FILE: pi-cluster/BUILD.md
# =========================================================================

# Build Guide

## Prerequisites

| Dependency | Required | Purpose |
|-----------|----------|---------|
| CMake ≥ 3.18 | Yes | Build system |
| C++17 compiler (GCC ≥ 9, Clang ≥ 10) | Yes | Core compilation |
| GMP + GMPXX | Yes (for production) | Arbitrary precision arithmetic |
| Boost.Multiprecision | Optional | Fallback if GMP unavailable |
| MPI (OpenMPI / MPICH) | Optional | Multi-node computation |
| CUDA Toolkit ≥ 11.0 | Optional | GPU acceleration |

### Installing dependencies

**Ubuntu/Debian:**
```bash
sudo apt install cmake g++ libgmp-dev libboost-dev
# For MPI:
sudo apt install libopenmpi-dev openmpi-bin
# For CUDA: install from NVIDIA (https://developer.nvidia.com/cuda-downloads)
```

**PHYSnet (via modules):**
```bash
module avail              # see what's available
module load gcc           # or gcc/11, gcc/12
module load gmp           # if available as module
module load openmpi       # or mpich
# module load cuda        # if GPU partition
```

**macOS (Homebrew):**
```bash
brew install cmake gmp boost open-mpi
```

---

## Build Configurations

### 1. Minimal local build (CPU only, no MPI, no CUDA)

```bash
mkdir build && cd build
cmake .. -DBUILD_CUDA=OFF -DBUILD_MPI=OFF
make -j$(nproc)
```

This is the simplest build. Requires only GMP + C++17 compiler.
Produces: `pi-cluster` binary with detect, bench, doctor, estimate, run commands.

### 2. PHYSnet production build (CPU + MPI)

```bash
module load gcc gmp openmpi    # adjust to available modules
mkdir build && cd build
cmake .. -DBUILD_MPI=ON -DBUILD_CUDA=OFF
make -j$(nproc)
```

Enables multi-node computation via MPI. Single-node runs still work.

### 3. Full hybrid build (CPU + MPI + CUDA)

```bash
module load gcc gmp openmpi cuda
mkdir build && cd build
cmake .. -DBUILD_MPI=ON -DBUILD_CUDA=ON
make -j$(nproc)
```

Enables GPU benchmarks and experimental CUDA hybrid path.
**If CUDA is not found, the build succeeds with GPU features disabled.**

### 4. Debug build

```bash
cmake .. -DCMAKE_BUILD_TYPE=Debug -DBUILD_TESTS=ON
make -j$(nproc)
ctest --output-on-failure
```

---

## Build Options Reference

| Option | Default | Description |
|--------|---------|-------------|
| `BUILD_CUDA` | OFF | Enable CUDA/GPU support |
| `BUILD_MPI` | OFF | Enable MPI multi-node support |
| `BUILD_TESTS` | ON | Build unit and smoke tests |
| `CMAKE_BUILD_TYPE` | Release | Release / Debug / RelWithDebInfo |

---

## Verifying the build

```bash
# Check binary runs
./pi-cluster --help

# Hardware detection
./pi-cluster detect

# System readiness
./pi-cluster doctor

# Quick smoke test (100 digits)
./pi-cluster run -d 100 -b cpu -v

# Run unit tests
ctest --output-on-failure
```

---

## Troubleshooting

**GMP not found:**
```
CMake Warning: GMP not found. Install libgmp-dev.
```
→ Install `libgmp-dev` (Ubuntu) or `gmp` (Homebrew) or load the GMP module on PHYSnet.

**MPI not found:**
```
CMake Error: MPI not found
```
→ Install `libopenmpi-dev` or load `openmpi`/`mpich` module.

**CUDA not found (non-fatal):**
```
CMake Warning: CUDA requested but no compiler found. Disabling GPU support.
```
→ This is fine. GPU features are disabled, everything else works.

**Linker errors with GMP:**
```
undefined reference to `__gmpf_init`
```
→ Make sure `-lgmp -lgmpxx` are linked. Check that `GMP_LIB` is found by CMake.

**C++17 filesystem errors:**
```
error: 'filesystem' is not a member of 'std'
```
→ Use GCC ≥ 9 or add `-lstdc++fs` on older compilers.


# =========================================================================
# FILE: pi-cluster/DEPLOY.md
# =========================================================================

# Deployment Guide — PHYSnet

## Quick Start on PHYSnet

```bash
# 1. Login
ssh login1.physnet.uni-hamburg.de

# 2. Clone
git clone https://github.com/error-wtf/pi-cluster.git
cd pi-cluster

# 3. Build
module load gcc gmp openmpi   # adjust to available modules
mkdir build && cd build
cmake .. -DBUILD_MPI=ON
make -j$(nproc)

# 4. Test locally on login node (small run)
./pi-cluster doctor
./pi-cluster detect
./pi-cluster run -d 1000 -b cpu -v

# 5. Submit to Slurm
cd ..
sbatch scripts/slurm/pi-single-node.sbatch
```

## Slurm Workflow

### Step 1: Dry-run to check resources
```bash
./build/pi-cluster run -d 1000000000 -b mpi --dry-run
```
This shows RAM/scratch/chunk plan without executing.

### Step 2: Single-node test
```bash
sbatch scripts/slurm/pi-single-node.sbatch
```
Edit the script to adjust digits, partition, time limit.

### Step 3: Multi-node run
```bash
sbatch scripts/slurm/pi-8nodes.sbatch
```

### Step 4: Monitor
```bash
squeue -u $USER              # job status
sacct -j <JOBID> --format=JobID,Elapsed,MaxRSS,State
tail -f pi-single_<JOBID>.out  # live output
```

## Slurm Script Customization

Edit `scripts/slurm/pi-single-node.sbatch`:
```bash
#SBATCH --partition=batch     # change to your partition
#SBATCH --time=24:00:00       # adjust wall time
#SBATCH --mem=64G             # adjust per-node RAM

# Adjust digits:
./build/pi-cluster run --digits 100000000 --backend cpu --confirm --verbose
```

## Scratch Strategy

pi-cluster automatically uses `$SLURM_TMPDIR` for temporary chunk data.
- Chunk partial results → node-local scratch (fast SSD)
- Final output → `$SLURM_SUBMIT_DIR/output/`
- Checkpoints → `$SLURM_TMPDIR/checkpoints/` (auto-saved on signal)

**Copy important results before job ends** — node-local scratch is deleted after job completion:
```bash
# In your sbatch script, after pi-cluster run:
cp -r $SLURM_TMPDIR/checkpoints/ $SLURM_SUBMIT_DIR/checkpoints_$SLURM_JOB_ID/
```

## Container Deployment (Alternative)

If modules are problematic, use Apptainer/Singularity:
```bash
# Build container on your machine
# Dockerfile → .sif conversion
apptainer build pi-cluster.sif docker://ubuntu:22.04
# Then on PHYSnet:
module load apptainer
apptainer exec pi-cluster.sif ./pi-cluster run -d 1000000 -b cpu
```

## Environment Variables

pi-cluster reads these automatically:
| Variable | Purpose |
|----------|---------|
| `SLURM_JOB_ID` | Job identification |
| `SLURM_NNODES` | Node count |
| `SLURM_TMPDIR` | Node-local scratch path |
| `SLURM_CPUS_PER_TASK` | Available CPU cores |
| `TMPDIR` | Fallback scratch path |

## Safety Notes

- pi-cluster **never** writes large temp data to AFS/home by default
- `--dry-run` always available to preview before committing resources
- Runs >10M digits require `--confirm` flag
- SIGTERM/SIGUSR1 from Slurm triggers graceful checkpoint save
- Disk watermark monitoring aborts safely if scratch fills up


# =========================================================================
# FILE: pi-cluster/docs/architecture.md
# =========================================================================

# pi-cluster Architecture

## Module Overview

```
pi-cluster/
├── core/       Chudnovsky algorithm (GMP arbitrary precision)
├── cpu/        CPU-specific paths (planned: NTT/Binary Splitting)
├── cuda/       Optional CUDA hybrid (≤700 digits, experimental)
├── mpi/        MPI multi-node: rank discovery, work partition, merge
├── detect/     Hardware detection: CPU, RAM, NUMA, GPU, Scratch, Slurm
├── bench/      Microbenchmarks: CPU throughput, memory BW, disk IO
├── progress/   Phase-based progress: ETA, throughput, chunk status
├── storage/    Chunk manager, scratch manager, checkpoint/resume
├── cli/        Main CLI with subcommands
└── util/       Guardrails (safe paths, resource limits, signal handling)
```

## Execution Flow

```
pi-cluster run -d 1000000 -b cpu -v

1. detect system (CPU, RAM, scratch, Slurm, GPU)
2. guardrails: feasibility check (RAM, scratch, disk)
3. build run plan (dry-run preview if --dry-run)
4. chunk planning (adaptive size based on RAM/scratch/ranks)
5. install signal handlers (SIGINT/SIGTERM graceful shutdown)
6. for each chunk assigned to this rank:
   a. set chunk status → COMPUTING
   b. compute partial result
   c. disk watermark check
   d. set chunk status → COMPUTED
7. MPI merge (if multi-node)
8. save checkpoint (chunk plan + metadata)
9. write output
10. report stats
```

## Chunk Architecture

Chunks are the fundamental unit of work:
- Each chunk covers a range of Chudnovsky terms
- Chunks are assigned round-robin to MPI ranks
- Chunk size is adaptive based on free RAM and scratch
- Each chunk has: id, range, owner_rank, status, checksum, timing
- Checkpoint saves chunk plan as JSON → resume recomputes only incomplete chunks

## Backend Selection

| Backend | Description | MPI | GPU |
|---------|-------------|-----|-----|
| auto | Conservative auto-detect | if available | only if ≤700 digits |
| cpu | GMP Chudnovsky, single process | no | no |
| hybrid | GPU for terms + GMP accumulation | no | yes |
| mpi | Distributed CPU across ranks | yes | no |
| mpi-hybrid | Distributed with GPU per node | yes | yes |

## Safety Model

- Safe path policy: only writes to project/scratch/output dirs
- Resource guardrails: max RAM fraction, scratch reserve, disk watermark
- Signal handling: graceful shutdown with last checkpoint on SIGTERM
- No destructive defaults: cleanup only in own directories
- Dry-run mode: preview full plan before execution


# =========================================================================
# FILE: pi-cluster/docs/physnet.md
# =========================================================================

# PHYSnet Integration Guide

## Cluster Overview

PHYSnet is the central HPC cluster of the Physics Department at Universität Hamburg:

- **12,812 CPU cores** across 539 nodes
- **45.5 TB RAM** total
- **42 NVIDIA GPGPUs** (~407,296 CUDA cores)
- **Ubuntu 22.04** with Slurm v23.02.5
- **Environment Modules** for software management
- **InfiniBand** interconnect (high bandwidth, low latency)
- **AFS** home directories + parallel filesystem (Lustre/GPFS)
- **Node-local scratch** (SSD/NVMe, job-specific via `$TMPDIR`)

## Login

```bash
ssh login1.physnet.uni-hamburg.de
```

## Building pi-cluster on PHYSnet

```bash
# Load required modules (adjust names to what's available)
module avail           # check available modules
module load gcc gmp    # compiler + arbitrary precision
module load mpi        # MPI (if multi-node needed)
# module load cuda     # only if GPU partition

# Build
mkdir build && cd build
cmake .. -DBUILD_MPI=ON -DBUILD_CUDA=OFF
make -j$(nproc)
```

## Running

### Quick smoke test (interactive)
```bash
./pi-cluster doctor
./pi-cluster detect
./pi-cluster bench
./pi-cluster run -d 10000 -b cpu -v
```

### Single-node Slurm job
```bash
sbatch scripts/slurm/pi-single-node.sbatch
```

### Multi-node MPI job
```bash
sbatch scripts/slurm/pi-8nodes.sbatch
```

### Dry-run before large computation
```bash
./pi-cluster run -d 1000000000 -b mpi --dry-run
```

## Scratch Usage

pi-cluster automatically detects `$SLURM_TMPDIR` or `$TMPDIR` for node-local scratch.
All temporary chunk data goes there — never directly to AFS/shared filesystem.

After job completion, node-local scratch is automatically cleaned by Slurm.

## Resource Guardrails

pi-cluster enforces conservative defaults:
- Max 70% of free RAM used
- 15% scratch reserve maintained
- Disk watermark monitoring during computation
- Graceful shutdown on SIGTERM/SIGUSR1 (Slurm preemption)
- No writes outside project/scratch/output directories

## GPU Policy

CUDA is **optional**. PHYSnet has 42 GPUs but they may not be available for every job.
pi-cluster detects GPU availability at runtime and falls back to CPU automatically.

Request GPUs via Slurm: `--gres=gpu:1`

## Support

PHYSnet support: support@physnet.uni-hamburg.de


# =========================================================================
# FILE: pi-cluster/README.md
# =========================================================================

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
