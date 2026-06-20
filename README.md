# Loop Library

> A curated, credited collection of **loops** — repeatable workflows you hand to an AI coding agent (Claude Code, Cursor, Codex, …) that make it iterate a process until a stopping condition is met.

[![Awesome](https://img.shields.io/badge/awesome-yes-c5203e.svg)](https://github.com/keysersoose/loop-library)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)
![Loops](https://img.shields.io/badge/loops-30%2B-8957e5.svg)

You bring the vision. The loop brings the senior engineer.

---

## What is a loop?

A loop is a prompt that doesn't stop at "done once." It **repeats a process until a condition is met** — refactor *until* the architecture is clean, add tests *until* coverage is 100%, hunt bugs *until* none remain. Progress lives in your files, tests, and git history, not in the chat.

A good loop specifies five things *(framing credit: [Forward Future Loop Library](https://signals.forwardfuture.ai/loop-library/))*:

| Part | Question it answers |
|------|---------------------|
| **Trigger** | When does the loop start? |
| **Action** | What does it do each pass? |
| **Proof** | How does it *verify* progress (a test, a scan, a screenshot — not self-opinion)? |
| **Memory** | What carries state between passes (files, a TODO, git)? |
| **Stopping condition** | When does it exit — and what's the safety cap so it can't spin forever? |

---

## Contents

- [Foundational / autonomous loops](#foundational--autonomous-loops)
- [Engineering](#engineering)
- [Testing & evaluation](#testing--evaluation)
- [Operations](#operations)
- [Content](#content)
- [Design](#design)
- [Full loops included in this repo](#full-loops-included-in-this-repo)
- [Credits & sources](#credits--sources)
- [Contributing](#contributing)
- [License](#license)

> Each entry links to its **original source** and credits its **original creator**. This repo is an *index* — the loops belong to the people who made them. Where a full prompt is included in this repo, it's noted as such.

---

## Foundational / autonomous loops

The patterns that started "loop-driven development."

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Ralph (Ralph Wiggum) Loop** | Feed the *same* prompt to an agent in an infinite shell loop; each pass gets a fresh context, state survives in files + git. The origin of loop-driven development. | Geoffrey Huntley | [ghuntley.com/loop](https://ghuntley.com/loop/) |
| **ralph** (PRD-driven) | An autonomous loop that keeps running until every item in a PRD is complete. | snarktank | [github.com/snarktank/ralph](https://github.com/snarktank/ralph) |
| **ralph-claude-code** | A Ralph loop for Claude Code with intelligent exit detection. | Frank Bria | [github.com/frankbria/ralph-claude-code](https://github.com/frankbria/ralph-claude-code) |
| **Recursive Self-Improving Agent** | An agent that iteratively improves its own prompts/tooling. | David R. Oliver | [Medium](https://medium.com/@davidroliver/recursive-self-improvement-building-a-self-improving-agent-with-claude-code-d2d2ae941282) |
| **Self-Improving Coding Agents** | A survey of self-improving agent loop techniques. | Addy Osmani | [addyosmani.com](https://addyosmani.com/blog/self-improving-agents/) |
| **TDAD — Test-Driven Agentic Development** | Graph-based impact analysis to cut regressions inside agent loops. | (research) | [arXiv](https://arxiv.org/pdf/2603.17973) |

---

## Engineering

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Senior Loops** ⭐ | Five build loops (spec → plan → test → security → critic) that force AI output to senior-engineer quality. *Full text in this repo.* | keysersoose | [loops/senior-loops.md](./loops/senior-loops.md) |
| **The Docs Sweep** | Review the codebase and bring every doc back in sync with the real implementation. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Architecture Satisfaction Loop** | Refactor — with live tests and commits each step — until the architecture is genuinely clean. | Peter Steinberger | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Sub-50ms Page-Load Loop** | Optimize until every page loads in under 50 ms. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Production Error Sweep** | Read production logs, trace each error to its root cause, and fix it. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The 100% Test Coverage Loop** | Add tests until coverage reaches 100%. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Logging Coverage Loop** | Add logging until every important path emits useful, tested logs. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Nightly Changelog Loop** | Each night, summarize the previous day's changes into the changelog. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Test-Suite Speed Loop** | Make the test suite run as fast as it can. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Repository Cleanup Loop** | Audit branches, PRs, commits, and worktrees, then tidy up. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Ticket-to-PR-Ready Loop** | Turn a ticket into a review-ready patch with the failure defined up front. | Hiten Shah | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Clodex Adversarial-Review Loop** | Run a Codex code review and fix every finding above a set threshold. | Lukas Kucinski | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Loop Harness Verification Loop** | Have a *second* Claude session verify the staged work against the criteria. | Istasha | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Fresh-Clone Loop** | Clone into a clean, empty environment and follow the README — to catch setup gaps. | 0xUmbra | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

---

## Testing & evaluation

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Quality Streak Loop** | Test realistic scenarios; when one fails, document it and fix it. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Full Product Evaluation Loop** | Generate N realistic scenarios, each with explicit success criteria. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Self-Improving Champion Loop** | Iterative optimization with a budget, scoring, and gate checks. | Jose C. Munoz | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Devil's-Advocate Loop** | Argue against your own design — via a critic sub-agent — until it survives. | Anonymous | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

---

## Operations

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Stale-Safe Batch Release Loop** | Exclude stale/unfinished work, combine the valid changes, and release. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Production Data Cleanup Loop** | Remove anything that doesn't meet the allowed definition. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Post-Release Baseline Loop** | Run the standard benchmarks and record the results. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Customer AI Deployment Loop** | Manage one customer AI deployment from priority to production. | AgentLed.ai | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

---

## Content

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The SEO/GEO Visibility Loop** | Audit crawlability, indexation, and structured data. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Product Update Podcast Loop** | Generate a short 3–5 minute podcast episode about new features. | Pierson Marks | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

---

## Design

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Boeing 747 Benchmark** | Build the most realistic Boeing 747 you can in Three.js — a model-capability benchmark. | @victormustar | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **War Loops: Autonomous Frontend Designer** | Point it at a URL or image and produce iterative design builds. | Swayam | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Infinite Clickbait Loop** | Generate ten thumbnail concepts and score each against a rubric. | @Alex_FF | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

---

## Full loops included in this repo

Loops whose complete, copy-paste text lives here (authored by this repo, MIT-licensed):

- **[Senior Loops](./loops/senior-loops.md)** — the five build loops with exact enter / continue / exit / safety conditions and per-step verification artifacts. Drop into your `CLAUDE.md` and your AI builds like a senior engineer.

> Want to add the full text of *your* loop? See [CONTRIBUTING.md](./CONTRIBUTING.md).

---

## Credits & sources

This library stands on the shoulders of the people who invented and shared these loops. Huge thanks to:

- **[Forward Future Loop Library](https://signals.forwardfuture.ai/loop-library/)** — the source for many loops catalogued here, and for the *trigger / action / proof / memory / stopping-condition* framing. Individual loops there are credited to their contributors (Matthew Berman, Peter Steinberger, Hiten Shah, Pierson Marks, Lukas Kucinski, Istasha, 0xUmbra, Jose C. Munoz, AgentLed.ai, @victormustar, Swayam, @Alex_FF, and others).
- **[Geoffrey Huntley](https://ghuntley.com/loop/)** — the Ralph (Ralph Wiggum) loop and loop-driven development.
- **Matthew Berman, Peter Steinberger ([@steipete](https://twitter.com/steipete)), Hiten Shah**, and every other creator linked in the tables above.

If a loop is attributed incorrectly or you'd like yours linked differently (or removed), please [open an issue](https://github.com/keysersoose/loop-library/issues) — we'll fix it immediately.

---

## Contributing

Found a loop? Made one? PRs and issues welcome — see **[CONTRIBUTING.md](./CONTRIBUTING.md)**. One loop per entry: name, one-line description, creator, and a source link.

## License

The **curation, descriptions, and original loops in this repo** (e.g. `loops/senior-loops.md`) are **[MIT licensed](./LICENSE)**. **Linked loops belong to their original authors** under whatever terms those sources set — this repo indexes and credits them, it does not relicense them.
