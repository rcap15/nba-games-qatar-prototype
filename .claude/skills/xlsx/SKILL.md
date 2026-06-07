---
name: xlsx
description: Work with Excel files (.xlsx, .xlsm) and tabular data (.csv, .tsv). Create, edit, format, and analyze spreadsheets. Covers financial model standards, formula best practices, pandas for analysis, and openpyxl for formatting.
license: Complete terms in LICENSE.txt
---

# XLSX Skill

Work with Excel files and tabular data. Use when spreadsheets are the primary input or output.

## Core Rules

- Use Excel formulas instead of Python-calculated hardcoded values
- Use pandas for data analysis; openpyxl for formulas and formatting
- Always recalculate formulas using `scripts/recalc.py` after creation
- Zero formula errors before delivery — verify `#REF!`, `#DIV/0!`, `#VALUE!`, `#NAME?`

## Output Standards

- Professional fonts throughout (Calibri or Aptos, not the default)
- Zero formula errors
- Preserve existing template styles when editing

## Financial Model Standards

**Color coding (industry standard):**
- Blue (`#0070C0`): User inputs
- Black: Formula-derived values
- Green (`#00B050`): Internal links (same file)
- Red (`#FF0000`): External links
- Yellow background: Key assumptions

**Number formatting:**
- Currency: `$#,##0.00` or `$#,##0` (no decimals for round numbers)
- Percentages: `0.0%` or `0.00%`
- Years: Format as text, not numbers
- Negatives: Use parentheses `(1,234)` not minus signs

**Model hygiene:**
- All assumptions in separate input cells — never hardcode values in formulas
- Document sources for any hardcoded external data
- Use named ranges for key assumptions

## Working with openpyxl

```python
from openpyxl import load_workbook
from openpyxl.styles import Font, PatternFill, Alignment
from openpyxl.utils import get_column_letter

wb = load_workbook("template.xlsx")
ws = wb.active

# Write a value
ws["B2"] = 100000

# Write a formula
ws["C2"] = "=B2*1.1"

# Format a cell
ws["B2"].font = Font(bold=True, color="0070C0")
ws["B2"].fill = PatternFill("solid", fgColor="E6F3FF")
ws["B2"].number_format = "$#,##0"

wb.save("output.xlsx")
```

## Data Analysis with pandas

```python
import pandas as pd

# Read
df = pd.read_excel("data.xlsx", sheet_name="Sheet1")

# Analyze
summary = df.groupby("category").agg({"revenue": "sum", "units": "count"})

# Write back
with pd.ExcelWriter("output.xlsx", engine="openpyxl") as writer:
    summary.to_excel(writer, sheet_name="Summary")
```

## Formula Best Practices

- Test formulas on sample cells before applying to full range
- Use absolute references (`$A$1`) for constants, relative for ranges
- Prefer `IFERROR()` wrapping for division or lookup formulas
- Use structured table references (`Table1[Revenue]`) for maintainability
- Document complex formulas with cell comments

## After Writing Formulas

Always recalculate to ensure formula values are computed:

```bash
python scripts/recalc.py output.xlsx
```

## Dependencies

```bash
pip install openpyxl pandas xlrd
```
