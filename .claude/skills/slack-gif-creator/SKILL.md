---
name: slack-gif-creator
description: Create animated GIFs optimized for Slack — emoji (128x128) or message (480x480). Covers the GIFBuilder Python toolkit, drawing with PIL, animation techniques (bounce, pulse, spin, fade), and optimization for file size.
license: Complete terms in LICENSE.txt
---

# Slack GIF Creator

Creates animated GIFs optimized for Slack using Python (Pillow + imageio).

## Slack Requirements

| Use case | Dimensions | Frame rate | Colors | Duration |
|----------|-----------|------------|--------|----------|
| Custom emoji | 128×128px | 10–30 FPS | 48–128 | < 3s |
| Message GIF | 480×480px | 10–30 FPS | 48–128 | < 5s |

## Core Workflow (GIFBuilder)

```python
from gifbuilder import GIFBuilder

builder = GIFBuilder(width=128, height=128)

for frame_num in range(30):
    frame = builder.new_frame()
    t = frame_num / 30  # 0.0 → 1.0 progress
    
    # Draw on frame
    frame.ellipse(
        [(48, 48), (80, 80)],
        fill=builder.lerp_color("#ff6b6b", "#4ecdc4", t)
    )
    
    builder.add_frame(frame, duration=50)  # 50ms = 20fps

builder.save("output.gif", colors=64, optimize=True)
```

## Drawing with PIL

```python
from PIL import Image, ImageDraw

img = Image.new("RGBA", (128, 128), (0, 0, 0, 0))
draw = ImageDraw.Draw(img)

# Shapes
draw.ellipse([(10, 10), (50, 50)], fill="#ff6b6b", outline="#cc0000", width=2)
draw.rectangle([(60, 10), (120, 50)], fill="#4ecdc4")
draw.line([(10, 70), (120, 70)], fill="#ffffff", width=3)

# From uploaded image
base = Image.open("icon.png").resize((128, 128))
img.paste(base, (0, 0), base)
```

## Animation Techniques

**Bounce**: `y = center + amplitude * abs(sin(t * π))`  
**Pulse**: `scale = 1 + 0.1 * sin(t * 2π)`  
**Spin**: `angle = t * 360`  
**Fade in**: `alpha = int(255 * t)`  
**Slide**: `x = start + (end - start) * easing(t)`  
**Zoom**: `size = int(base_size * (0.5 + 0.5 * t))`  
**Particle**: spawn particles with velocity + gravity each frame

## Easing Functions

```python
def ease_in_out(t):
    return t * t * (3 - 2 * t)

def ease_out(t):
    return 1 - (1 - t) ** 3

def bounce_out(t):
    if t < 1/2.75:
        return 7.5625 * t * t
    elif t < 2/2.75:
        t -= 1.5/2.75
        return 7.5625 * t * t + 0.75
    # ... etc
```

## Design Principles

- **Thickness**: shapes should have enough weight to read at small sizes
- **Contrast**: strong value contrast, especially for dark Slack themes
- **Color**: use 3–5 colors maximum for clean quantization
- **Loop**: animations should loop seamlessly (end state = start state)
- **Polish**: spend time on easing curves — they make the difference

## Optimization

Reduce file size by:
- Fewer frames (drop to 10fps for simple motion)
- Fewer colors (`colors=32` instead of `colors=128`)
- Smaller dimensions if allowed
- `optimize=True` in save options
- Crop to actual content bounds

## Dependencies

```bash
pip install pillow imageio numpy
```
