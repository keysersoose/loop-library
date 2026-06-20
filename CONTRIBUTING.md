# Contributing to Loop Library

Thanks for helping grow the library! This is a **credited index** — every loop points back to its original creator and source.

## Add a loop (the common case)

1. Fork the repo and edit `README.md`.
2. Add **one row** to the right category table:

   ```
   | **Loop name** | One-line description of what it does | Creator name/handle | [source](https://link) |
   ```

3. Rules:
   - **Credit the original creator.** If it's not yours, name the person who made it and link the original (tweet, blog, repo, gist).
   - **Describe it in your own words** — don't paste someone else's copyrighted prompt text. Link to it instead.
   - **One sharp line.** What does the loop *do* and what's its stopping condition?
   - Put it in the right category (Engineering / Testing & evaluation / Operations / Content / Design / Foundational).
4. Open a PR. Title it `add: <loop name>`.

## Add a full loop (your own work)

If the loop is **yours** and you want the complete copy-paste text hosted here:

1. Add a markdown file under `loops/` (e.g. `loops/my-loop.md`).
2. Include: what it does, the full prompt, and the enter / exit / safety conditions.
3. Link it from the **Full loops included in this repo** section of the README.
4. By submitting, you confirm it's your work (or properly licensed) and you're sharing it under this repo's MIT license.

## Fix attribution

Spotted a wrong credit, or want your loop linked differently or removed? **Open an issue** — we'll fix it fast. Correct attribution matters more than completeness.

## What makes a good loop entry

- Has a clear **stopping condition** (and ideally a safety cap so it can't spin forever).
- Verifies progress with **proof** (a test, a scan, a screenshot) — not the model's own opinion.
- Is **repeatable** — it's a process, not a one-shot prompt.
