<div align="center">

# 🔁 Loop Library

**The most complete, credited collection of AI-agent _loops_ — repeatable workflows you hand to a coding agent (Claude Code, Cursor, Codex, Gemini CLI…) that iterate a process until a stopping condition is met.**

[![Awesome](https://img.shields.io/badge/awesome-yes-c5203e.svg)](https://github.com/keysersoose/loop-library)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)
![Loops](https://img.shields.io/badge/loops-50%2B-8957e5.svg)

*Refactor until the architecture is clean. Add tests until 100%. Hunt bugs until none remain.*
*You bring the vision — the loop brings the senior engineer.*

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
- [Operations](#operations)
- [DevOps & infrastructure](#devops--infrastructure)
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

---

## Testing & evaluation

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **The Quality Streak Loop** | Test realistic scenarios; when one fails, document it and fix it. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Full Product Evaluation Loop** | Generate N realistic scenarios, each with explicit success criteria. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Self-Improving Champion Loop** | Iterative optimization with a budget, scoring, and gate checks. | Jose C. Munoz | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Devil's-Advocate Loop** | Argue against your own design — via a critic sub-agent — until it survives. | Anonymous | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **TDAD — Test-Driven Agentic Development** | Use a code dependency graph for blast-radius before each change; cut agent regressions. | (research) | [arXiv](https://arxiv.org/pdf/2603.17973) |

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
| **The SEO/GEO Visibility Loop** | Audit crawlability, indexation, and structured data. | Matthew Berman | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Product Update Podcast Loop** | Generate a short 3–5 minute podcast episode about new features. | Pierson Marks | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

---

## Design

| Loop | What it does | Creator | Source |
|------|--------------|---------|--------|
| **War Loops: Autonomous Frontend Designer** | Point it at a URL or image and produce iterative design builds. | Swayam | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Boeing 747 Benchmark** | Build the most realistic Boeing 747 you can in Three.js — a model-capability benchmark. | @victormustar | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |
| **The Infinite Clickbait Loop** | Generate ten thumbnail concepts and score each against a rubric. | @Alex_FF | [Forward Future](https://signals.forwardfuture.ai/loop-library/) |

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

---

## 🛠 Tools & harnesses (run-it-yourself loop repos)

Open-source repos that *run* the loop for you.

| Repo | What it gives you | Creator | Source |
|------|-------------------|---------|--------|
| **loop-engineering** | Patterns, starters & CLI tools (`loop-audit`, `loop-init`, `loop-cost`) for loop engineering. | Cobus Greyling | [github](https://github.com/cobusgreyling/loop-engineering) |
| **autoloop** | Agent-agnostic iterative-optimization loops for Claude Code, Codex, Cursor, OpenCode, Gemini CLI. | Arm Gabrielyan | [github](https://github.com/armgabrielyan/autoloop) |
| **agentic-loop** | Autonomous Claude Code toolkit based on RALPH + PRD-driven development. | allierays | [github](https://github.com/allierays/agentic-loop) |
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
- **[Andrej Karpathy](https://github.com/yibie/awesome-autoresearch)** — autoresearch.
- The researchers behind **ReAct, Reflexion, Self-Refine, OPRO, TextGrad, DSPy, and PromptBreeder**, and the maintainers of every tool linked above.

Attribution wrong or want your loop linked differently (or removed)? [Open an issue](https://github.com/keysersoose/loop-library/issues) — we fix these first.

---

## Contributing

Found a loop? Made one? PRs and issues welcome — see **[CONTRIBUTING.md](./CONTRIBUTING.md)**. One loop per row: name, one-line description, creator, source link. **Star the repo** if it saved you time — it's how other builders find it. ⭐

## License

The **curation, descriptions, and original loops in this repo** (e.g. `loops/senior-loops.md`) are **[MIT licensed](./LICENSE)**. **Linked loops belong to their original authors** under whatever terms their sources set — this repo indexes and credits them, it does not relicense them.
