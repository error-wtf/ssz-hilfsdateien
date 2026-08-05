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
