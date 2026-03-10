# Catle

Cattle Disease Classification using Vision Transformer (ViT) — a Flask web application that lets users upload cattle images for AI-powered disease detection.

## Project Structure

| Path | Description |
|------|-------------|
| `index.html` | Static landing page (deployed to GitHub Pages) |
| `capstone-project/` | Flask application (cattle disease classifier) |
| `.github/workflows/deploy.yml` | GitHub Pages deployment workflow |
| `.github/workflows/deploy-capstone.yml` | Capstone project CI & deployment guide |

## Quick Start

### Option 1 — Docker Compose (recommended)

```bash
cd capstone-project
docker compose up --build
# Open http://localhost:5000
```

### Option 2 — Local virtual environment

```bash
cd capstone-project
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python app.py
# Open http://localhost:5000
```

### Option 3 — Deploy to Render.com

The repo includes a `capstone-project/render.yaml`. Connect this repository on [Render](https://dashboard.render.com) and it will auto-detect the configuration.

## Model Weights

The trained model file (`cattle_disease_vit_model.pth`, ~328 MB) exceeds GitHub's file-size limit and is **not** stored in this repository. Download it separately and place it at:

```
capstone-project/models/cattle_disease_vit_model.pth
```

## GitHub Pages

The static landing page is deployed automatically on push to `main` at:

`https://shashankxou.github.io/catle/`

## License

See `capstone-project/LICENSE` for license details.
