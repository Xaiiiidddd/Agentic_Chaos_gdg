# ClauseGuard Deployment Guide

## Production Options

### 1. Docker Compose (Recommended for local / single VM deployment)
```bash
cp .env.example .env
docker compose up --build -d
```

### 2. Render / Railway / Fly.io Deployment
1. Connect GitHub Repository.
2. Deploy Dockerfile.backend with env `GEMINI_API_KEY`.
3. Deploy Dockerfile.frontend or static SPA build.
