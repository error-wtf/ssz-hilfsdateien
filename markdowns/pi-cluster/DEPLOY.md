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
