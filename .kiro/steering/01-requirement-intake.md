---
inclusion: fileMatch
fileMatchPattern: "docs/01-change-request/**"
---

# Phase 1: Requirement Parsing

Parse user input into structured requirements.

## Process

1. Extract each distinct requirement, assign REQ-XXX IDs
2. Classify: Type (Feature/Enhancement/Bug/Config/Integration), Priority, Module
3. Flag ambiguities — list clarification questions
4. Draft acceptance criteria per requirement (Given/When/Then)
5. Log assumptions

## Output Format

| REQ ID | Description | Type | Priority | Module |
|---|---|---|---|---|
| REQ-001 | ... | Feature | High | ... |

Acceptance Criteria:
- AC-001-01: Given [X], When [Y], Then [Z]

Clarifications Needed:
- Q1: [question about REQ-XXX]

Assumptions:
- A-001: [assumption] → Pending Confirmation

End with: "Please review and confirm requirements before I generate the Change Request."
