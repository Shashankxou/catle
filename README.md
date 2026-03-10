# catle

## Capstone Project Import

The `capstone-project/` folder contains the imported code from
[Ayisha114/Capstone-project](https://github.com/Ayisha114/Capstone-project) —
a **Flask-based cattle disease detection** web application powered by a
Vision Transformer (ViT) ML model.

---

### Where the code lives

```
capstone-project/
├── app.py                 # Flask application entry-point
├── requirements.txt       # Python dependencies
├── Dockerfile             # Docker image definition
├── docker-compose.yml     # Local Docker Compose setup
├── render.yaml            # One-click Render.com deployment config
├── Procfile               # Heroku/Render process declaration
├── models/                # ML model files (*.pth excluded from git — see below)
├── static/                # CSS, JS, uploaded images
└── templates/             # Jinja2 HTML templates
```

> **Note on model weights:** The trained model file (`models/cattle_disease_vit_model.pth`)
> is excluded from Git because it exceeds GitHub's 100 MB file limit.
> Download it separately and place it at `capstone-project/models/cattle_disease_vit_model.pth`
> before running the app (see the source repo's `models/README.md`).

---

### How to build / run locally

#### Option A — Python virtualenv

```bash
cd capstone-project

# Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate

# Install dependencies (CPU-only torch recommended for dev)
pip install -r requirements.txt

# Start the development server
python app.py
# → open http://localhost:5000
```

#### Option B — Docker Compose

```bash
cd capstone-project
docker compose up --build
# → open http://localhost:5000
```

#### Option C — Docker

```bash
cd capstone-project
docker build -t capstone-project .
docker run -p 5000:5000 \
  -e PORT=5000 \
  -e SECRET_KEY=change-me \
  capstone-project
```

---

### Deployment

#### Automated CI (GitHub Actions)

The workflow at `.github/workflows/deploy-capstone.yml` runs on every push to
`main` that touches `capstone-project/**` and on manual `workflow_dispatch`.

It:
1. Installs Python deps and validates `app.py` syntax + imports.
2. Builds the Docker image to confirm it compiles correctly.
3. Prints step-by-step deployment instructions in the workflow log.

#### Render.com (recommended, free tier available)

1. Go to <https://render.com> and sign in.
2. Click **New +** → **Web Service**.
3. Connect this GitHub repository.
4. Set **Root Directory** to `capstone-project`.
5. Render auto-detects `render.yaml` and configures the service.
6. Add the `SECRET_KEY` environment variable in the Render dashboard.

#### Configuring a different deploy target

Edit `.github/workflows/deploy-capstone.yml` and add a step after the
`docker-build` job that pushes the built image to your registry
(GHCR, Docker Hub, ECR, etc.) and triggers a redeploy.
Required GitHub Actions secrets to add in **Settings → Secrets**:

| Secret name | Purpose |
|---|---|
| `REGISTRY_USERNAME` | Container-registry login |
| `REGISTRY_PASSWORD` | Container-registry password / token |
| `SECRET_KEY` | Flask `SECRET_KEY` for production |
