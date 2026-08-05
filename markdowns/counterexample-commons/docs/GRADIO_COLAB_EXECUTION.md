# Gradio Colab Execution

## Public Demo (Default)

```python
from app.main import build_app
from app.config import AppMode
demo = build_app(mode=AppMode.COLAB_PUBLIC_DEMO)
demo.queue().launch(share=True, debug=False)
```

No API spending. No secrets. Safe validation only.

## Private Research (Manual)

Requires Colab Secrets for API keys. Separate cell, not default.

## Limitations

- Colab VMs are temporary — save outputs before shutdown
- `localhost` = Colab VM, not your PC — use Ollama Cloud instead
- Share links are public — not enterprise security
- For persistent deployment use Hugging Face Spaces or local app
