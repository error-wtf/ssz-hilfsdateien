# Colab Usage Guide

## Default Mode: `colab-public-demo`

When you open any notebook in Google Colab, it runs in **public demo mode** by default:

- No API keys loaded
- No paid provider calls
- No Google Drive mounted
- Exact baselines and finite explorer enabled
- Gradio share link allowed only through manual launch cell

## Private Research Mode: `colab-private`

To enable AI provider experiments:

1. Set `COUNTEREXAMPLE_MODE=colab-private` in a notebook cell
2. Store API keys in Colab Secrets (`google.colab.userdata`)
3. Manually enable provider cells
4. Be aware: shared authenticated UI links may trigger configured actions

## Important Limitations

- Colab sessions are **temporary** — all data is lost on disconnect
- `localhost` in Colab is the VM, not your home computer
- Ollama Local is **not available** from hosted Colab
- Save important results before the session ends
