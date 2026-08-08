# ClauseGuard API Reference

## Endpoints

### 1. Document Management
- `POST /api/documents/upload` - Upload document (PDF, DOCX, TXT, MD)
- `GET /api/documents` - List all uploaded documents
- `DELETE /api/documents/{id}` - Delete document and associated vector chunks

### 2. Question Answering
- `POST /api/qa/ask` - Submit query to `ComplianceAuditorAgent`
  - Body: `{ "question": string, "document_ids": string[] }`
  - Response: `{ "answer": string, "citations": Citation[], "verified": boolean }`

### 3. Compliance Audits
- `POST /api/audit/run` - Run compliance audit against rule set
  - Body: `{ "document_id": string, "rules": string[] }`
  - Response: `{ "audit_id": string, "status": "pending", "report": AuditReport }`
- `POST /api/audit/{id}/approve` - Human approval of audit report (status -> "approved")
- `POST /api/audit/{id}/reject` - Reject audit report (status -> "rejected")

### 4. History & Analytics
- `GET /api/history` - Retrieve query and audit history

### 5. System Health
- `GET /health` or `GET /api/health` - Health check endpoint
