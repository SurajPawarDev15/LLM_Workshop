# LLM Workshop

A small full-stack example project demonstrating a retrieval-augmented generation (RAG) prototype with a Python backend and a JavaScript frontend. This repository contains a backend that serves LLM-assisted endpoints and a frontend SPA for interacting with them.

## Quick overview

- Backend: Python (FastAPI / minimal Flask-like handlers) located in `backend/`.
- Frontend: JavaScript/React (Vite) located in `frontend/`.
- Local vector store: Chroma data under `backend/chroma_data/` (SQLite file included for quick demos).
- Dev & deployment: Dockerfiles for backend and frontend, plus `frontend/docker-compose.yml`.

## Features

- Retrieval-augmented generation (RAG) demo using local Chroma index.
- Simple REST endpoints for querying the assistant.
- Minimal React UI to call the backend and display responses.

## Repo structure

```
f:/Workshop/LLM_Workshop
├─ backend/
│  ├─ main.py           # backend entrypoint
│  ├─ rag.py            # RAG helpers
│  ├─ requirements.txt  # Python dependencies
│  └─ chroma_data/      # persisted vector DB (SQLite)
├─ frontend/
│  ├─ src/              # React app
│  ├─ package.json
│  └─ Dockerfile
├─ Dockerfile
├─ README.md
└─ notes*.txt
```

## Prerequisites

- Python 3.10+ (recommended)
- Node 16+ / npm or pnpm
- Docker (optional, for containers)

## Backend - run locally

1. Create a virtual environment and install dependencies:

```bash
cd backend
python -m venv .venv
.venv\Scripts\activate    # Windows
pip install -r requirements.txt
```

2. Start the backend service:

```bash
python main.py
# or if there's an ASGI entry: uvicorn main:app --reload --port 8000
```

3. Important files:

- `backend/main.py` — application entrypoint and HTTP handlers.
- `backend/rag.py` — ingestion and retrieval helpers for the Chroma vector store.
- `backend/chroma_data/chroma.sqlite3` — bundled SQLite index for fast demos.

## Frontend - run locally

```bash
cd frontend
npm install
npm run dev
# open http://localhost:5173 (or the port printed by Vite)
```

The UI calls the backend endpoints defined in `backend/` (see `src/api.js`). If you run backend on a non-default port, update the base URL in `frontend/src/api.js`.

## Docker (quick)

Build and run the backend and frontend containers (from repo root):

```bash
docker build -t llm-workshop-backend -f backend/Dockerfile backend
docker build -t llm-workshop-frontend -f frontend/Dockerfile frontend
# Optionally use docker-compose if configured:
cd frontend
docker-compose up -d
```

## Environment variables

- If the backend requires API keys (LLM provider, etc.), store them in a `.env` file in `backend/` or set them in your environment. Example `.env` placeholder:

```
# backend/.env
OPENAI_API_KEY=your_api_key_here
CHROMA_DB_PATH=./chroma_data/chroma.sqlite3
```

If a `.env` file is missing, create it from the example above and replace placeholders.

## Data notes

- `backend/chroma_data/` contains a small SQLite-backed Chroma index used for demos. If you want to recreate it, use the ingestion utilities in `backend/rag.py`.

## Development notes

- Keep Python dependencies in `backend/requirements.txt` and frontend packages in `frontend/package.json`.
- Unit tests (if added) should live in `backend/tests` and `frontend/tests`.

## Troubleshooting

- Backend not reachable: ensure it's running and the CORS settings allow the frontend origin.
- Port conflicts: modify ports in the startup commands or Dockerfiles.
- Missing Python packages: run `pip install -r backend/requirements.txt` again.

## Contributing

1. Fork the repo
2. Create a feature branch
3. Open a pull request with a clear description of changes

## License & contact

This project is provided as-is for demo/learning purposes. Add your preferred LICENSE file if you intend to publish.

---

If you want, I can also:

- add a minimal `.env.example` in `backend/` with placeholders,
- add basic run scripts to `package.json` / a Makefile,
- or generate a short CONTRIBUTING.md.
