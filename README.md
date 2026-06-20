<div align="center">

# 🔁 Loop Library

**The most complete, credited collection of AI-agent _loops_ — repeatable workflows you hand to a coding agent (Claude Code, Cursor, Codex, Gemini CLI…) that iterate a process until a stopping condition is met.**

[![Awesome](https://img.shields.io/badge/awesome-yes-c5203e.svg)](https://github.com/keysersoose/loop-library)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)
![Loops](https://img.shields.io/badge/loops-133-8957e5.svg)
![Domains](https://img.shields.io/badge/domains-19-1f6feb.svg)

*Refactor until the architecture is clean. Add tests until 100%. Hunt bugs until none remain.*
*You bring the vision — the loop brings the senior engineer.*

### 🔎 [**Browse & copy every loop interactively → keysersoose.github.io/loop-library**](https://keysersoose.github.io/loop-library/)
*Every loop ships with a ready-to-paste **prompt**. Search, filter, copy one — or grab them all:*
**⬇ [Download all 133 prompts (`ALL-LOOPS.md`)](./ALL-LOOPS.md)** · **[`loops.json`](./loops.json)** (machine-readable) · *one click, no link-chasing.*

</div>

---

## What is a loop?

A loop is a prompt that doesn't stop at "done once." It **repeats a process until a condition is met.** Progress lives in your files, tests, and git history — not in the chat window — so the agent can run fresh context every pass and keep going long after a single prompt would have quit.

A good loop specifies five things *(framing credit: [Forward Future Loop Library](https://signals.forwardfuture.ai/loop-library/))*:

| Part | Question it answers |
|------|---------------------|
| **Trigger** | When does the loop start? |
| **Action** | What does it do each pass? |
| **Proof** | How does it *verify* progress — a test, a scan, a screenshot — not its own opinion? |
| **Memory** | What carries state between passes (files, a TODO, git)? |
| **Stopping condition** | When does it exit — and what's the safety cap so it can't spin forever? |

```mermaid
flowchart LR
  T([Trigger]) --> A[Action]
  A --> P{Proof?}
  P -- not yet --> M[(Memory:<br/>files · TODO · git)]
  M --> A
  P -- passed --> X([Exit ✓])
  A -. safety cap .-> S([Stop &amp; ask])
```

> This repo is a **credited index.** Every loop links to its **original source** and names its **original creator** — the loops belong to the people who made them. Wrong credit? [Open an issue](https://github.com/keysersoose/loop-library/issues) and we'll fix it immediately.

---

## Contents

- [⭐ Start here — foundational loops](#-start-here--foundational-loops)
- [Engineering](#engineering)
- [Testing & evaluation](#testing--evaluation)
- [Prompt & model optimization](#prompt--model-optimization)
- [Research & data science](#research--data-science)
- [Security & red-teaming](#security--red-teaming)
- [Writing & content](#writing--content)
- [Design](#design)
- [Accessibility](#accessibility)
- [Data & analytics](#data--analytics)
- [International (translated)](#international-translated)
- [Marketing & growth](#marketing--growth)
- [Support & sales](#support--sales)
- [Operations](#operations)
- [DevOps & infrastructure](#devops--infrastructure)
- [Autonomous coding agents (loop-based)](#autonomous-coding-agents-loop-based)
- [Loop frameworks (GitHub)](#loop-frameworks-github)
- [🛠 Tools & harnesses (run-it-yourself loop repos)](#-tools--harnesses-run-it-yourself-loop-repos)
- [📚 Patterns & theory (the research behind loops)](#-patterns--theory-the-research-behind-loops)
- [Full loops included in this repo](#full-loops-included-in-this-repo)
- [Credits & sources](#credits--sources)
- [Contributing](#contributing)
- [License](#license)

---

## ⭐ Start here — foundational loops

The patterns that defined loop-driven development.

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Ralph (Ralph Wiggum) Loop** | Feed the *same* prompt to an agent in an infinite shell loop; each pass gets fresh context, state survives in files + git. The origin of loop-driven development. | Geoffrey Huntley | [ghuntley.com/loop](https://ghuntley.com/loop/) |
| **autoresearch** | Point an agent at a measurable script; it proposes a change, runs a time-boxed (5-min) experiment, keeps it if the metric improves, reverts if not — all night. 66k+ stars. | Andrej Karpathy | [explainer](https://kingy.ai/ai/autoresearch-karpathys-minimal-agent-loop-for-autonomous-llm-experimentation/) · [awesome list](https://github.com/yibie/awesome-autoresearch) |
| **The Senior Loops** ⭐ | Five build loops (spec → plan → test → security → critic) that force AI output to senior-engineer quality. *Full text in this repo.* | [keysersoose](https://github.com/keysersoose) | [loops/senior-loops.md](./loops/senior-loops.md) |

---

## Engineering

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
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
| **The Loop Harness Verification Loop** | Have a *second* agent session verify the staged work against the criteria. | Istasha | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Fresh-Clone Loop** | Clone into a clean, empty environment and follow the README — to catch setup gaps. | 0xUmbra | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The LLM Codegen Workflow** | Brainstorm a spec (LLM asks one question at a time) → generate a `prompt_plan.md` + `todo.md` → feed prompts to the agent in order. | Harper Reed (popularized by Simon Willison) | [harper.blog](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/) |
| **The Multi-File Refactor Loop** | Plan the change, apply rule-based transforms across call sites, run tests after each, repeat until behavior is preserved and clean. | (community) | [Augment Code](https://www.augmentcode.com/learn/automate-multi-file-code-refactoring-with-ai-agents-a-step-by-step-guide) |
| **The Code Migration Loop** | "Environment-in-the-loop": plan → set up env → migrate → run tests → refine, iterating until the port passes. | (research) | [arXiv](https://arxiv.org/pdf/2602.09944) |
| **The Self-Correcting Agent Loop** | A state-machine loop (LangGraph/CrewAI) with conditional edges: act → check → retry, bounded by iteration limits. | (community) | [guide](https://www.matterai.so/guides/agentic-workflows-building-self-correcting-loops-with-langgraph-and-crewai-state-machines) |
| **The Mobile Closed-Loop Build** | Install on a virtual device, tap through every screen, verify layouts across sizes, fix crashes, repeat until store-ready. | Alexander Zanfir | [writeup](https://medium.com/@alexzanfir/closed-loop-development-how-ai-agents-build-software-while-you-sleep-6df42cd05a85) |
| **Timebox / Ultimatum Loop** | Give an assistant's suggestion a hard time budget; if it doesn't yield value with minimal extra effort, abandon and code manually. | Birgitta Böckeler (Thoughtworks) | [martinfowler.com](https://martinfowler.com/articles/exploring-gen-ai/08-how-to-tackle-unreliability.html) |
| **Guardrails Correction Loop** | Generate → validate; if a check fails, filter or regenerate; stop when output passes all validators or a max-retry cap. | Eugene Yan | [eugeneyan.com](https://eugeneyan.com/writing/llm-patterns/) |

---

## Testing & evaluation

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Quality Streak Loop** | Test realistic scenarios; when one fails, document it and fix it. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Full Product Evaluation Loop** | Generate N realistic scenarios, each with explicit success criteria. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Self-Improving Champion Loop** | Iterative optimization with a budget, scoring, and gate checks. | Jose C. Munoz | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Devil's-Advocate Loop** | Argue against your own design — via a critic sub-agent — until it survives. | Anonymous | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **TDAD — Test-Driven Agentic Development** | Use a code dependency graph for blast-radius before each change; cut agent regressions. | (research) | [arXiv](https://arxiv.org/pdf/2603.17973) |
| **Eval-Driven Development (LLM-as-Judge)** | Write evals first → change → run evals → integrate; route flagged production traces back into a golden dataset. | Eugene Yan (& community) | [eugeneyan.com](https://eugeneyan.com/writing/eval-process/) |
| **Pre-Commit Guard** | A hook that runs the test suite before every commit and blocks the commit while the suite is red. | elorm | [loops.elorm.xyz](https://loops.elorm.xyz/) |
| **Post-Edit Test Guard** | A hook that runs the related tests after each file edit to catch regressions immediately. | elorm | [loops.elorm.xyz](https://loops.elorm.xyz/) |
| **Independent Verifier Pass** | When the implementer claims done, a separate verifier runs build + lint + tests with no access to the implementer's rationale. | elorm | [loops.elorm.xyz](https://loops.elorm.xyz/) |
| **Plan-Execute-Validate (PEV)** | Planner → executor → LLM-scorer; route to retry / replan / complete by quality score; stop on pass or budget. | Manjunath G | [dev.to](https://dev.to/manjunathgovindaraju/building-a-reliable-langgraph-workflow-plan-execute-validate-pev-automated-retries-and-mcp-1pik) |
| **The Iteration Flywheel** | Evaluate quality → debug → change behaviour; tighten the eval step to speed every other step. | Hamel Husain | [hamel.dev](https://hamel.dev/blog/posts/evals/) |
| **Model–Human Alignment Loop** | Iterate the LLM-judge critique prompt until model grades agree with human grades on 25–50 examples. | Hamel Husain | [hamel.dev](https://hamel.dev/blog/posts/evals/) |
| **TDD Red-Green-Refactor (AI-assisted)** | Red→Green→Refactor for AI coding; each phase gates on a hard condition; fall back to manual if regen fails twice. | Paul Sobocinski (Thoughtworks) | [martinfowler.com](https://martinfowler.com/articles/exploring-gen-ai/06-tdd-with-coding-assistance.html) |

---

## Prompt & model optimization

Loops that improve the *prompt or model itself* against a metric.

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **OPRO (Optimization by PROmpting)** | Feed the LLM prompts paired with their scores; it generates better variants, iterating toward higher accuracy. | Google DeepMind (Yang et al.) | [overview](https://billtcheng2013.medium.com/automated-prompt-engineering-part-2-c5745039cd81) |
| **TextGrad** | "Textual gradient descent" — an LLM proposes edits that reduce a textual loss, backpropagated through your pipeline. | Stanford (Yuksekgonul et al.) | [arXiv](https://arxiv.org/pdf/2406.07496) |
| **DSPy** | Program prompts as modules with signatures; a compiler optimizes them against a metric instead of you hand-tuning. | Stanford NLP (Khattab et al.) | [github](https://github.com/stanfordnlp/dspy) |
| **PromptBreeder** | Evolutionary search that mutates and "breeds" prompts, selecting by fitness across generations. | Google DeepMind (Fernando et al.) | [overview](https://futureagi.com/blog/top-10-prompt-optimization-tools-2025/) |

---

## Research & data science

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **autoresearch** | The headline ML loop: edit → time-boxed experiment → measure → keep/revert → repeat. | Andrej Karpathy | [awesome-autoresearch](https://github.com/yibie/awesome-autoresearch) |
| **The AI Scientist** | Autonomous loop: generate research ideas, run experiments, analyze results, write the paper. | Sakana AI (Lu et al.) | [survey](https://arxiv.org/pdf/2503.24047) |
| **Agentomics-ML** | Autonomous ML experimentation loop for genomic/transcriptomic data. | (research) | [arXiv](https://arxiv.org/pdf/2506.05542) |
| **Deep Research Loop** | Planner → search sub-agents → synthesize → "need more?" → loop until coverage is sufficient, then cite. | LangChain (Open Deep Research) | [blog](https://www.langchain.com/blog/open-deep-research) |
| **The MLOps Retraining Loop** | Monitor for drift → when it exceeds threshold, retrain → compare vs current → ship only if better → keep monitoring. | (community) | [guide](https://www.auxiliobits.com/blog/mlops-for-agentic-ai-continuous-learning-and-model-drift-detection/) |
| **DeepSearch Loop** | Iterative search → read → reason over vector/FTS/ripgrep tools; loop until the optimal answer is found. | Han Xiao (Jina AI) | [via Simon Willison](https://simonwillison.net/2025/Mar/4/deepsearch-deepresearch/) |

---

## Security & red-teaming

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The AI Red-Teaming Loop** | Adversarially attack the system (prompt injection, jailbreaks, data leakage), feed results back, re-test on a schedule/CI. | (community) | [AI-Red-Teaming-Guide](https://github.com/requie/AI-Red-Teaming-Guide) |
| **RvB — Iterative Red-Blue Games** | Automate system hardening through repeated red-team-attacks / blue-team-defends rounds. | (research) | [arXiv](https://arxiv.org/pdf/2601.19726) |

---

## Writing & content

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **Self-Refine** | One LLM drafts, critiques its own draft, then revises — looping until a stopping criterion. ~20% avg gains across tasks. | Madaan et al. | [learnprompting](https://learnprompting.org/docs/advanced/self_criticism/self_refine) |
| **Draft → Critique → Finalize** | Force deliberation: generate an idea, critique it against criteria, regenerate from the critique. | (community) | [learnwithparam](https://learnwithparam.com/blog/prompt-engineering-self-critique-refinement) |
| **LLM Peer Review** | Multiple agents review each other's drafts, then privately revise — distributed critique for creative writing. | (research) | [arXiv](https://arxiv.org/pdf/2601.08003) |
| **Chain of Density** | Iteratively rewrite a summary, fusing in missing entities each pass *without* growing the length — denser every loop. | Adams et al. | [arXiv](https://arxiv.org/pdf/2309.04269) · [learnprompting](https://learnprompting.org/docs/advanced/self_criticism/chain-of-density) |
| **The SEO/GEO Visibility Loop** | Audit crawlability, indexation, and structured data. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Product Update Podcast Loop** | Generate a short 3–5 minute podcast episode about new features. | Pierson Marks | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

---

## Design

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **War Loops: Autonomous Frontend Designer** | Point it at a URL or image and produce iterative design builds. | Swayam | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Boeing 747 Benchmark** | Build the most realistic Boeing 747 you can in Three.js — a model-capability benchmark. | @victormustar | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Infinite Clickbait Loop** | Generate ten thumbnail concepts and score each against a rubric. | @Alex_FF | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Three.js Game Loop** | Build a playable loop first, then iterate (playtest → tweak → re-test) until it passes gameplay, visual, perf & release checks. | majidmanzarpour | [github](https://github.com/majidmanzarpour/threejs-game-skills) |
| **VideoAgent** | Agentic video understanding/editing with reflection rounds + adaptive feedback loops that refine the plan via self-evaluation. | HKUDS | [github](https://github.com/HKUDS/VideoAgent) |

---

## Accessibility

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The a11y Audit Loop** | Scan for WCAG violations, apply remediation hints, re-scan until compliant. (Automated tools catch ~30–40% — pair with manual testing.) | snapsynapse | [skill-a11y-audit](https://github.com/snapsynapse/skill-a11y-audit) |
| **Accessibility Review Agents** | Specialist agents that enforce WCAG 2.2 AA so coding agents stop generating inaccessible code. | Community-Access | [github](https://github.com/Community-Access/accessibility-agents) |

---

## Data & analytics

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Text-to-SQL Self-Correction Loop** | Creator generates SQL → Runner executes → Enhancer critiques → regenerate, until the query is executable and semantically correct. | Rudder Analytics | [writeup](https://medium.com/@rudderanalytics/ai-agent-for-sql-queries-and-visualization-using-multi-agent-framework-7f9f3d639108) |
| **The Active-Learning Labeling Loop** | Auto-label high-confidence items, route low-confidence ones to humans, retrain, repeat until a quality/budget stop rule is hit. | (community) | [guide](https://dev.co/ai/ai-assisted-data-labeling-using-active-learning-loops) |

---

## International (translated)

Loops sourced from Chinese-language communities (53AI, Tencent Cloud), translated to English with credit to the original authors.

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **Loop Engineering (循环工程)** | Write the program that *drives* the agent: goal → execute → judge → re-prompt with errors → repeat; stop on budget or judge pass. | Omar (omarsar0); ThinkInAI | [53AI](https://www.53ai.com/news/tishicijiqiao/2026062001243.html) |
| **MetaSkills Self-Bootstrap Loop (元技能自举)** | Agent generates new reusable workflow templates for itself: match → fill → DAG check → quality gate → sandbox → human approval. | geffzhang; via 53AI | [53AI](https://www.53ai.com/news/Assistant/2026061894560.html) |
| **Judge-Model Termination Loop (法官模型)** | Pursue a persistent goal across turns with a *separate* judge model deciding completion (not self-declaration). | Youming Zhang, Tencent Cloud | [Tencent Cloud](https://cloud.tencent.com/developer/article/2669097) |
| **Self-Repair Loop (pass@t)** | Generator → executor (tests) → *separate* feedback model → repair model; stop when a sample passes all tests. | Gao & Wang, Microsoft Research | [writeup](https://cloud.tencent.com/developer/article/2308702) |
| **Prefix-Caching Agent Loop (前缀缓存)** | Tool-call loop where the old prompt stays an exact prefix of the new one, making per-token cost linear via KV-cache reuse. | OpenAI Eng; via Synced | [writeup](https://cloud.tencent.com/developer/article/2624854) |

---

## Marketing & growth

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **Loop Marketing / Growth Loop** | Run small, fast A/B tests on hooks, offers and audiences; roll each learning back into creative, targeting and spend — compounding every cycle. | HubSpot | [hubspot.com](https://www.hubspot.com/loop-marketing) |

---

## Support & sales

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Support Resolution Loop (ATTD)** | Analyze → Train → Test → Deploy: resolve tickets, learn from human-corrected escalations, and improve resolution over time. | Fin AI (Intercom) | [fin.ai](https://fin.ai/learn/ai-agents-resolve-tickets-faster) |

---

## Operations

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Stale-Safe Batch Release Loop** | Exclude stale/unfinished work, combine the valid changes, and release. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Production Data Cleanup Loop** | Remove anything that doesn't meet the allowed definition. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Post-Release Baseline Loop** | Run the standard benchmarks and record the results. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Customer AI Deployment Loop** | Manage one customer AI deployment from priority to production. | AgentLed.ai | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

---

## DevOps & infrastructure

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Terraform Fix Loop** | `validate → plan → apply → verify` — read the error, fix, re-run until the infra is correct. (Constrain scope: fix mode loves to refactor adjacent code.) | (community) | [guide](https://computingforgeeks.com/ai-coding-agents-devops-terraform-ansible-kubernetes/) |
| **Ship PR Until Green** | Implement on a branch, run tests, push, open a PR, wait for CI, and loop until checks pass and it's merge-ready. | elorm | [loops.elorm.xyz](https://loops.elorm.xyz/) |
| **CI Failure Watcher** | Poll CI on an interval; when checks go red, investigate and push fixes until green. | elorm | [loops.elorm.xyz](https://loops.elorm.xyz/) |
| **Deploy Verification Loop** | After a deploy, hit health + smoke endpoints on an interval until everything returns healthy. | elorm | [loops.elorm.xyz](https://loops.elorm.xyz/) |

---

## Autonomous coding agents (loop-based)

The agent frameworks whose whole architecture *is* a loop.

| Agent | The loop it runs | Creator | Source |
|-------|------------------|---------|--------|
| **Aider** | Pair-programming loop with an **architect → editor** two-model mode; edits via diffs, runs against a tree-sitter repo map. | Paul Gauthier | [github](https://github.com/Aider-AI/aider) |
| **SWE-agent** | Agent-computer-interface loop that reads an issue, edits the repo, runs tests, and iterates to a patch. | Princeton NLP | [github](https://github.com/princeton-nlp/SWE-agent) |
| **OpenHands** (ex-OpenDevin) | Multi-agent delegation loop: plan → act → observe across a dev environment. | All-Hands-AI | [github](https://github.com/All-Hands-AI/OpenHands) |
| **AutoGPT** | The original autonomous goal loop: decompose a goal into tasks and execute them until the objective is met. | Significant-Gravitas | [github](https://github.com/Significant-Gravitas/AutoGPT) |
| **BabyAGI** | Task-creation/prioritization/execution loop backed by a vector store of prior results. | Yohei Nakajima | [github](https://github.com/yoheinakajima/babyagi) |

---

## Loop frameworks (GitHub)

Battle-tested open-source repos whose whole job is to run a loop for you — verified live, with star counts.

| Repo | The loop it runs | Creator | Stars | Source |
|------|------------------|---------|-------|--------|
| **agent-skills** | Slash-command suite (`/spec /plan /build /test /review /ship`) — a verifiable multi-phase loop; `/build auto` removes human stepping. | Addy Osmani | ~64k | [github](https://github.com/addyosmani/agent-skills) |
| **claude-engineer** | v3 self-expanding loop: detect a capability gap → generate a new tool → validate → hot-reload → chain tools; bounded by a token cap. | Doriandarko | ~11k | [github](https://github.com/Doriandarko/claude-engineer) |
| **ccg-workflow** | Classify → parallel Codex+Gemini analysis → plan → hard-stop user approval → parallel impl → dual-model cross-review → gates. | fengshao1227 | ~5.6k | [github](https://github.com/fengshao1227/ccg-workflow) |
| **ouroboros** | Socratic interview → immutable spec → decompose → execute → evaluator scores → loop until spec satisfied. | Q00 | ~4.6k | [github](https://github.com/Q00/ouroboros) |
| **EvoAgentX** | Self-evolving agents: evaluators score, then TextGrad/AFlow/EvoPrompt evolve prompts + workflow across iterations. | EvoAgentX | ~3.1k | [github](https://github.com/EvoAgentX/EvoAgentX) |
| **agentic-context-engine (ACE)** | Run → Reflector analyzes the trace → SkillManager updates a persistent Skillbook → restart with it injected; stops when tests pass or after N epochs. | kayba-ai | ~2.5k | [github](https://github.com/kayba-ai/agentic-context-engine) |
| **autoharness** | An outer agent improves your *harness* (prompts, params, context), benchmarks each change on a fixed eval, keeps only wins — overnight. | kayba-ai | ~295 | [github](https://github.com/kayba-ai/autoharness) |
| **lauren** | Drains a *mutable* task queue; each task runs implement→review→fix in its own git worktree and auto-merges; edit the queue mid-run. | ofux | ~9 | [github](https://github.com/ofux/lauren) |
| **claude-code-harness** | Enforces Plan → Work → Review → Ship; spec approved before code, review gated, evidence packaged before release. | Chachamaru127 | ~2.8k | [github](https://github.com/Chachamaru127/claude-code-harness) |
| **awesome-harness-engineering** | Reference index of agent-loop primitives: planning, context, MCP, memory, orchestration, verification, HITL. | ai-boost | ~1.9k | [github](https://github.com/ai-boost/awesome-harness-engineering) |
| **continuous-claude** | Runs Claude Code in a loop: opens PRs, waits for CI, merges, next task — context via a markdown handoff file. | AnandChowdhary | ~1.4k | [github](https://github.com/AnandChowdhary/continuous-claude) |
| **cavekit** | grill → spec → research → review → build over a durable SPEC.md; test failures back-propagate into spec invariants. | JuliusBrussee | ~1k | [github](https://github.com/JuliusBrussee/cavekit) |
| **loki-mode** | Multi-agent autonomous SDLC: Reason-Act-Reflect-Verify cycles + quality gates, from PRD to deployed app. | asklokesh | ~982 | [github](https://github.com/asklokesh/loki-mode) |
| **ralph-loop-agent** | Wraps the Vercel AI SDK in a Ralph outer loop: run → verifyCompletion → feedback → repeat until done/cap. | vercel-labs | ~800 | [github](https://github.com/vercel-labs/ralph-loop-agent) |
| **helixent** | Minimal TypeScript/Bun library for ReAct-style think→act→observe loops with parallel tool calls. | MagicCube | ~582 | [github](https://github.com/MagicCube/helixent) |
| **bernstein** | Manager decomposes goal → agents in isolated worktrees → janitor verifies (tests/lint/types) → merge; loop until a predicate passes. | Alex Chernysh | ~574 | [github](https://github.com/chernistry/bernstein) |
| **self_improving_coding_agent** | Evaluate on benchmarks → archive → let the agent improve its OWN codebase → repeat, stacking gains. | MaximeRobeyns | ~353 | [github](https://github.com/MaximeRobeyns/self_improving_coding_agent) |
| **orch** | CTO agent splits goal into tasks; parallel engineering agents in isolated worktrees; QA verifies; state machine to done. | oxgeneral | ~83 | [github](https://github.com/oxgeneral/orch) |
| **foreman** | Boris-style TUI supervising headless Claude Code agents: plan → ADR/PRD → issues → TDD → e2e, human gates + budget caps. | VisionForge-OU | ~56 | [github](https://github.com/VisionForge-OU/foreman) |
| **millrace** | Governed agentic-loop runtime: stage gates, durable queues, recovery rules that persist state across context windows. | tim-osterhus | ~48 | [github](https://github.com/tim-osterhus/millrace) |
| **great_cto** | Spec synthesis → single human approval gate → scaffold/backend/frontend/test/deploy; risk-tiered gates; stop when a live URL ships. | avelikiy | ~41 | [github](https://github.com/avelikiy/great_cto) |
| **forge** | Idea → R-numbered spec → task DAG → TDD per worktree → reviewer + 4-level verifier; stop on FORGE_COMPLETE or budget. | LucasDuys | ~29 | [github](https://github.com/LucasDuys/forge) |
| **llm-loop** | Plugin for the `llm` CLI: turn-based autonomous loop (`--max-turns`, default 25) with optional tool-call approval. | nibzard | ~17 | [github](https://github.com/nibzard/llm-loop) |
| **pi-ralph** | Agent cycles through named "hats" (roles) triggered by emitted events; stop on a completion-promise string or guard rails. | samfoy | ~13 | [github](https://github.com/samfoy/pi-ralph) |

---

## 🛠 Tools & harnesses (run-it-yourself loop repos)

Open-source repos that *run* the loop for you.

| Repo | What it gives you | Creator | Source |
|------|-------------------|---------|--------|
| **loop-engineering** | Patterns, starters & CLI tools (`loop-audit`, `loop-init`, `loop-cost`) for loop engineering. | Cobus Greyling | [github](https://github.com/cobusgreyling/loop-engineering) |
| **autoloop** | Agent-agnostic iterative-optimization loops for Claude Code, Codex, Cursor, OpenCode, Gemini CLI. | Arm Gabrielyan | [github](https://github.com/armgabrielyan/autoloop) |
| **agentic-loop** | Autonomous Claude Code toolkit based on RALPH + PRD-driven development. | allierays | [github](https://github.com/allierays/agentic-loop) |
| **agent-loop** | A guide + workflows for orchestrating specialized AI personas to build, test, and deploy in a loop. | Saik0s | [github](https://github.com/Saik0s/agent-loop) |
| **ralph** | An autonomous loop that runs until every item in a PRD is complete. | snarktank | [github](https://github.com/snarktank/ralph) |
| **ralph-claude-code** | A Ralph loop for Claude Code with intelligent exit detection. | Frank Bria | [github](https://github.com/frankbria/ralph-claude-code) |
| **codex-autoresearch-harness** | Bash harness to run Karpathy's autoresearch with Codex CLI + an A/B framework. | SarahXC | [github](https://github.com/SarahXC/codex-autoresearch-harness) |
| **autoresearch-guide** | 3,000+ line guide teaching agents to autonomously optimize anything measurable. | Rkcr7 | [github](https://github.com/Rkcr7/autoresearch-guide) |
| **awesome-autoresearch** | A curated list of autoresearch resources. | yibie | [github](https://github.com/yibie/awesome-autoresearch) |

---

## 📚 Patterns & theory (the research behind loops)

The academic patterns every loop is built on.

| Pattern | The idea | Origin | Source |
|---------|----------|--------|--------|
| **ReAct** | Interleave Thought → Action → Observation so reasoning guides tool use and vice versa. | Yao et al. | [explainer](https://www.mindstudio.ai/blog/what-is-react-loop-ai-agent-reasoning) |
| **Reflexion** | Actor + Evaluator + Self-Reflection; verbal self-feedback stored in memory across trials. 91% pass@1 on HumanEval. | Shinn et al. | [NeurIPS](https://proceedings.neurips.cc/paper_files/paper/2023/file/1b44b878bb782e6954cd888628510e90-Paper-Conference.pdf) |
| **Self-Refine** | A single LLM as generator, critic, and refiner, looping with feedback memory. | Madaan et al. | [learnprompting](https://learnprompting.org/docs/advanced/self_criticism/self_refine) |
| **Evaluator-Optimizer** | Generator proposes, evaluator scores, loop until a quality threshold — the generic critic loop. | (Anthropic, *Building Effective Agents*) | [pattern catalogue](https://arxiv.org/pdf/2405.10467) |
| **Self-Consistency / Tree of Thoughts** | Sample many reasoning paths / search a tree of thoughts, then select the best. | Wang et al. / Yao et al. | [pattern catalogue](https://arxiv.org/pdf/2405.10467) |
| **Agent Design Pattern Catalogue** | A catalogue of architectural patterns for foundation-model agents. | Liu et al. | [arXiv](https://arxiv.org/pdf/2405.10467) |
| **Anthropic's Agent Workflow Patterns** | The five canonical patterns: prompt chaining, routing, parallelization, orchestrator-worker, and evaluator-optimizer. | Anthropic | [anthropic.com](https://www.anthropic.com/research/building-effective-agents) |
| **Basic Reflection** | Generator LLM paired with a reflector LLM playing "teacher"; generate → reflect → revise; stop at an iteration cap. | Ankush Gola / LangChain | [langchain](https://www.langchain.com/blog/reflection-agents) |
| **Language Agent Tree Search (LATS)** | Reflection + Monte-Carlo tree search: Select → Expand → Reflect/Evaluate → Backpropagate; stop when solved or depth cap. | Zhou et al. / LangChain | [langchain](https://www.langchain.com/blog/reflection-agents) |
| **On-the-Loop (Harness Loop)** | Humans improve the *harness* that produces artifacts rather than fixing artifacts directly; agents run the inner loop. | Kief Morris (Thoughtworks) | [martinfowler.com](https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html) |

---

## Full loops included in this repo

Loops whose complete, copy-paste text lives here (authored by this repo, MIT-licensed):

- **[Senior Loops](./loops/senior-loops.md)** — the five build loops with exact enter / continue / exit / safety conditions and per-step verification artifacts. Drop into your `CLAUDE.md` and your AI builds like a senior engineer.

> Want the full text of *your* loop hosted here? See [CONTRIBUTING.md](./CONTRIBUTING.md).

---

## Credits & sources

This library stands on the shoulders of the people who invented and shared these loops. Deep thanks to:

- **[Forward Future Loop Library](https://signals.forwardfuture.ai/loop-library/)** — source for many loops here and the *trigger / action / proof / memory / stopping-condition* framing. Contributors there include Matthew Berman, Peter Steinberger, Hiten Shah, Pierson Marks, Lukas Kucinski, Istasha, 0xUmbra, Jose C. Munoz, AgentLed.ai, @victormustar, Swayam, and @Alex_FF.
- **[Geoffrey Huntley](https://ghuntley.com/loop/)** — the Ralph loop & loop-driven development.
- **[elorm](https://loops.elorm.xyz/)** — the loops! library (CI / testing / deploy loops).
- **[Andrej Karpathy](https://github.com/yibie/awesome-autoresearch)** — autoresearch.
- The researchers behind **ReAct, Reflexion, Self-Refine, OPRO, TextGrad, DSPy, and PromptBreeder**, and the maintainers of every tool linked above.

Attribution wrong or want your loop linked differently (or removed)? [Open an issue](https://github.com/keysersoose/loop-library/issues) — we fix these first.

---

## Contributing

Found a loop? Made one? PRs and issues welcome — see **[CONTRIBUTING.md](./CONTRIBUTING.md)**. One loop per row: name, one-line description, creator, source link. **Star the repo** if it saved you time — it's how other builders find it. ⭐

## License

The **curation, descriptions, and original loops in this repo** (e.g. `loops/senior-loops.md`) are **[MIT licensed](./LICENSE)**. **Linked loops belong to their original authors** under whatever terms their sources set — this repo indexes and credits them, it does not relicense them.
