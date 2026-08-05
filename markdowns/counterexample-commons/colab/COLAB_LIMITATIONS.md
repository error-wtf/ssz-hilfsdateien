# Colab Limitations

## Runtime

- Sessions disconnect after inactivity (~30–90 min)
- GPU/TPU availability is not guaranteed on free tier
- All files are deleted when the runtime disconnects

## Networking

- `localhost` refers to the Colab VM, not your local machine
- Ollama Local cannot be used from Colab (no local GPU access)
- Gradio share links are temporary and expire with the session

## Security

- Do not hardcode API keys in notebook cells
- Use `google.colab.userdata` for secret storage
- Public demo mode disables all paid API calls by default
- Anyone with your Gradio share link can interact with the UI

## Storage

- Google Drive is not mounted by default
- Export validated results before session ends
- Run directories are ephemeral
