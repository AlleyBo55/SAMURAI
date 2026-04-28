---
inclusion: fileMatch
fileMatchPattern: "docs/03-test-scenarios/**"
---

# Phase 6: Test Scenarios

Generate test scenarios from approved FS. Save to `docs/03-test-scenarios/TS-[ID]-v1.0.md`.

## Coverage Rules

- Every main flow → at least 1 positive test
- Every alternative flow → at least 1 test
- Every exception flow → at least 1 negative test
- Every business rule → tested
- Every validation rule → valid + invalid input tests
- Edge cases identified and covered

## Format Per Scenario

### TS-XXX: [Title]

- Traces To: FR-XXX, REQ-XXX
- Priority: Critical / High / Medium / Low
- Type: Functional / Integration / Regression / Edge Case / Negative

| Step | Action | Input | Expected Result |
|---|---|---|---|
| 1 | ... | ... | ... |

## Coverage Matrix

| REQ ID | FR ID | Test Scenarios | Coverage |
|---|---|---|---|
| REQ-001 | FR-001 | TS-001, TS-002 | Main + Alt + Exception |

Ensure 100% requirement coverage before proceeding.
