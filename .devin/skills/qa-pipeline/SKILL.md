---
name: qa-pipeline
description: Run the full AI QA pipeline for the fake project end to end.
---

# AI QA Pipeline

Run the full QA pipeline by invoking the 10 skills in order:

1. `/context` — Context Gathering & Setup
2. `/requirements` — Requirements Grooming
3. `/checklist` — Atomic Verification Setup
4. `/test-cases` — Test Case Design
5. `/pr-summary` — PR Changes Mapping
6. `/code-review` — Code Analysis & Review
7. `/backend-testing` — Backend Verification (API, DB)
8. `/web-testing` — Web UI Verification
9. `/defect-analysis` — Defect Analysis & Triage
10. `/coverage-critic` — Coverage & Quality Assessment

Synthesize the outputs into a final QA summary with coverage and release readiness.
