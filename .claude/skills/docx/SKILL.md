---
name: docx
description: Create, read, edit, and manipulate Word documents (.docx). Covers the docx JS library for creation, XML editing for advanced modifications, tracked changes, tables, images, headers/footers, and multi-column layouts.
license: Complete terms in LICENSE.txt
---

# DOCX Skill

Creates, reads, and edits Word documents. A `.docx` file is a ZIP archive containing XML — it can be inspected and modified directly.

## Quick Reference

| Task | Approach |
|------|----------|
| Read content | pandoc or python-docx |
| Create new document | `docx` npm library |
| Edit existing document | Unpack XML → modify → repack |
| Convert to PDF | LibreOffice headless |

## Creating with docx (JavaScript)

```js
import { Document, Paragraph, TextRun, HeadingLevel } from "docx";
import { Packer } from "docx";
import fs from "fs";

const doc = new Document({
  sections: [{
    properties: {
      page: {
        size: { width: 12240, height: 15840 },  // US Letter in DXA (twips)
      }
    },
    children: [
      new Paragraph({
        text: "Document Title",
        heading: HeadingLevel.HEADING_1,
      }),
      new Paragraph({
        children: [new TextRun("Body text here.")],
      }),
    ],
  }],
});

const buffer = await Packer.toBuffer(doc);
fs.writeFileSync("output.docx", buffer);
```

## Critical Rules

- **Always set page size explicitly** — default is A4, not US Letter. US Letter = `{ width: 12240, height: 15840 }` DXA
- **Never use unicode bullets** (`•`, `‣`) — use `LevelFormat.BULLET` from the library
- **Never use `\n` in text runs** — create separate Paragraphs instead
- **Always set table widths in DXA** (both table-level and cell-level)
- Use `ShadingType.CLEAR` for shading, not `ShadingType.SOLID` with white

## Lists

```js
import { LevelFormat, AlignmentType } from "docx";

// Define numbering in Document constructor
const numbering = {
  config: [{
    reference: "my-bullet-list",
    levels: [{
      level: 0,
      format: LevelFormat.BULLET,
      text: "•",
      alignment: AlignmentType.LEFT,
    }],
  }],
};

// Use in paragraphs
new Paragraph({
  text: "List item",
  numbering: { reference: "my-bullet-list", level: 0 },
})
```

## Tables

```js
import { Table, TableRow, TableCell, WidthType } from "docx";

new Table({
  width: { size: 9000, type: WidthType.DXA },
  rows: [
    new TableRow({
      children: [
        new TableCell({
          width: { size: 4500, type: WidthType.DXA },
          children: [new Paragraph({ text: "Cell content" })],
        }),
      ],
    }),
  ],
})
```

## Editing Existing Documents (XML)

1. **Unpack**: `unzip document.docx -d unpacked/`
2. **Edit**: Modify XML in `unpacked/word/document.xml`
3. **Repack**: `cd unpacked && zip -r ../output.docx .`

**Smart quote entities in XML:**
- `'` (apostrophe): `&#x2019;`
- `"` (open): `&#x201C;`
- `"` (close): `&#x201D;`

## Tracked Changes (XML)

```xml
<!-- Insertion -->
<w:ins w:id="1" w:author="Author" w:date="2026-01-01T00:00:00Z">
  <w:r><w:t>inserted text</w:t></w:r>
</w:ins>

<!-- Deletion -->
<w:del w:id="2" w:author="Author" w:date="2026-01-01T00:00:00Z">
  <w:r><w:delText>deleted text</w:delText></w:r>
</w:del>
```

## Convert to PDF

```bash
libreoffice --headless --convert-to pdf document.docx
```

## Dependencies

```bash
npm install docx
pip install python-docx
apt install pandoc libreoffice
```
