---
inclusion: fileMatch
fileMatchPattern: "docs/02-functional-spec/**"
---

# Phase 4: Functional Specification (FS)

Generate detailed FS from approved CR. Save to `docs/02-functional-spec/FS-[ID]-v1.0.md`.

## Sections

1. Overview — Purpose, CR reference, process flow diagram (mermaid)
2. Actors/Roles — Table of roles, descriptions, permissions
3. Functional Requirements — For each FR:
   - REQ trace, actors, preconditions, trigger
   - Main flow (numbered steps)
   - Alternative flows
   - Exception flows
   - Postconditions, business rules applied, acceptance criteria
4. Data Requirements — Entities, attributes, validation rules with error messages
5. Interface Requirements — UI descriptions, API contracts, integration points
6. Non-Functional Requirements — Performance, security, scalability targets
7. Traceability Matrix — REQ → CR → FS → BR mapping
8. Assumptions & Risks — Updated
9. Approval Block — Checklist, instruction to reply "Approved"

## GATE: Do NOT proceed without explicit user approval.
