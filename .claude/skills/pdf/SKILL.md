---
name: pdf
description: Read, create, edit, merge, split, and process PDF files. Covers pypdf for structure, pdfplumber for text/table extraction, reportlab for creation, and CLI tools (pdftotext, qpdf, pdftk) for common operations.
license: Complete terms in LICENSE.txt
---

# PDF Skill

Read, create, and manipulate PDF files. Use when PDFs are the primary input or output.

## Quick Reference

| Task | Library/Tool |
|------|-------------|
| Read/merge/split/rotate | pypdf |
| Extract text with layout | pdfplumber |
| Extract tables | pdfplumber + pandas |
| Create new PDFs | reportlab |
| CLI text extraction | pdftotext |
| Merge/split/rotate | qpdf or pdftk |

## Reading with pypdf

```python
from pypdf import PdfReader, PdfWriter, PdfMerger

# Read
reader = PdfReader("file.pdf")
for page in reader.pages:
    print(page.extract_text())

# Merge
merger = PdfMerger()
for f in ["a.pdf", "b.pdf"]:
    merger.append(f)
merger.write("merged.pdf")

# Split
writer = PdfWriter()
writer.add_page(reader.pages[0])
writer.write("page1.pdf")
```

## Extracting Text with Layout (pdfplumber)

```python
import pdfplumber

with pdfplumber.open("file.pdf") as pdf:
    for page in pdf.pages:
        print(page.extract_text(layout=True))
```

## Extracting Tables

```python
import pdfplumber, pandas as pd

with pdfplumber.open("file.pdf") as pdf:
    tables = pdf.pages[0].extract_tables()
    df = pd.DataFrame(tables[0][1:], columns=tables[0][0])
```

## Creating PDFs (reportlab)

```python
from reportlab.pdfgen import canvas
from reportlab.lib.pagesizes import letter

c = canvas.Canvas("output.pdf", pagesize=letter)
c.setFont("Helvetica", 12)
c.drawString(72, 700, "Hello, world")
c.showPage()
c.save()
```

**Important**: Do not use Unicode subscript/superscript characters in ReportLab. Use XML markup instead:
```python
c.drawString(72, 700, "H<sub>2</sub>O")  # correct approach
```

## CLI Operations

```bash
# Extract text
pdftotext input.pdf output.txt
pdftotext -layout input.pdf output.txt  # preserve layout

# Merge
qpdf --empty --pages a.pdf b.pdf -- merged.pdf

# Split (extract pages 1-3)
qpdf input.pdf --pages . 1-3 -- output.pdf

# Rotate
qpdf input.pdf --rotate=90:1 -- output.pdf
```

## Common Tasks

```python
# OCR a scanned document
import subprocess
subprocess.run(["ocrmypdf", "scanned.pdf", "searchable.pdf"])

# Add watermark
from pypdf import PdfReader, PdfWriter
stamp = PdfReader("watermark.pdf").pages[0]
writer = PdfWriter()
for page in PdfReader("original.pdf").pages:
    page.merge_page(stamp)
    writer.add_page(page)
writer.write("watermarked.pdf")

# Password protect
writer = PdfWriter()
# ... add pages ...
writer.encrypt("user_password", "owner_password")
writer.write("protected.pdf")
```

## Dependencies

```bash
pip install pypdf pdfplumber reportlab ocrmypdf
apt install poppler-utils pdftk
```
