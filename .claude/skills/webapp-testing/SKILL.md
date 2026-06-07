---
name: webapp-testing
description: Test local web applications using Playwright. Verifies frontend functionality, debugs UI behavior, captures screenshots, and inspects browser logs. Includes helper scripts for managing server lifecycle.
license: Complete terms in LICENSE.txt
---

# Web App Testing

Tests local web applications using native Python Playwright scripts.

## Setup

Main helper: `scripts/with_server.py` — manages server lifecycle and supports multiple concurrent servers.

Always run scripts with `--help` first rather than reading source code (bundled scripts can be large and consume context).

## Decision Framework

```
Is the app static HTML?
  → YES: Read the file directly, no server needed
  → NO: Is a server already running?
      → YES: Connect to it
      → NO: Use with_server.py to start one
```

## Core Guidance

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=True)  # always headless
    page = browser.new_page()
    page.goto("http://localhost:3000")
    page.wait_for_load_state("networkidle")     # wait before inspecting dynamic content
    
    # reconnaissance: inspect DOM first
    content = page.content()
    
    # then act
    page.click("button#submit")
    page.screenshot(path="screenshot.png")
    
    browser.close()
```

## Key Rules

- **Always launch Chromium in headless mode**
- **Wait for `networkidle` before inspecting dynamic app state**
- **Close the browser** after completing automation
- **Read DOM first** (reconnaissance), then act — don't guess selectors
- Treat bundled scripts as black boxes — don't read their source for selectors

## Patterns

### Element Discovery

```python
# Find elements before interacting
elements = page.query_selector_all("[data-testid]")
for el in elements:
    print(el.get_attribute("data-testid"), el.text_content())
```

### Screenshots

```python
page.screenshot(path="debug.png", full_page=True)
```

### Console Logs

```python
page.on("console", lambda msg: print(f"[{msg.type}] {msg.text}"))
```

## When to Test

- Present the artifact or change to the user first
- Only run tests when specifically requested or when debugging an issue
- Avoid upfront testing that adds latency before the user sees results

## Examples

See `examples/` directory for:
- Element discovery scripts
- Static HTML automation
- Console log inspection
