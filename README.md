# ClauseGuard

> Grounded Document Question Answering and Compliance Audit System with Zero-Hallucination Citation Verification.

ClauseGuard ingests contracts, policies, and regulatory documents, allowing users to ask grounded questions and run compliance audits. Every single claim is verified against exact source spans with page numbers and character offsets. If a claim cannot be verified, the system explicitly refuses to guess.

## Core Features
- **Multi-Format Ingestion**: PDF, DOCX, TXT, Markdown parser preserving page & character offsets.
- **RAG & Chroma DB**: Semantic top-K chunk retrieval with document isolation.
- **Custom Agent**: `ComplianceAuditorAgent` with iterative retrieval and verification loop.
- **Custom Skill**: `citation-verifier` performing substring, semantic, and paraphrase verification.
- **Human-in-the-Loop Audits**: Audit reports require explicit human approval before status becomes FINAL.
- **Modern Responsive UI**: Dark mode dashboard, citation viewer, document previewer, audit manager.

## Quickstart
```bash
cp .env.example .env
docker compose up --build
```
Access Frontend at `http://localhost:3000` and API at `http://localhost:8000/health`.

## Project Structure
- `backend/app/` — FastAPI application, RAG pipeline, agents, skills
- `frontend/src/` — React UI (Upload, Ask, Audit, History, Settings)
- `docs/` — Architecture, API Docs, Deployment, and Developer Guides
- `tests/` — Unit, Integration, and Playwright E2E test suites
