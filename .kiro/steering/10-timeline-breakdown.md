---
inclusion: manual
---

# Timeline & Gantt Chart Generation

## Purpose

SINTA produces a realistic, consulting-grade project timeline with Gantt chart visualization. All estimates are derived from actual project artifacts (NCR, FS, TS) and — for SAP projects — from real technical evidence gathered via MCP.

The timeline document is saved to `docs/04-task-breakdown/TIMELINE-[ID]-v[X.X].md`.

## Evidence-Based Duration Derivation

### Rule: No Generic Estimates

Every duration MUST be justified by referencing specific artifacts:

| Duration Input | Source | Example |
|---------------|--------|---------|
| Development effort | FS → REQ count, complexity score, object count from MCP | "3 FORMs × 1.5 days avg = 4.5 days dev" |
| Testing effort | TS → scenario count, step count per scenario | "12 scenarios × 8 avg steps = ~96 test steps → 3 days SIT" |
| Review/approval | NCR → stakeholder count, approval chain | "2 approvers (FC + Business Owner) → 1.5 days review" |
| Bug fix buffer | FS → exception flow count, risk register | "4 exception flows + 3 medium risks → 2 days bug fix" |

### For SAP Projects — MCP-Informed Estimates

When SAP ADT MCP data was gathered in Phase 2, use it to refine estimates:

| MCP Evidence | How It Affects Timeline |
|-------------|----------------------|
| Program source LOC (from `read_object_source`) | >500 LOC existing program → higher integration risk → +1 day buffer |
| Number of includes (from `read_object_structure`) | Multiple includes → parallel dev possible OR dependency chain |
| Table structure (from `read_table_definition`) | Complex key / many fields → longer query dev + more test data prep |
| Package contents (from `list_package_contents`) | Many related objects → wider regression scope → longer SIT |
| Where-used results (from `where_used`) | High usage count → higher risk → more careful testing |
| Existing transport (from `list_transports`) | Open transports on same objects → conflict risk → add resolution time |

**Rule:** In the timeline document, include a "Technical Evidence" section that lists what was found via MCP and how it influenced the estimates.

## Size Classification

Classify based on actual FS content, not assumptions:

| Criteria | How to Measure | Small | Medium | Large |
|----------|---------------|-------|--------|-------|
| REQ count | Count REQ-XXX in FS | 1–2 | 3–5 | 6+ |
| Objects modified | Count from FS Traceability Matrix | 1–2 | 3–5 | 6+ |
| Tables involved | Count from FS Data Requirements | 1–2 | 3–5 | 6+ |
| Test scenarios | Count TS-XXX in TS document | 1–5 | 6–15 | 16+ |
| Exception flows | Count EF-XXX in FS | 0–1 | 2–4 | 5+ |
| Integration points | Count cross-module/system touches | 0–1 | 2–3 | 4+ |
| Business process impact | From NCR description | Minor tweak | Process modification | New process |

**Scoring:** Sum the column positions (Small=1, Medium=2, Large=3). Total 7–10=Small, 11–16=Medium, 17+=Large.

## Duration Benchmarks (Calibrated by Size)

| Activity | Small CR | Medium CR | Large CR | Depends On |
|----------|----------|-----------|----------|-----------|
| Requirement Analysis | 1–2 days | 2–3 days | 3–5 days | NCR complexity |
| CR Drafting & Approval | 1–2 days | 2–3 days | 3–5 days | Stakeholder availability |
| Functional Spec Writing | 2–3 days | 3–5 days | 5–10 days | REQ count, data mapping complexity |
| FS Review & Sign-off | 1 day | 1–2 days | 2–3 days | Number of reviewers |
| Development / Configuration | 3–5 days | 5–10 days | 10–20 days | Object count, LOC, complexity score |
| Unit Testing (Dev) | 1–2 days | 2–3 days | 3–5 days | REQ count, exception flow count |
| Test Scenario Preparation | 1–2 days | 2–3 days | 3–5 days | TS scenario count |
| SIT Execution | 2–3 days | 3–5 days | 5–10 days | TS step count, test data complexity |
| UAT Execution | 2–3 days | 3–5 days | 5–10 days | Business user availability |
| Bug Fix & Retest | 1–2 days | 2–3 days | 3–5 days | Risk register severity |
| Go-Live Preparation | 1 day | 1–2 days | 2–3 days | Transport count, config items |
| Go-Live & Hypercare | 1–2 days | 3–5 days | 5–10 days | Business criticality |

## Consulting Best Practices

### Dependencies & Parallel Tracks
- Show predecessor/successor relationships explicitly
- Identify parallel workstreams (e.g., Test Prep can overlap with Development)
- Mark approval gates as milestones (◆), not tasks
- Identify and highlight the critical path

### Buffer Strategy
- 10% contingency for Small CRs
- 15% contingency for Medium CRs
- 20% contingency for Large CRs
- Place buffer AFTER SIT and AFTER UAT (not at the end)

### Resource Assignment
- Every task must have an owner role
- Roles: PM, Functional Consultant (FC), ABAP Developer, QA, Business User, Basis/Admin
- Show resource loading to identify over-allocation

## Output Format

### 1. Mermaid Gantt Chart

Always include a Mermaid gantt chart with:
- Sections for each phase
- Milestones marked with `milestone, crit`
- Dependencies using `after` syntax
- Weekend exclusions

```mermaid
gantt
    title [PROJECT ID] — [Description]
    dateFormat  YYYY-MM-DD
    excludes    weekends

    section Phase 1 — Analysis & Design
    Requirement Analysis    :req, [start], [duration]
    ...
```

### 2. Detailed Task Table

Per phase, include:

| # | Task | Duration | Start | End | Owner | Predecessor | REQ Trace | Effort (MD) |
|---|------|----------|-------|-----|-------|-------------|-----------|-------------|

### 3. Milestone Summary

| # | Milestone | Target Date | Owner | Predecessor | Status |
|---|-----------|-------------|-------|-------------|--------|
| M1 | CR Approved | [Date] | PM / Business | — | 🔵 |

### 4. RACI Matrix

| Activity | PM | FC | Developer | QA | Business User | Basis |
|----------|----|----|-----------|----|--------------|----|

R = Responsible, A = Accountable, C = Consulted, I = Informed

### 5. Effort Summary by Role

| Role | Phase 1 | Phase 2 | Phase 3 | Total (MD) |
|------|---------|---------|---------|------------|

### 6. Risk-Adjusted Timeline

| Scenario | Total Duration | Go-Live Date | Key Assumption |
|----------|---------------|--------------|----------------|
| Optimistic | X days | [Date] | No bugs, instant approvals |
| Baseline | Y days | [Date] | 1 round bug fix, normal approvals |
| Pessimistic | Z days | [Date] | Multiple cycles, scope creep |

### 7. Technical Evidence (SAP Projects)

For SAP projects, include a section documenting what was found via MCP:

```markdown
## Technical Evidence (from SAP ADT)

| Object | Type | Finding | Impact on Estimate |
|--------|------|---------|-------------------|
| SAPMZPP_CSSD_FINAL_INSP | Program | 850 LOC, 12 FORMs, 3 includes | Medium complexity, +1 day integration |
| RESB | Table | 15 fields, composite key (5 fields) | Standard query, no extra effort |
| ZTBAB0001 | Custom Table | Simple structure, 6 fields | Minimal config effort |
```

### 8. Dependencies & Constraints

| # | Dependency | Type | Impact if Delayed |
|---|-----------|------|-------------------|

### 9. Key Dates

| Date | Event | Notes |
|------|-------|-------|
