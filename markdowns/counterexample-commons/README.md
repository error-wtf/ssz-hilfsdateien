# Counterexample Commons

## An Anti-Capitalist AI-Assisted Mathematics Research Lab

[![License: ACSL v1.4](https://img.shields.io/badge/License-ACSL%20v1.4-red.svg)](LICENSE)
[![Python 3.11+](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://python.org)
[![Research Status](https://img.shields.io/badge/Status-Experimental-orange.svg)]()

**Counterexample Commons** is a source-available research laboratory for exact
mathematical validation and controlled AI-assisted exploration.

Its first case study examines the 2026 AI-generated counterexample to Paul
Erdős' planar unit-distance conjecture: a result showing that, for infinitely
many values of n, there exist planar point configurations with at least
n^{1+δ} unit-distance pairs for some fixed δ>0. Will Sawin obtains the
explicit exponent n^{1.014}.

This repository does not treat AI output as proof. It separates
source-documented results from locally reproduced exact calculations,
exploratory model-generated candidates and rejected or failed experiments.

Released under the **Anti-Capitalist Software License (v 1.4)**.
Copyright © 2026 Lino Casu.

---

## 1. Political and Scientific Mission

Mathematics should not become privately enclosed research infrastructure for
corporate extraction or military power. This project supports a
commons-oriented, anti-capitalist approach to technical knowledge.

## 2. First Case Study: Erdős' Unit-Distance Problem

Let u(n) = max unit-distance pairs among n planar points.

- **Line:** n−1 edges. **Grid k×k:** 2k(k−1) edges.
- **Historical:** n^{1+C/log log n} constructions.
- **2026:** AI construction achieves n^{1+δ} (fixed δ>0); Sawin: n^{1.014}.
- **Open:** exact u(n) between n^{1.014} and O(n^{4/3}).

### Visuals

![Line](docs/images/line.png)
<br>*Line: 5 points → 4 unit edges*

![Grid](docs/images/grid.png)
<br>*Grid: 3×3 → 12 unit edges*

![Custom](docs/images/custom.png)
<br>*Unit Square: 4 points → 4 unit edges*

![Rational mesh baseline](docs/images/rational_mesh_baseline.png)
<br>*Finite rational mesh baseline (not Sawin's construction)*

## 3. What This Repository Reproduces

| Component | Status |
|-----------|--------|
| Line edge count | LOCALLY_REPRODUCED_EXACT |
| Grid edge count | LOCALLY_REPRODUCED_EXACT |
| Custom finite validation | LOCALLY_REPRODUCED_EXACT |
| OpenAI fixed-δ theorem | SOURCE_DOCUMENTED |
| Finite rational mesh baseline | LOCALLY_REPRODUCED_EXACT |
| Sawin n^{1.014} | SOURCE_DOCUMENTED — not yet locally reproduced |
| AI-generated candidates | AI_GENERATED_HYPOTHESIS |

## 4. What This Repository Does NOT Claim

- Does not reproduce OpenAI's internal model execution
- A finite configuration does not prove an asymptotic theorem
- Sawin's explicit exponent n^{1.014} is source-documented only; not yet locally reproduced
- The rational-mesh code is an exact finite baseline, not Sawin's algebraic-number-theoretic construction
- Does not provide free API-funded research to public visitors

## 5. Claim Status System

[Full definitions](references/CLAIM_TO_SOURCE_MATRIX.md)

`SOURCE_DOCUMENTED` · `LOCALLY_REPRODUCED_EXACT` · `LOCALLY_REPRODUCED_NUMERICAL`
`AI_GENERATED_HYPOTHESIS` · `FORMALLY_VERIFIED` · `REJECTED_OR_FAILED` · `INCONCLUSIVE`

## 6. Main User Interface (Gradio)

Overview · Exact Baselines · Configuration Explorer · Visualisierung ·
AI Candidate Lab · Provider Comparison · Claim Registry · Reports & Export ·
Settings

![AI Pipeline](docs/images/ai_pipeline.png)
<br>*AI Experiment Pipeline: From pre-registration to sanitized export*

## 7. Quick Start: Localhost

```bash
pip install -r requirements.txt
python scripts/run_gradio_local.py --mode local-private
```

Without `.env`, the app runs as a complete safe no-key finite-validation lab:
Exact Baselines, Explorer, Visualisierung, read-only claims and finite exports
remain available; AI/provider actions report `NOT_CONFIGURED` and make no live
request.

The primary live AI path is **Ollama Local**. It does not need an API key; it
only needs an Ollama server reachable from the runtime:

```bash
ollama serve
ollama pull llama3.1:8b
export OLLAMA_MODEL=llama3.1:8b
python scripts/run_gradio_local.py --mode local-private --no-browser --port 7861
```

On PowerShell, use `$env:OLLAMA_MODEL="llama3.1:8b"` instead of `export`.
If Ollama is running, the AI Candidate Lab defaults to `ollama_local`.

To switch to a different local Ollama endpoint, set `OLLAMA_BASE_URL` before
launch, for example `http://localhost:11434` or another trusted private host.
To switch to a cloud provider, copy `.env.example` to `.env`, fill only the
provider you want, restart the app and select that provider in the UI.

For private cloud-provider testing:

```bash
cp .env.example .env
python scripts/run_gradio_local.py --mode local-private --no-browser --port 7861
```

Provider keys are never displayed or exported. A shared live-AI session requires
an explicit warning flag:

```bash
python scripts/run_gradio_local.py --mode local-private --confirm-live-ai-share --port 7861
```

## 7a. Six Execution Modes

| Mode | Key | AI Labs | Share |
|------|-----|:---:|:---:|
| `local-private` | env file | yes | no |
| `local-share` | none | no | yes |
| `public-demo` | none | no | no |
| `colab-private` | Colab Secrets | yes | no |
| `colab-public-demo` | none | no | yes |
| `hosted-public-demo` | none | no | no |

## 7b. AI Experiment Pipeline

1. **Pre-register** claim and falsifier before generation
2. **Generate** from any provider (manual trigger only)
3. **Extract** candidate coordinates from raw output
4. **Validate** with exact SymPy rational arithmetic
5. **Record** all artifacts (including failed runs)
6. **Export** sanitized reports

Current AI Lab scope: finite rational point candidates only. It does not
attempt the algebraic-number-theoretic construction used in the OpenAI proof,
does not reproduce Sawin's `n^{1.014}` result, and does not establish
asymptotic bounds.

### Grid Scaling Analysis

![Grid Scaling](docs/images/grid_scaling.png)
<br>*Grid k×k scaling: Points vs edges → ratio approaches 2*

## 7c. Google Colab Research Lab — Complete Lab

The previously published multi-notebook Colab layer has been **withdrawn** as a
validated public workflow.

Local execution inside an existing repository checkout was incorrectly treated
as evidence of fresh Google Colab functionality. It is not.

The public `main` branch now contains **one complete, end-to-end research lab
notebook**. It launches the same Gradio app and, by default, starts keyless
Ollama Local inside the Colab VM:

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/error-wtf/counterexample-commons/blob/main/notebooks/Counterexample_Commons_Complete_Lab_Colab.ipynb?cacheBust=ollama-archive-installer-v2)

Current status:

- Previous ten-notebook Colab layer: **deprecated / not validated**
- Single complete Colab lab: integrated as the public notebook entry point
- Default Colab AI path: keyless Ollama Local inside the Colab VM
- Finite-only fallback: set `ENABLE_COLAB_OLLAMA = False` in the notebook
- Live API-key provider workflow: not part of the public Colab notebook
- Sawin n^{1.014}: SOURCE\_DOCUMENTED only, not locally reproduced

The deprecated prototype notebooks remain in the repository under
`notebooks/` for reference but are not advertised as public workflows.

The complete notebook clones `main` and starts the same local-first Gradio lab.
It must not be read as evidence that the asymptotic OpenAI/Sawin theorem has
been locally reproduced.

Colab cannot see an Ollama server running on your desktop `localhost`.
By default the notebook installs/starts Ollama inside the Colab VM, pulls
`OLLAMA_MODEL` and launches the app in `colab-private` mode. This uses Colab
runtime compute, not an API key. The notebook uses Ollama's official Linux
archives directly instead of relying on the service install script, because
fresh Colab runtimes do not behave like normal systemd Linux hosts. Set
`ENABLE_COLAB_OLLAMA = False` for a finite-only `colab-public-demo` run.

## 8. Supported AI Providers (7)

| Provider | Env Var | Local Private | Colab Private | Public Demo |
|----------|---------|:---:|:---:|:---:|
| OpenAI | `OPENAI_API_KEY` | yes | yes | no |
| OpenRouter | `OPENROUTER_API_KEY` | yes | yes | no |
| Ollama Cloud | `OLLAMA_API_KEY` | yes | yes | no |
| Ollama Local | *(none)* | yes | yes, Colab VM only | no |
| Mistral | `MISTRAL_API_KEY` | yes | yes | no |
| Google Gemini | `GEMINI_API_KEY` | yes | yes | no |
| Anthropic Claude | `ANTHROPIC_API_KEY` | yes | yes | no |

## 9. Sources

| Source | Role |
|--------|------|
| [OpenAI announcement (2026-05-20)](https://openai.com/index/model-disproves-discrete-geometry-conjecture/) | Claim framing |
| [Alon et al., arXiv:2605.20695](https://arxiv.org/abs/2605.20695) | Companion analysis |
| [Sawin, arXiv:2605.20579](https://arxiv.org/abs/2605.20579) | Explicit n^{1.014} |

## 10. License

All original material: **Anti-Capitalist Software License (v 1.4)**.
Copyright © 2026 Lino Casu.

This is source-available anti-capitalist research software, not OSI-defined
open-source software. See [LICENSE](LICENSE), [LICENSE_POLICY.md](LICENSE_POLICY.md),
[THIRD_PARTY_SOURCES_AND_LICENSES.md](THIRD_PARTY_SOURCES_AND_LICENSES.md).

## 11. Contributions

Welcome from individuals, educational contexts, non-profits and cooperatives
consistent with ACSL v1.4. No military, policing, surveillance or exploitative
commercial application work.

## 12. Author

**Lino Casu** — independent anti-capitalist mathematical research.
