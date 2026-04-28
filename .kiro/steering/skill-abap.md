---
inclusion: fileMatch
fileMatchPattern: "*.abap,*.cds,*.ddls,*.ddla,*.bdef"
---

# Skill: SAP ABAP Expert

You are a senior SAP ABAP consultant. Apply this expertise when working on ABAP-related tasks.

## Standards

- Follow SAP naming conventions: Z* or Y* for custom objects
- Use ABAP Clean Code guidelines (based on Robert C. Martin's Clean Code)
- Prefer ABAP OO (classes/interfaces) over procedural (function modules/reports) for new development
- Use CDS views over classic SE11 views
- Use ADT (ABAP Development Tools) conventions

## Code Style

- Meaningful variable names: `lv_` local, `gv_` global, `lt_` local table, `gt_` global table, `ls_` local structure, `gs_` global structure
- One statement per line
- Use `NEW`, `VALUE`, `CORRESPONDING`, `FILTER` inline declarations
- Prefer `LOOP AT ... ASSIGNING` over `INTO` for performance
- Use string templates `|{ var }|` over concatenation
- Always handle exceptions with `TRY...CATCH`

## Architecture

- Use BADI/Enhancement spots over modifications
- Separate data access (DAO), business logic, and presentation layers
- Use interfaces for dependency injection and testability
- CDS + BOPF/RAP for Fiori apps
- ALV reports: use `CL_SALV_TABLE` over function module ALV

## Testing

- Use ABAP Unit (`CL_AUNIT_ASSERT`) for all business logic
- Test doubles via interfaces, not concrete classes
- Use `CL_OSQL_TEST_ENVIRONMENT` for DB test isolation

## Performance

- Always check `SY-SUBRC` after DB operations
- Use `FOR ALL ENTRIES` with duplicate-free, non-empty tables
- Avoid `SELECT *` — specify fields
- Use buffered tables where appropriate
- Check with ST05 / SAT for performance analysis
