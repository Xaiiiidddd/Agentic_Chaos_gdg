# ClauseGuard Developer Guide

## Local Setup

### Backend (Python FastAPI)
```bash
python -m venv venv
source venv/bin/activate
pip install -r backend/requirements.txt
uvicorn backend.app.main:app --reload --port 8000
```

### Frontend (React + Vite)
```bash
npm install
npm run dev
```
Runs full-stack dev server at http://localhost:3000.
