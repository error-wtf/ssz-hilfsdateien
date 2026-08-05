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
