# Deployment Options Comparison

| Option | Persistence | Providers | Cost Risk | Security |
|--------|-------------|-----------|-----------|----------|
| **Localhost** | Permanent | All configured | User-controlled | Best (local only) |
| **Colab share** | Temporary | None (demo) or secrets (private) | Low (demo) / user (private) | Public link |
| **HF Spaces** | Permanent | None (public demo) | None | Public, no secrets |
| **Auth server** | Permanent | All | Controlled | Authenticated |

## Recommended defaults

- **Development:** localhost `--mode local-private`
- **Public demo:** Hugging Face Spaces or Colab public-demo
- **Private cloud research:** Colab private (temporary) or authenticated server (future)
