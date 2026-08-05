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
