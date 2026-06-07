---
name: pptx
description: Create, edit, and analyze PowerPoint presentations (.pptx). Read existing files, edit templates by unpacking XML, create from scratch with PptxgenJS. Includes design patterns for layouts, typography, color palettes, and QA workflows.
license: Complete terms in LICENSE.txt
---

# PPTX Skill

Creates, edits, and analyzes PowerPoint files. Use when presentations are the primary input or output.

## Quick Reference

| Task | Approach |
|------|----------|
| Read slide content | `scripts/read_pptx.py` |
| Edit a template | Unpack XML → modify → repack |
| Create from scratch | PptxgenJS |
| Visual overview | Convert to PDF → JPEG images |

## Reading Content

```python
# Extract text from all slides
from pptx import Presentation

prs = Presentation("file.pptx")
for slide in prs.slides:
    for shape in slide.shapes:
        if shape.has_text_frame:
            print(shape.text_frame.text)
```

For raw XML access, unzip the `.pptx` file and inspect `ppt/slides/slide*.xml`.

## Editing Existing Files

1. Analyze template with `scripts/read_pptx.py`
2. Unpack: `unzip file.pptx -d unpacked/`
3. Modify XML in `unpacked/ppt/slides/`
4. Repack: `cd unpacked && zip -r ../output.pptx .`

## Creating from Scratch (PptxgenJS)

```js
const pptx = new PptxGenJS();
const slide = pptx.addSlide();

slide.addText("Title", { x: 0.5, y: 0.5, w: 9, h: 1.5, fontSize: 36, bold: true });
slide.addShape(pptx.ShapeType.rect, { x: 0, y: 0, w: 10, h: 7.5, fill: { color: "1a1a1a" } });

await pptx.writeFile({ fileName: "output.pptx" });
```

## Design Guidance

**Color palettes (examples):**
- Midnight Executive: `#1a1a2e` + `#16213e` + `#e94560`
- Ocean Gradient: `#0f3460` + `#533483` + `#e94560`
- Clean Corporate: `#ffffff` + `#f8f9fa` + `#0066cc`

**Layouts:**
- Two-column: text left, visual right (or reverse)
- Grid: 2×2 or 3×3 feature cards
- Half-bleed image: image occupies 50% of slide

**Typography:**
- Title: 36–48pt, bold
- Body: 18–24pt, regular
- Caption/label: 12–14pt

**Avoid:** Default themes, clip art, all-cap bodies, centered wall-of-text layouts.

## QA Process

1. Extract text with script — verify all content is present
2. Inspect visually: convert to PDF → JPEG for review
3. Check for: overlapping text, missing slides, broken layouts

```bash
libreoffice --headless --convert-to pdf file.pptx
pdftoppm -r 150 output.pdf slide
```

## Dependencies

```bash
pip install python-pptx MarkItDown Pillow
npm install pptxgenjs
apt install libreoffice poppler-utils
```
