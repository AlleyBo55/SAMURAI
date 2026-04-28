---
inclusion: fileMatch
fileMatchPattern: "docs/05-technical-spec/**"
---

# Phase 8: Technical Specification

Generate tech spec from FS and task breakdown. Save to `docs/05-technical-spec/TECH-[ID]-v1.0.md`.

## Sections

1. Architecture — System diagram (mermaid), component diagram, tech stack
2. Database Design — ER diagram (mermaid), table definitions, indexes, migration strategy
3. API Design — Endpoints (method, path, request/response), auth, error format
4. Component Design — Per component: responsibility, interfaces, dependencies, key logic
5. Security — Auth mechanism, authorization model, encryption, input validation, OWASP considerations
6. Performance — Expected load, caching, query optimization, scalability
7. Error Handling — Classification, logging, retry policies, user-facing messages

Keep it implementation-ready. Reference FR-XXX and BR-XXX throughout.
