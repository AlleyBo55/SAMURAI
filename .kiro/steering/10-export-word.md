---
inclusion: fileMatch
fileMatchPattern: "*.docx"
---

# Export to Word (.docx)

There are TWO export methods. Choose based on document type.

## Method 1: Template-Based (FS, TS, Test Script)

For documents that need corporate branding (headers, logos, table styles), use the Python template generator:

```bash
source .venv/bin/activate && python scripts/generate_from_template.py
```

This uses real .docx templates from `FSTS/` folder and produces branded documents with:
- Corporate header images (logos)
- Styled tables (colored headers, alternating rows, borders)
- Code blocks with Consolas font and grey background
- Proper cover page layout

**Output files:**
- `docs/02-functional-spec/FS-[ID]-v1.0.docx`
- `docs/03-test-scenarios/TS-[ID]-v1.0.docx`
- `docs/03-test-scenarios/MIKA_TestScript_[ID]-v1.0.docx`

**Prerequisites:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install python-docx
```

## Method 2: Pandoc (CR, TB, Tech Spec, Tech Docs, etc.)

For documents that don't need corporate branding, use pandoc:

```bash
pandoc docs/[path]/[file].md -o docs/[path]/[file].docx --from markdown --to docx
```

### Batch Export (All non-branded documents)

```bash
find docs -name "*.md" -exec sh -c 'pandoc "$1" -o "${1%.md}.docx" --from markdown --to docx' _ {} \;
```

**Prerequisites:** `brew install pandoc` (macOS) or `apt install pandoc` (Linux)

## Formatting Notes

- Mermaid diagrams will NOT render in Word — flag this when relevant
- Tables, headings, bold, lists convert cleanly via pandoc
- For branded output, always use Method 1

## When to Offer Export

| Phase | Document | Method |
|-------|----------|--------|
| Phase 2 | CR | Pandoc |
| Phase 4 | FS | Template (Method 1) |
| Phase 6 | TS, Test Script | Template (Method 1) |
| Phase 7 | Task Breakdown | Pandoc |
| Phase 8 | Technical Spec | Pandoc |
| Phase 11 | Technical Docs | Pandoc |
