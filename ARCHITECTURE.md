# ClauseGuard Architecture Overview

ClauseGuard is a Grounded Document Question Answering & Compliance Audit System engineered for zero-hallucination legal and policy compliance workloads.

## 1. High-Level Architecture
```
[ User UI ] ──> [ React + Vite Frontend ]
                         │
                         ▼
             [ Express / FastAPI Gateway ]
                         │
       ┌─────────────────┴─────────────────┐
       ▼                                   ▼
[ Document Ingestion ]             [ ComplianceAuditorAgent ]
  • File Parsers (PDF/DOCX/TXT)      • Dense Retriever (Top-K)
  • Chunking with Metadata           • Draft Generation
  • Span offsets (Page, Chars)       • citation-verifier skill
       │                                   │
       ▼                                   ▼
[ Chroma Vector DB ] ◄─────────────── [ Verification Gate ]
                                           │ (Refuse if ungrounded)
                                           ▼
                                [ Human Approval (Audit) ]
```

## 2. Key Architectural Components

### A. Grounded Document Ingestion & Chunking (`backend/app/rag/chunker.py`)
- Preserves document IDs, page numbers, character start/end offsets.
- Multi-format parsers (PDF, DOCX, TXT, Markdown).

### B. Dense Vector Store (`backend/app/rag/vector_store.py`)
- Persistent Chroma database storing embeddings with rich metadata.
- Cosine similarity search with configurable top-K retrieval.

### C. Custom Agent: `ComplianceAuditorAgent` (`backend/app/agents/compliance_auditor.py`)
- Orchestrates document Q&A and Compliance Audits.
- Forces citation verification before producing final response.
- Manages human-in-the-loop state (Pending -> Approved / Rejected -> Final).

### D. Custom Skill: `citation-verifier` (`backend/app/skills/citation_verifier.py`)
- Multi-tier verification pipeline:
  1. Substring exact match
  2. Semantic similarity vector overlap
  3. LLM paraphrase verification against exact source span
- If claim verification fails, claim is stripped or query is refused.

## 3. Data Model Schema
- `Document`: `{ id, filename, uploaded_at, page_count, file_size }`
- `Chunk`: `{ id, document_id, text, page_number, char_start, char_end }`
- `Query`: `{ id, question, answer, citations, verified }`
- `AuditReport`: `{ id, document_id, status: "pending" | "approved" | "rejected", rules: [...] }`
