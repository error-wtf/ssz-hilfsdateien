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
