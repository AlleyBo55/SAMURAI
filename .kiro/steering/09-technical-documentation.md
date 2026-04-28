---
inclusion: fileMatch
fileMatchPattern: "docs/07-technical-docs/**"
---

# Phase 11: Technical Documentation

Generate full technical docs after implementation is complete. Save to `docs/07-technical-docs/TD-[ID]-v1.0.md`.

## Sections

1. Solution Overview — What was built, architecture diagram (mermaid), tech stack, key decisions
2. Project Structure — Actual file tree with one-line descriptions
3. Setup & Installation — Prerequisites, install steps, env config, DB setup, build/run commands
4. Configuration Reference — All env variables/settings with descriptions (no real values)
5. API Reference (if applicable) — Per endpoint: method, path, auth, request/response examples, FR trace
6. Database Schema — ER diagram (mermaid), table details, indexes, migrations
7. Business Logic — BR-XXX mapped to code locations
8. Error Handling — Error codes, causes, user messages, resolutions
9. Testing — How to run tests, coverage summary, TS-XXX to test file mapping
10. Deployment — Steps, env configs, rollback procedure
11. Troubleshooting — Common issues and fixes
12. Traceability — End-to-end: REQ → CR → FS → Tech → Code → Test → Doc

## Rules

- Document the ACTUAL implementation, not just the spec
- No secrets or PII
- All setup steps must be accurate and reproducible
