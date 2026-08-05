# Gradio Local Execution

## Installation

```bash
git clone https://github.com/OWNER/counterexample-commons.git
cd counterexample-commons
pip install -r requirements.txt
```

## Launch (localhost only)

```bash
python scripts/run_gradio_local.py --mode local-private
```

Default: `http://127.0.0.1:7860` — no share link, no external access.

## Optional flags

| Flag | Default | Description |
|------|---------|-------------|
| `--port` | 7860 | Custom port |
| `--no-browser` | False | Don't auto-open browser |
| `--mode` | `local-private` | Execution mode |
| `--confirm-public-share` | — | Required to enable share link |

## Local Ollama

In `local-private` mode:

- Ollama Local is supported when running on `http://localhost:11434`
- Availability is checked only when the user requests it
- Custom model names are allowed
- No automatic model download is triggered

## Environment Variables for Providers

```bash
OPENAI_API_KEY=sk-...
OPENROUTER_API_KEY=sk-or-...
MISTRAL_API_KEY=...
GOOGLE_GEMINI_API_KEY=...
ANTHROPIC_API_KEY=...
OLLAMA_CLOUD_URL=...
OLLAMA_CLOUD_API_KEY=...
```

Store in `.env` (gitignored) or set in shell. Never commit secrets.

## Private Local Workflow

1. Configure providers via environment variables
2. Launch with `--mode local-private`
3. Use AI Candidate Lab to generate candidates
4. Validate candidates with exact arithmetic
5. Export sanitized reports
