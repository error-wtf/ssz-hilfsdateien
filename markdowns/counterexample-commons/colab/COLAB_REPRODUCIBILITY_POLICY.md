# Colab Reproducibility Policy

## Principles

1. **Exact baselines are always reproducible** — they use SymPy rational arithmetic
2. **AI experiments are inherently non-deterministic** — models may produce different outputs
3. **All experiment artifacts must be saved** — including failed runs
4. **Pre-registration happens before generation** — never retroactively

## What Colab Can Reproduce

- Line configuration edge counts (exact)
- Grid configuration edge counts (exact)
- Custom finite configuration validation (exact)
- The validation step of any AI experiment (exact)

## What Colab Cannot Reproduce

- The exact same model output from a previous run
- Results from a disconnected session (unless exported)
- Ollama Local experiments (localhost = Colab VM)
