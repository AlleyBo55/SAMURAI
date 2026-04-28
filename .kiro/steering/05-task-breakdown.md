---
inclusion: fileMatch
fileMatchPattern: "docs/04-task-breakdown/**"
---

# Phase 5: Task Breakdown + Timeline

Generate a comprehensive WBS with effort estimation and project timeline. Save to `docs/04-task-breakdown/TIMELINE-[ID]-v1.0.md`.

## Evidence-Based Estimation

All estimates MUST be derived from actual project artifacts — never from generic templates alone.

### Input Sources for Estimation

| Source | What to Extract | Impact on Estimate |
|--------|----------------|-------------------|
| NCR / CR document | Scope, business process affected, urgency | Overall size classification |
| FS (Functional Spec) | Number of REQs, complexity of flows, exception paths, data mappings | Development & testing effort |
| FS — Data Requirements | Tables involved, query complexity, cross-table joins | DB/query development effort |
| FS — Interface Requirements | Screen changes, ALV modifications, new fields | UI development effort |
| FS — Non-Functional Requirements | Performance targets, security checks | Additional dev + testing effort |
| FS — Traceability Matrix | REQ → Object mapping | Task decomposition basis |

### For SAP Projects — Additional MCP-Based Evidence

When SAP ADT MCP server is available, use it to gather real technical evidence before estimating:

| MCP Tool | What to Check | Impact on Estimate |
|----------|--------------|-------------------|
| `read_object_source` | Read existing program source — measure LOC, complexity, number of FORMs/methods | Accurate dev effort per object |
| `read_object_structure` | Understand class hierarchy, includes, dependencies | Integration complexity |
| `read_table_definition` | Check table fields, key structure, indexes | Query development effort |
| `search_objects` | Find related objects, dependencies, where-used | Impact analysis scope |
| `read_data_element` | Understand field types, domains, value ranges | Validation logic effort |
| `list_package_contents` | See all objects in the package | Regression testing scope |

**Rule:** If MCP data was gathered in Phase 2 (Technical Clarification), reference those findings directly. Do NOT re-estimate from scratch — use the actual object complexity observed.

### Complexity Scoring Per Requirement

For each REQ in the FS, score complexity:

| Factor | Low (1) | Medium (2) | High (3) |
|--------|---------|-----------|----------|
| Tables involved | 1 | 2–3 | 4+ |
| Query complexity | Simple SELECT | JOIN / nested | Dynamic / multi-step |
| UI changes | None | Field additions | New screen / ALV restructure |
| Business logic | Straightforward | Conditional branching | State machine / matrix logic |
| Integration points | None | 1 system | 2+ systems |
| Error handling | Standard message | Custom validation chain | Rollback / compensation logic |

Total score per REQ determines effort multiplier:
- 6–8: Simple (base effort)
- 9–12: Medium (1.5x base)
- 13–18: Complex (2.5x base)

## Task Decomposition Rules

### Granularity
- Each task should be 0.5–3 days. If larger, break it down further.
- Every REQ in the FS must map to at least 1 development task + 1 test task.
- Configuration tasks (parameter setup, table entries) are separate from development.

### Categories
- **DEV** — ABAP coding, program modification, enhancement implementation
- **DB** — Table creation/modification, data migration, index optimization
- **CONFIG** — Parameter maintenance, customizing, transport setup
- **TEST** — Test scenario execution, test data preparation, defect verification
- **DEPLOY** — Transport management, go-live execution, production verification
- **DOC** — Documentation, training material, handover

### SAP-Specific Task Patterns

For SAP ABAP projects, always include these task types:

| Pattern | Tasks to Include |
|---------|-----------------|
| New FORM/method | Code + unit test + code review |
| ALV enhancement | Field catalog change + data population + display logic + visual testing |
| Validation logic | Check logic + error message + ON/OFF switch + positive/negative test |
| Table query | SELECT optimization + index check + performance test |
| Transport | TR creation + TR review + TR release + import verification |

## WBS Format

```markdown
## Work Breakdown Structure

| Task ID | Description | Category | Duration | Dependencies | REQ Trace | Owner | Effort (MD) |
|---------|-------------|----------|----------|-------------|-----------|-------|-------------|
| T-001 | ... | DEV | 1d | — | REQ-001 | Developer | 1.0 |
```

## 3-Point Estimation (PERT)

For each task, estimate using PERT formula: `E = (O + 4M + P) / 6`

| Task ID | Optimistic (hrs) | Most Likely (hrs) | Pessimistic (hrs) | Expected (hrs) | Mandays |
|---------|-----------------|-------------------|-------------------|----------------|---------|
| T-001 | O | M | P | (O+4M+P)/6 | E/8 |

**1 Manday = 8 hours.**

## Effort Summary

| Category | Tasks | Total Mandays |
|----------|-------|---------------|
| Development (DEV) | T-001, T-002, ... | X |
| Database (DB) | T-00x | X |
| Configuration (CONFIG) | T-00x | X |
| Testing (TEST) | T-00x | X |
| Deployment (DEPLOY) | T-00x | X |
| Documentation (DOC) | T-00x | X |
| **Subtotal** | | **X** |
| Contingency Buffer (15%) | | X |
| **Grand Total** | | **X** |
