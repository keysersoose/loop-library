# <Loop Name>

> One-line description of what this loop does and when to use it.

**Creator:** <name/handle> · **Category:** <engineering / testing / …> · **Source:** <link if any>

## The loop

```
ENTER when: <the trigger that starts the loop>

Each iteration:
  1. <action step>
  2. <action step>
  3. <produce PROOF — a test result, scan output, screenshot, metric>

CONTINUE while: <a measurable reason to go again — not "until it's good">
EXIT when: <an observable finish line, backed by an artifact>
SAFETY EXIT: <hard cap — max N rounds / no-progress — stop and ask instead of spinning>
```

## Notes

- **Proof:** how each pass verifies real progress (never the model's own opinion).
- **Memory:** what carries state between passes (files / TODO / git).
- **Why it works / gotchas:** <optional>

---
*Copy this file to `loops/your-loop.md`, fill it in, and link it from the README's "Full loops" section. See [CONTRIBUTING.md](../CONTRIBUTING.md).*
