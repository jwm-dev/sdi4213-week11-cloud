# SDI 4213 Week 11 - Cloud Deployment Starter

This repository contains the Help Desk / Service Request Tracker used for the Week 11 individual exercise.

## Week 11 Goal
Deploy the containerized application to a real cloud web service and connect it to a managed PostgreSQL database. The application should be publicly reachable through HTTPS and retain ticket data across application redeployments.

## Local Run

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

macOS/Linux activation:

```bash
source .venv/bin/activate
```

The local version uses SQLite unless `DATABASE_URL` is configured.

## Tests

```bash
python -m pytest -v
```

## Docker

```bash
docker build -t helpdesk-cloud:week11 .
docker run --rm -p 8501:8501 -e DEPLOY_ENV=Local-Docker helpdesk-cloud:week11
```

Open `http://localhost:8501`.

## Cloud Deployment
Live application: https://week11-helpdesk.onrender.com

The app runs as a Docker web service on Render (Free plan, Ohio) and stores tickets in a managed Render PostgreSQL database. Render builds the `Dockerfile` and redeploys automatically when `main` changes. `DATABASE_URL`, `DEPLOY_ENV`, and `APP_VERSION` are set as environment variables in the Render dashboard, and the health check path is `/_stcore/health`.

Changes follow the branch, pull request, CI, merge to `main` workflow.

Follow the Week 11 Individual Exercise document in `docs/` for the full steps.

## Security
- Do not commit `.env`.
- Do not place database passwords in source code.
- In the cloud dashboard, environment-variable names may be visible in screenshots, but secret values must be hidden.
