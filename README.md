# Senior Loops

**5 loops that make your AI build like a senior engineer.**
A drop-in for Claude Code, Cursor, or any AI coding agent.

> In 2025 an AI coding agent deleted a company's production database — during a code freeze — then admitted it "panicked." Vibe coding is incredible. It just doesn't think like a senior engineer.
>
> These loops make it.

---

## The problem

AI writes features fast — then skips the things that kill apps in production: auth, data isolation, secrets, edge cases, tests. In Veracode's 2025 test, ~45% of AI-generated code introduced a known security flaw with no human review. The AI gets you to "it works." It doesn't get you to "it's safe to ship."

Senior engineers close that gap with a fixed process they run on **every** feature. These 5 loops give your AI that process.

---

## The 5 loops

| # | Loop | The rule | Catches |
|---|------|----------|---------|
| 1 | **Spec** | Never code until the AI can say what "done" looks like | building the wrong thing |
| 2 | **Plan** | Smallest reversible change + know the blast radius | "what else does this touch?" fires |
| 3 | **Test-First** | A green test you never saw fail is a test you can't trust | happy-path-only code, silent regressions |
| 4 | **Security** | Treat the AI's code like a stranger wrote it | auth holes, leaked data, injection, hallucinated deps |
| 5 | **Critic** | The AI that wrote it can't be the one that grades it | "looks right" but is wrong |

Plus a **Self-Heal loop** that fires on any failure (one hypothesis at a time, fix the root cause, revert anything that makes it worse).

The full version — each loop with exact **enter / continue / exit / safety-exit** conditions and per-step verification artifacts — is in **[`SENIOR-LOOPS.md`](./SENIOR-LOOPS.md)**.

---

## Quick start

1. Copy [`SENIOR-LOOPS.md`](./SENIOR-LOOPS.md) into your project's `CLAUDE.md` (or keep it as `LOOPS.md` and tell your agent: *"follow LOOPS.md"*).
2. Describe your idea.
3. The loops do the rest: **spec → plan → test → secure → critic → ship.**

You bring the vision. The loops bring the senior engineer.

### Try just one first

Paste this into your `CLAUDE.md` to feel the difference immediately — it's the Spec loop in miniature:

```
Before writing any code, answer:
- who is allowed to do this?
- whose data can they see?
- what happens on bad / empty input?
- what breaks at 100x scale?
Do not write code until all 4 are answered.
```

---

## One honest thing

These loops **raise the floor, not the ceiling.** A prompt can't *force* an LLM — it can skip a step, fake a checkbox, or "review" its own code. They don't replace CI, a human reviewer, or your own eyes on the output.

What they *do*: make your AI run the senior-engineer process by default, and tell you exactly what to demand on every feature. The two loops worth enforcing for real (with hooks / CI), not just instructing, are **Security** and **Critic** — because "did you actually run a fresh reviewer and a scanner?" is the most skippable, highest-stakes step.

---

## License

MIT — use it, fork it, ship it.
