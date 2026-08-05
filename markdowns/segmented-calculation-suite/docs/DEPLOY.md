# SSZ Calculation Suite - Deployment Guide

## Quick Start

### Local Development
```bash
pip install -r requirements.txt
python app_v3.py
```
App runs at `http://localhost:7860`

---

## Docker Deployment

### Build & Run Locally
```bash
docker build -t ssz-suite .
docker run -p 7860:7860 ssz-suite
```

### Environment Variables
| Variable | Default | Description |
|----------|---------|-------------|
| `HOST` | `0.0.0.0` | Bind address |
| `PORT` | `7860` | Port number |

---

## Cloud Platforms

### Hugging Face Spaces
1. Create new Space (Gradio SDK)
2. Upload all files or connect GitHub repo
3. App auto-deploys

### Render
1. Create new Web Service
2. Connect GitHub repo
3. Build Command: `pip install -r requirements.txt`
4. Start Command: `python app_v3.py`
5. Set PORT environment variable if needed

### Fly.io
```bash
fly launch
fly deploy
```

### Railway
1. Connect GitHub repo
2. Auto-detects Dockerfile
3. Deploy

---

## Health Check

The app exposes a health endpoint via Gradio's built-in mechanisms.
Docker HEALTHCHECK is configured to verify the app is responding.

---

## Requirements

- Python 3.10+
- See `requirements.txt` for dependencies

---

## Files Structure

```
ssz-suite/
├── app_v3.py           # Main application
├── Dockerfile          # Container definition
├── requirements.txt    # Python dependencies
├── segcalc/           # Core calculation modules
│   ├── config/        # Constants, settings
│   ├── core/          # Data models, run bundles
│   ├── methods/       # SSZ calculations
│   ├── datasets/      # Schema validation
│   └── plotting/      # Visualization
└── docs/              # Documentation
```

---

## Troubleshooting

### Port Already in Use
Set a different port via environment:
```bash
PORT=8080 python app_v3.py
```

### Memory Issues
For large datasets, increase container memory limits.

### Plots Not Rendering
Ensure `matplotlib` and `plotly` are installed.
For Plotly image export, install `kaleido`:
```bash
pip install kaleido
```
