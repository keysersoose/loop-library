# Loop Library — All Prompts

> A curated, credited collection of AI-agent loops — repeatable workflows for coding agents (Claude Code, Cursor, Codex, Gemini CLI) that iterate until a stopping condition is met. Each loop ships with a ready-to-paste prompt.

**85 loops** · repo: https://github.com/keysersoose/loop-library · site: https://keysersoose.github.io/loop-library/

_Prompts are original implementations of each loop's technique, written for this library so they are copy-paste ready and license-clean. Credit each creator if you share._


---


## Categories

- [Foundational](#foundational) (3)
- [Engineering](#engineering) (18)
- [Testing & evaluation](#testing--evaluation) (9)
- [Prompt & model optimization](#prompt--model-optimization) (4)
- [Research & data science](#research--data-science) (4)
- [Security & red-teaming](#security--red-teaming) (2)
- [Writing & content](#writing--content) (6)
- [Design](#design) (5)
- [Accessibility](#accessibility) (2)
- [Data & analytics](#data--analytics) (2)
- [Marketing & growth](#marketing--growth) (1)
- [Support & sales](#support--sales) (1)
- [Operations](#operations) (4)
- [DevOps & infrastructure](#devops--infrastructure) (4)
- [Autonomous coding agents](#autonomous-coding-agents) (5)
- [Tools & harnesses](#tools--harnesses) (9)
- [Patterns & theory](#patterns--theory) (6)



## Foundational

### The Ralph (Ralph Wiggum) Loop
*Feed the same prompt to an agent in an infinite shell loop; fresh context each pass, state lives in files + git.*  
**Creator:** Geoffrey Huntley · **Source:** https://ghuntley.com/loop/

```text
You are running inside an infinite shell loop and get a FRESH context every pass. Do not rely on memory of previous runs — all state lives in the repo, in TODO.md, and in git history.

Each pass:
1. Read TODO.md and pick the single most important unchecked item.
2. Implement only that item.
3. Run the full test suite. If green, commit with a clear message and check the item off in TODO.md. If red, fix before committing.
4. Append a one-line note of what you did to PROGRESS.md.

Stop only when every item in TODO.md is checked and the suite is green.
```

### autoresearch
*Propose a change to a measurable script, run a time-boxed experiment, keep it if the metric improves, revert if not.*  
**Creator:** Andrej Karpathy · **Source:** https://github.com/yibie/awesome-autoresearch

```text
You are optimizing a measurable script against a single metric (e.g. validation loss). Work in a loop:
1. Read the current code and the best metric so far (in BEST.md).
2. Propose ONE concrete change with a hypothesis for why it should improve the metric.
3. Apply it and run the time-boxed experiment (same fixed budget every time).
4. If the metric improves, commit and update BEST.md. If not, revert the change.
5. Log the result (change, hypothesis, metric, kept/reverted) to RESULTS.md.
Repeat. Never change the experiment budget or the metric definition.
```

### The Senior Loops
*Five build loops (spec -> plan -> test -> security -> critic) that force AI output to senior-engineer quality.*  
**Creator:** keysersoose · **Source:** https://github.com/keysersoose/loop-library/blob/main/loops/senior-loops.md

```text
For any build request, run these gates in order; a gate can't start until the previous one passes.
1. SPEC: restate the idea as testable acceptance criteria; answer who-can-access, whose-data, what-on-bad-input, what-breaks-at-100x. No code until unambiguous.
2. PLAN: read existing code, state the smallest reversible change + its blast radius.
3. TEST-FIRST: write a failing test (fails for the right reason) -> minimal code -> full suite green.
4. SECURITY: check auth, data isolation, secrets, input validation, safe defaults, real dependencies, least privilege. Fix every finding.
5. CRITIC: a FRESH reviewer (separate session) gets only the diff + spec and tries to break it. Fix real findings. Max 3 rounds.
Only then is it done. Full version: loops/senior-loops.md.
```


## Engineering

### The Docs Sweep
*Review the codebase and bring every doc back in sync with the real implementation.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Sweep the entire repo's documentation against the current implementation. For each doc (README, comments, API docs, examples): verify every claim, command, and signature actually matches the code. Fix each mismatch in the doc to reflect reality. Repeat full passes until a complete pass finds zero discrepancies, then report what changed.
```

### The Architecture Satisfaction Loop
*Refactor with live tests and commits each step until the architecture is genuinely clean.*  
**Creator:** Peter Steinberger · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Refactor this codebase toward a clean architecture, one small step at a time. Each step: make a single focused improvement (extract a unit, clarify a boundary, remove duplication), run the full test suite, and commit only if green. After each step, ask: 'Am I satisfied with the architecture?' If no, continue. Stop when you genuinely are, and summarize the before/after structure. Never break a passing test.
```

### The Sub-50ms Page-Load Loop
*Optimize until every page loads in under 50 ms.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Measure the load time of every page. For the slowest one, find the biggest bottleneck (query, payload, render, blocking asset), fix it, and re-measure. Repeat, always attacking the current slowest page, until every page loads in under 50 ms (or you've hit a documented hard floor). Report the measured before/after for each page.
```

### The Production Error Sweep
*Read production logs, trace each error to root cause, and fix it.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Pull the recent production error logs. Group them by signature and order by frequency/impact. For the top one: reproduce it, trace it to its root cause (not the symptom), write a failing test, fix it, and confirm the test passes. Repeat down the list until the top errors are resolved. Report each root cause and fix.
```

### The 100% Test Coverage Loop
*Add tests until coverage reaches 100%.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Run the coverage report. Find the file with the lowest coverage, write meaningful tests (real behavior, edge + error cases — not assertion-free filler) for its uncovered lines, and re-run coverage. Repeat until coverage is 100% and the whole suite passes. Skip nothing silently — if a line is genuinely untestable, mark it with an explicit ignore + reason.
```

### The Logging Coverage Loop
*Add logging until every important path emits useful, tested logs.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Walk the important code paths (entry points, external calls, error branches, state changes). For each that lacks useful logging, add a structured log line (timestamp, operation, key ids, outcome) and a test asserting it fires. Repeat until every important path produces useful, tested logs. Avoid noise — log decisions and failures, not every line.
```

### The Nightly Changelog Loop
*Each night, review the previous day's changes and update the changelog.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Review all commits/merged PRs from the last 24 hours. Summarize the meaningful user-facing and developer-facing changes into clear changelog entries grouped by Added / Changed / Fixed / Removed. Prepend a dated section to CHANGELOG.md. Skip noise (formatting, typo-only). Run nightly.
```

### The Test-Suite Speed Loop
*Make the test suite run as fast as possible.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Profile the test suite and find the slowest tests/setup. Speed up the biggest offender (parallelize, share fixtures, mock slow I/O, remove redundant work) WITHOUT weakening coverage, then re-time the suite. Repeat, always attacking the current bottleneck, until the suite is as fast as it reasonably can be. Report total time before/after each step.
```

### The Repository Cleanup Loop
*Audit branches, PRs, commits, and worktrees, then tidy up.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Inspect local and remote branches, open PRs, stale worktrees, and dangling commits. For each: decide keep / merge / close / delete with a one-line reason, and act on the safe ones (delete merged branches, flag stale PRs). Never delete unmerged work without surfacing it first. Repeat until the repo is tidy; report what you removed and what needs a human decision.
```

### The Ticket-to-PR-Ready Loop
*Turn a ticket into a review-ready patch with the failure defined up front.*  
**Creator:** Hiten Shah · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Take this ticket and turn it into a review-ready PR. First, define the failure precisely: write a test that reproduces the bug/encodes the feature and currently fails. Then implement the minimal fix, make the test pass, run the full suite, and write a clear PR description (problem, fix, test, risk). Iterate until the PR would pass review with no obvious gaps.
```

### The Clodex Adversarial-Review Loop
*Run a Codex code review and fix every finding above a set threshold.*  
**Creator:** Lukas Kucinski · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Hand your current diff to a separate code-review agent (e.g. Codex) and ask it to find problems adversarially. Triage findings by severity. Fix every finding at or above your chosen threshold (e.g. medium+), re-run the review on the new diff, and repeat until no findings remain above threshold. Log deferred low-severity items with reasons.
```

### The Loop Harness Verification Loop
*Have a second agent session verify the staged work against the criteria.*  
**Creator:** Istasha · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
After staging your work, spin up a SECOND, independent agent session that did not write the code. Give it only the acceptance criteria and the staged diff. Its job: build, lint, run tests, and verify each criterion is actually met. If it finds gaps, return them to the implementer to fix, then re-verify. Only mark done when the independent session passes it.
```

### The Fresh-Clone Loop
*Clone into a clean, empty environment and follow the README to catch setup gaps.*  
**Creator:** 0xUmbra · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Clone this repo into a clean, empty environment with nothing preinstalled. Follow the README's setup steps EXACTLY as written, top to bottom. Every time a step fails or a hidden prerequisite surfaces, fix the README (or setup script) so the next person doesn't hit it. Repeat from a fresh clone until setup works end-to-end with zero manual guesswork.
```

### The LLM Codegen Workflow
*Brainstorm a spec one question at a time, generate a plan, then execute prompts in order.*  
**Creator:** Harper Reed (popularized by Simon Willison) · **Source:** https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/

```text
Phase 1 (spec): Ask me ONE question at a time to build a thorough, step-by-step spec for this idea; each question builds on my last answer. When complete, write spec.md.
Phase 2 (plan): From spec.md, produce prompt_plan.md — a sequence of small, safe implementation prompts — plus todo.md of granular steps.
Phase 3 (build): Execute the prompts from prompt_plan.md in order, running tests after each, checking off todo.md as you go.
```

### The Multi-File Refactor Loop
*Plan the change, apply transforms across call sites, run tests after each, until behavior is preserved.*  
**Creator:** community · **Source:** https://www.augmentcode.com/learn/automate-multi-file-code-refactoring-with-ai-agents-a-step-by-step-guide

```text
Plan a refactor that spans multiple files. First map every call site / dependency affected. Apply the change in small, behavior-preserving steps; after EACH step run the full test suite and commit only if green. If a step changes behavior, revert and rethink. Repeat until the refactor is complete, all references are updated, and the suite is green.
```

### The Code Migration Loop
*Environment-in-the-loop: plan, set up env, migrate, run tests, refine until the port passes.*  
**Creator:** research · **Source:** https://arxiv.org/pdf/2602.09944

```text
Migrate this code to the target language/framework with the environment in the loop. Steps: (1) plan the migration and set up a runnable target environment; (2) port a slice; (3) run the target's tests against it; (4) read failures and refine. Repeat slice by slice until the migrated code passes the same behavioral tests as the original. Keep a mapping of old->new for traceability.
```

### The Self-Correcting Agent Loop
*A state-machine loop with conditional edges: act -> check -> retry, bounded by iteration limits.*  
**Creator:** community · **Source:** https://www.matterai.so/guides/agentic-workflows-building-self-correcting-loops-with-langgraph-and-crewai-state-machines

```text
Run as a state machine: ACT (attempt the task) -> CHECK (validate the result against explicit success criteria) -> if it fails, RETRY with the failure reason fed back in. Cap retries at N (e.g. 3). On success, exit and return the result; on hitting the cap, stop and report the last failure plus what you tried. Never loop unbounded.
```

### The Mobile Closed-Loop Build
*Install on a virtual device, tap through every screen, fix crashes, repeat until store-ready.*  
**Creator:** Alexander Zanfir · **Source:** https://medium.com/@alexzanfir/closed-loop-development-how-ai-agents-build-software-while-you-sleep-6df42cd05a85

```text
Build and install the app on a virtual device. Programmatically tap through every screen and flow; verify layouts across screen sizes; watch for crashes, broken navigation, and slow frames. When you hit a defect, reproduce it, fix it, rebuild, and re-run the full walkthrough. Repeat until a complete walkthrough passes clean on all target device sizes.
```


## Testing & evaluation

### The Quality Streak Loop
*Test realistic scenarios; when one fails, document it and fix it.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Run realistic end-to-end scenarios against the product, one after another. The moment one fails: document it (steps, expected, actual), find the root cause, fix it, add a regression test, and only then continue the streak. Keep going until you can run a long streak of realistic scenarios with zero failures. Report the streak length and every issue found.
```

### The Full Product Evaluation Loop
*Generate N realistic scenarios, each with explicit success criteria.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Create N realistic user scenarios that exercise the product's real use cases, each with explicit, checkable success criteria. Run every scenario, score pass/fail against its criteria, and collect failures. Fix the failures (root cause, not symptom), then re-run the whole set. Repeat until all N pass. Keep the scenario set as a living eval suite.
```

### The Self-Improving Champion Loop
*Iterative optimization with a budget, scoring, and gate checks.*  
**Creator:** Jose C. Munoz · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Hold a 'champion' solution and its score. Within a fixed budget, repeatedly: generate a challenger variation, score it on the same rubric, and run gate checks (correctness, constraints). If the challenger beats the champion AND passes all gates, it becomes the new champion. Otherwise discard it. Stop when the budget is spent or improvements stall; return the champion.
```

### The Devil's-Advocate Loop
*Argue against your own design via a critic sub-agent until it survives.*  
**Creator:** Anonymous · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Take your current design/plan. Spawn a critic persona whose only job is to argue AGAINST it — find the strongest objections, failure modes, and cheaper alternatives. For each serious objection, either fix the design or write a clear rebuttal. Repeat the attack with fresh eyes until the design survives a round with no new serious objections. Summarize the objections raised and how each was resolved.
```

### TDAD — Test-Driven Agentic Development
*Use a code dependency graph for blast-radius before each change to cut regressions.*  
**Creator:** research · **Source:** https://arxiv.org/pdf/2603.17973

```text
Before changing any code, build/consult a dependency graph to identify exactly which modules and tests your change can affect (its blast radius). Write/identify the tests covering that radius. Make the change, then run that targeted set first and the full suite second. If a previously-passing test in the radius breaks, treat it as a regression and revert. Repeat per change.
```

### Eval-Driven Development (LLM-as-Judge)
*Write evals first, change, run evals, integrate; route flagged traces into a golden dataset.*  
**Creator:** Eugene Yan (& community) · **Source:** https://eugeneyan.com/writing/eval-process/

```text
Treat evals like tests. (1) Before building an AI feature, define success criteria as evals with a clear rubric and a golden dataset. (2) Make a change. (3) Run the evals (use an LLM-as-judge validated to ~75-90% agreement with human labels). (4) Integrate only if scores hold/improve. When production surfaces a bad case, add it to the golden dataset and re-test. Loop.
```

### Pre-Commit Guard
*A hook that runs tests before each commit and blocks commits while the suite is red.*  
**Creator:** elorm · **Source:** https://loops.elorm.xyz/

```text
Set up a pre-commit hook that runs the test suite (or the fast, relevant subset) before every commit. If anything fails, block the commit and surface the failures. Only allow the commit through when the suite is green. Keep the hook fast enough that it doesn't tempt anyone to bypass it.
```

### Post-Edit Test Guard
*A hook that runs the related tests after each file edit to catch regressions immediately.*  
**Creator:** elorm · **Source:** https://loops.elorm.xyz/

```text
After every file edit, automatically run the tests related to the changed file (map source->tests). If a related test now fails, stop and surface it immediately so the regression is caught at the moment it's introduced, not at commit time. Keep running until edits leave related tests green.
```

### Independent Verifier Pass
*A separate verifier runs build + lint + tests with no access to the implementer's rationale.*  
**Creator:** elorm · **Source:** https://loops.elorm.xyz/

```text
When the implementer claims the task is done, hand a SEPARATE verifier agent only the diff and the acceptance criteria — not the implementer's reasoning or chat. The verifier independently runs build, lint, and tests and checks each criterion. It returns PASS or a list of concrete failures. The work is done only when an independent verifier returns PASS.
```


## Prompt & model optimization

### OPRO (Optimization by PROmpting)
*Feed the LLM prompts paired with their scores; it generates better variants toward higher accuracy.*  
**Creator:** Google DeepMind (Yang et al.) · **Source:** https://billtcheng2013.medium.com/automated-prompt-engineering-part-2-c5745039cd81

```text
Optimize a prompt by treating the LLM as the optimizer. Maintain a history of (candidate prompt, score) pairs on a fixed eval set. Each step: show the LLM the top-scoring candidates with their scores and ask it to propose a NEW prompt likely to score higher. Evaluate the new prompt on the eval set, add it to the history, and repeat until scores plateau. Return the best prompt.
```

### TextGrad
*Textual gradient descent — an LLM proposes edits that reduce a textual loss across your pipeline.*  
**Creator:** Stanford (Yuksekgonul et al.) · **Source:** https://arxiv.org/pdf/2406.07496

```text
Improve this prompt/pipeline via textual gradients. (1) Run it and compute a textual 'loss' — an LLM critique of what went wrong vs the target. (2) Ask an LLM for the 'gradient': specific edits to the prompt that would reduce that loss. (3) Apply the edits, re-run, re-evaluate. Repeat for K steps or until the loss stops decreasing. Keep the best version.
```

### DSPy
*Program prompts as modules with signatures; a compiler optimizes them against a metric.*  
**Creator:** Stanford NLP (Khattab et al.) · **Source:** https://github.com/stanfordnlp/dspy

```text
Instead of hand-tuning prompts, declare your task as modules with input/output signatures and a metric. Provide a small training/dev set. Let the optimizer (compiler) search prompts/demonstrations that maximize the metric on the dev set, iterating automatically. Evaluate the compiled program on held-out data; keep it if it beats the baseline. (Use the DSPy framework.)
```

### PromptBreeder
*Evolutionary search that mutates and breeds prompts, selecting by fitness across generations.*  
**Creator:** Google DeepMind (Fernando et al.) · **Source:** https://futureagi.com/blog/top-10-prompt-optimization-tools-2025/

```text
Evolve prompts genetically. Start with a population of candidate prompts. Each generation: score every candidate on a fixed eval set (fitness), keep the top performers, then create the next generation by mutating and recombining them (also evolve the mutation instructions themselves). Repeat for G generations and return the highest-fitness prompt.
```


## Research & data science

### The AI Scientist
*Autonomous loop: generate research ideas, run experiments, analyze results, write the paper.*  
**Creator:** Sakana AI (Lu et al.) · **Source:** https://arxiv.org/pdf/2503.24047

```text
Run an autonomous research loop on this problem. (1) Generate a novel, testable hypothesis. (2) Design and implement an experiment for it. (3) Run it and record results. (4) Analyze: did it support the hypothesis? (5) Write up the finding. Feed what you learned into the next hypothesis. Repeat, keeping a research log, until you have a result worth reporting.
```

### Agentomics-ML
*Autonomous ML experimentation loop that produces a suitable model for a dataset.*  
**Creator:** research · **Source:** https://arxiv.org/pdf/2506.05542

```text
Given a dataset and a target metric, autonomously build a good model. Loop: inspect the data, propose a modeling approach (features, model, hyperparameters), train, evaluate on a held-out split, and record the metric. Keep changes that improve held-out performance, revert those that don't. Repeat until the metric plateaus; output the best model and a summary of what worked.
```

### Deep Research Loop
*Planner -> search sub-agents -> synthesize -> 'need more?' -> loop until coverage is sufficient, then cite.*  
**Creator:** LangChain (Open Deep Research) · **Source:** https://www.langchain.com/blog/open-deep-research

```text
Research this question thoroughly. (1) Plan: break it into sub-questions. (2) For each, search, fetch sources, and extract findings with citations. (3) Synthesize what you have and identify gaps or contradictions. (4) If coverage is insufficient, generate sharper follow-up queries and loop. Stop when the plan is well covered, then write a cited, structured report. Verify load-bearing claims against primary sources.
```

### The MLOps Retraining Loop
*Monitor for drift, retrain past threshold, compare, ship only if better, keep monitoring.*  
**Creator:** community · **Source:** https://www.auxiliobits.com/blog/mlops-for-agentic-ai-continuous-learning-and-model-drift-detection/

```text
Continuously monitor the deployed model for data/prediction drift. When drift exceeds the threshold for the agreed window, trigger retraining on fresh labeled data. Evaluate the new model against the current one on a holdout; promote it only if it's meaningfully better and passes gates. Then resume monitoring. Log every drift event, retrain, and promotion decision.
```


## Security & red-teaming

### The AI Red-Teaming Loop
*Adversarially attack the system, feed results back, re-test on a schedule.*  
**Creator:** community · **Source:** https://github.com/requie/AI-Red-Teaming-Guide

```text
Adversarially attack this AI system. Run a battery of attacks: prompt injection (direct + indirect), jailbreaks, data/secret exfiltration, tool misuse, and cross-user access. For each successful attack, document the exploit and the fix (input handling, isolation, guardrail). Apply fixes, then re-run the full battery. Repeat until the battery passes, and schedule it to re-run as new attack techniques appear.
```

### RvB — Iterative Red-Blue Games
*Automate hardening through repeated red-team-attacks / blue-team-defends rounds.*  
**Creator:** research · **Source:** https://arxiv.org/pdf/2601.19726

```text
Harden the system through rounds. RED: find and exploit a weakness; document the attack. BLUE: patch that weakness and add a detection/test for it. Re-run RED against the patched system. Repeat round after round; each round RED must find something new or the system is considered hardened for the current threat model. Keep a log of every attack and defense.
```


## Writing & content

### Self-Refine
*One LLM drafts, critiques its own draft, then revises, looping until a stopping criterion.*  
**Creator:** Madaan et al. · **Source:** https://learnprompting.org/docs/advanced/self_criticism/self_refine

```text
Produce a first draft. Then, against an explicit rubric, write specific, actionable critique of YOUR OWN draft (what's weak, unclear, missing). Revise the draft using that critique. Keep a memory of past feedback so you don't repeat mistakes. Repeat draft->critique->revise until the critique finds nothing material to fix or you hit a set number of rounds.
```

### Draft -> Critique -> Finalize
*Force deliberation: generate an idea, critique it against criteria, regenerate from the critique.*  
**Creator:** community · **Source:** https://learnwithparam.com/blog/prompt-engineering-self-critique-refinement

```text
Step 1 DRAFT: generate your first answer. Step 2 CRITIQUE: evaluate that draft against the stated criteria, listing concrete weaknesses. Step 3 FINALIZE: write a NEW version that addresses every critique point. Don't just lightly edit — regenerate from the critique. Output only the finalized version plus a one-line note on what improved.
```

### LLM Peer Review
*Multiple agents review each other's drafts, then privately revise — distributed critique.*  
**Creator:** research · **Source:** https://arxiv.org/pdf/2601.08003

```text
Create K independent drafts (different personas/angles). Have each draft reviewed by the OTHER agents, who give blind, constructive feedback against a rubric — no agent sees others' revisions. Each author then privately revises using the feedback received. Select or merge the strongest revised draft. Report the feedback themes that drove the improvements.
```

### Chain of Density
*Iteratively rewrite a summary, fusing in missing entities each pass without growing length.*  
**Creator:** Adams et al. · **Source:** https://arxiv.org/pdf/2309.04269

```text
Summarize the text in a fixed length. Then repeat N times: identify 1-3 salient entities/details MISSING from your current summary and rewrite a new summary of the SAME length that includes them — making room via fusion, abstraction, and compression, never by dropping prior content or adding length. Output the final, densest summary.
```

### The SEO/GEO Visibility Loop
*Audit crawlability, indexation, and structured data, and fix gaps.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Audit the site for search + generative-engine visibility: crawlability, indexation, metadata, structured data, internal links, and content gaps. List issues by impact. Fix the highest-impact issue, re-audit, and repeat. Continue until a full audit surfaces no high-impact issues, then report the before/after on each checked dimension.
```

### The Product Update Podcast Loop
*Generate a short 3-5 minute podcast episode about new features.*  
**Creator:** Pierson Marks · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Review the latest shipped features (from the changelog/PRs). Write a tight 3-5 minute podcast script that explains what's new, why it matters, and how to use it, in a natural spoken voice. Generate the audio. Run this on each release so every update gets its own short episode.
```


## Design

### War Loops: Autonomous Frontend Designer
*Point it at a URL or image and produce iterative design builds.*  
**Creator:** Swayam · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Given a target URL or reference image, capture it, derive a design spec (layout, type, color, spacing), then build the UI to match. Render your build, screenshot it, and compare it against the target. For each visual gap, make a surgical fix and re-render. Repeat until the build matches the reference to a high fidelity. Report the remaining intentional differences.
```

### The Boeing 747 Benchmark
*Build the most realistic Boeing 747 you can in Three.js — a model-capability benchmark.*  
**Creator:** @victormustar · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Build the most realistic Boeing 747 you can in Three.js. Render it, screenshot from multiple angles, and critique the result against real reference photos (proportions, livery, lighting, detail). Fix the biggest realism gap, re-render, and compare again. Repeat until it's as photorealistic as you can get. (A fun benchmark for a model's spatial + graphics ability.)
```

### The Infinite Clickbait Loop
*Generate ten thumbnail concepts and score each against a rubric.*  
**Creator:** @Alex_FF · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Generate 10 distinct thumbnail concepts for the topic. Score each against a rubric (clarity at small size, curiosity, contrast, focal point, emotional hook). Keep the top scorers, then generate 10 new variations that push on what made them work. Repeat until a concept clearly tops the rubric. Output the winner plus the runner-ups and their scores.
```

### The Three.js Game Loop
*Build a playable loop first, then iterate until it passes gameplay, visual, perf & release checks.*  
**Creator:** majidmanzarpour · **Source:** https://github.com/majidmanzarpour/threejs-game-skills

```text
Build the smallest PLAYABLE core loop first (move, interact, win/lose). Then iterate: playtest it, pick the weakest aspect (fun, feel, visuals, performance), improve it, and playtest again. After each pass, run the checklist: plays on desktop + mobile, no visual glitches, stable frame rate, clear UI. Repeat until every check passes.
```

### VideoAgent
*Agentic video editing with reflection rounds + adaptive feedback loops that refine the plan.*  
**Creator:** HKUDS · **Source:** https://github.com/HKUDS/VideoAgent

```text
Plan the video edit (shots, cuts, captions, pacing). Produce a draft, then REFLECT: watch it back and evaluate against the goal (clarity, pacing, hook). Use that self-evaluation to refine the plan and re-render the affected parts. Repeat the reflect->refine loop until the cut meets the goal. (Or use the VideoAgent framework.)
```


## Accessibility

### The a11y Audit Loop
*Scan for WCAG violations, apply remediation hints, re-scan until compliant.*  
**Creator:** snapsynapse · **Source:** https://github.com/snapsynapse/skill-a11y-audit

```text
Audit the site against WCAG 2.x AA. For each violation, apply the remediation (labels, contrast, focus order, alt text, ARIA) and re-scan. Repeat until automated scans are clean. NOTE: automated tools catch only ~30-40% of issues — finish with keyboard-only navigation, a real screen-reader pass, and flag anything needing human/user testing.
```

### Accessibility Review Agents
*Specialist agents that enforce WCAG 2.2 AA so coding agents stop generating inaccessible code.*  
**Creator:** Community-Access · **Source:** https://github.com/Community-Access/accessibility-agents

```text
Before accepting any generated UI, run it past accessibility specialist checks for WCAG 2.2 AA: semantic structure, keyboard operability, focus management, color contrast, names/roles/values, and motion safety. Block code that fails; return specific fixes. Re-check after fixes. Make this a standing gate so inaccessible UI never lands.
```


## Data & analytics

### The Text-to-SQL Self-Correction Loop
*Generate SQL, execute, critique, regenerate until executable and semantically correct.*  
**Creator:** Rudder Analytics · **Source:** https://medium.com/@rudderanalytics/ai-agent-for-sql-queries-and-visualization-using-multi-agent-framework-7f9f3d639108

```text
Turn the question into SQL. Then: EXECUTE it against the database (read-only). If it errors, read the error and rewrite. If it runs, CRITIQUE the result — does it actually answer the question, with the right grain, filters, and joins? If not, revise and re-run. Repeat until the query is both executable and semantically correct, then return the SQL + a one-line explanation.
```

### The Active-Learning Labeling Loop
*Auto-label high-confidence items, route low-confidence to humans, retrain, until a stop rule.*  
**Creator:** community · **Source:** https://dev.co/ai/ai-assisted-data-labeling-using-active-learning-loops

```text
Label a dataset efficiently. (1) Auto-label items where model confidence exceeds the quality threshold. (2) Route the lowest-confidence items to a human. (3) Retrain on the new labels and update uncertainty estimates. (4) Repeat. Stop when one of: the model hits the production KPI, marginal accuracy gain per round falls below threshold, or the labeling budget is exhausted.
```


## Marketing & growth

### Loop Marketing / Growth Loop
*Run small fast A/B tests on hooks/offers/audiences; roll each learning back in, compounding.*  
**Creator:** HubSpot · **Source:** https://www.hubspot.com/loop-marketing

```text
Run growth as a compounding loop. Each cycle: pick one lever (hook, offer, audience, or channel), ship a small fast A/B test with a clear metric, measure, and roll the winning learning back into your creative, targeting, and spend. Kill losers quickly. Keep cycles small and frequent so each one sharpens the next. Track the metric trend across cycles.
```


## Support & sales

### The Support Resolution Loop (ATTD)
*Analyze -> Train -> Test -> Deploy: resolve tickets and improve from human-corrected escalations.*  
**Creator:** Fin AI (Intercom) · **Source:** https://fin.ai/learn/ai-agents-resolve-tickets-faster

```text
Improve support resolution in a loop. ANALYZE recent tickets to find common, automatable intents and where the agent fails. TRAIN/update the agent's answers and actions for those. TEST against held-out tickets and edge cases. DEPLOY, routing low-confidence/high-risk/emotional cases to humans. Feed human corrections back into the next ANALYZE. Repeat.
```


## Operations

### The Stale-Safe Batch Release Loop
*Exclude stale/unfinished work, combine valid changes, and release.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Prepare a batch release. Inventory all candidate changes; for each, decide if it's complete and safe or stale/unfinished. Exclude anything stale or risky (with a reason). Combine the valid changes, run the full test + smoke suite, and only cut the release if green. Repeat the inclusion check until the batch is clean. Report what was included and what was held back.
```

### The Production Data Cleanup Loop
*Remove anything that doesn't meet the allowed definition.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Define precisely what 'valid' data looks like. Scan production data against that definition; for each record that doesn't meet it, decide fix vs remove. Act on a SMALL reversible batch first (with a backup), verify nothing legitimate was lost, then continue. Repeat until all data meets the definition. Never bulk-delete without a backup and a verified sample.
```

### The Post-Release Baseline Loop
*Run the standard benchmarks and record the results after each release.*  
**Creator:** Matthew Berman · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
After each release, run the standard benchmark suite (latency, throughput, error rate, key business metrics) and record the results as the new baseline, tagged to the release. Compare against the previous baseline; flag any regression beyond the agreed tolerance and open an issue. Keep the history so trends are visible across releases.
```

### The Customer AI Deployment Loop
*Manage one customer AI deployment from priority to production.*  
**Creator:** AgentLed.ai · **Source:** https://signals.forwardfuture.ai/loop-library/

```text
Drive one customer AI deployment from intake to production. Loop through: clarify the priority use case + success criteria, configure/integrate, test against the customer's real scenarios, fix gaps, and get sign-off. Don't advance a stage until its criteria are met. Track blockers explicitly and surface them. Stop when it's live and meeting the agreed success criteria.
```


## DevOps & infrastructure

### The Terraform Fix Loop
*validate -> plan -> apply -> verify, reading the error and fixing until the infra is correct.*  
**Creator:** community · **Source:** https://computingforgeeks.com/ai-coding-agents-devops-terraform-ansible-kubernetes/

```text
Iterate on infrastructure code: run `terraform validate`, then `plan`, read any error or unexpected diff, fix the code, and repeat until the plan is clean and matches intent. Then `apply` and verify the real resources (via CLI/API) are healthy. IMPORTANT: keep scope tight — only change what the task needs; do not refactor adjacent infra. Revert if apply misbehaves.
```

### Ship PR Until Green
*Implement on a branch, push, open a PR, wait for CI, loop until checks pass and it's merge-ready.*  
**Creator:** elorm · **Source:** https://loops.elorm.xyz/

```text
Implement the change on a feature branch. Run tests locally, push, and open a PR. Wait for CI; when checks go red, read the logs, push a fix, and wait again. Repeat until every check is green and the PR is genuinely merge-ready (description, tests, no unresolved review comments). Then report it's ready to merge.
```

### CI Failure Watcher
*Poll CI on an interval; when checks go red, investigate and push fixes until green.*  
**Creator:** elorm · **Source:** https://loops.elorm.xyz/

```text
Poll CI on a fixed interval. When a run goes red, fetch the logs, identify the failing job and root cause, push a targeted fix, and keep watching. Repeat until the pipeline is green again. Summarize each failure and the fix. Don't sit idle — re-check on the interval until resolved.
```

### Deploy Verification Loop
*After a deploy, hit health + smoke endpoints on an interval until everything returns healthy.*  
**Creator:** elorm · **Source:** https://loops.elorm.xyz/

```text
After a deploy, poll the health and smoke-test endpoints on an interval. Treat the deploy as unverified until all checks return healthy responses within the timeout. If checks fail past the threshold, surface it (and trigger rollback if configured). Only mark the deploy verified once a full pass is healthy. Log each check.
```


## Autonomous coding agents

### Aider
*Pair-programming loop with architect -> editor mode; edits via diffs against a repo map.*  
**Creator:** Paul Gauthier · **Source:** https://github.com/Aider-AI/aider

```text
Use Aider's loop: it builds a tree-sitter repo map for context, proposes edits as diffs, applies them, and can run tests/lint and auto-fix. For complex work use architect mode (one model plans the change, another writes the edits). Iterate edit->test until the task passes. (This is the Aider CLI; `pip install aider-install`.)
```

### SWE-agent
*Agent-computer-interface loop that reads an issue, edits the repo, runs tests, iterates to a patch.*  
**Creator:** Princeton NLP · **Source:** https://github.com/princeton-nlp/SWE-agent

```text
Use SWE-agent's loop on a GitHub issue: it reads the issue, navigates the repo through a constrained agent-computer interface, edits files, runs the tests, observes failures, and iterates until it produces a passing patch. Best for turning an issue into a PR-ready diff. (See the SWE-agent repo for setup.)
```

### OpenHands (ex-OpenDevin)
*Multi-agent delegation loop: plan -> act -> observe across a dev environment.*  
**Creator:** All-Hands-AI · **Source:** https://github.com/All-Hands-AI/OpenHands

```text
Use OpenHands to run a full plan->act->observe loop in a sandboxed dev environment: it writes code, runs commands, browses, and delegates subtasks between agents, observing results and iterating toward the goal. Good for end-to-end tasks that span editing, running, and testing. (See the OpenHands repo for setup.)
```

### AutoGPT
*The original autonomous goal loop: decompose a goal into tasks and execute until met.*  
**Creator:** Significant-Gravitas · **Source:** https://github.com/Significant-Gravitas/AutoGPT

```text
Give AutoGPT a high-level goal. It will decompose the goal into tasks, execute them using its tools, observe the results, and create follow-up tasks — looping autonomously toward the objective. Add a max-iteration cap and clear success criteria so it terminates. (See the AutoGPT repo for setup.)
```

### BabyAGI
*Task-creation/prioritization/execution loop backed by a vector store of prior results.*  
**Creator:** Yohei Nakajima · **Source:** https://github.com/yoheinakajima/babyagi

```text
Run BabyAGI's loop on an objective: it pulls the top task, executes it, stores the result in a vector store, then creates and reprioritizes new tasks based on the objective and what it has learned — repeating until the objective is met or you cap iterations. (See the BabyAGI repo for setup.)
```


## Tools & harnesses

### loop-engineering
*Patterns, starters & CLI tools (loop-audit, loop-init, loop-cost) for loop engineering.*  
**Creator:** Cobus Greyling · **Source:** https://github.com/cobusgreyling/loop-engineering

```text
Use the loop-engineering toolkit to scaffold and run agent loops: `loop-init` to start a loop project, `loop-audit` to check loop design/quality, and `loop-cost` to track spend. A practical starter for building your own recursive agent loops. (See the repo.)
```

### autoloop
*Agent-agnostic iterative-optimization loops for Claude Code, Codex, Cursor, Gemini CLI.*  
**Creator:** Arm Gabrielyan · **Source:** https://github.com/armgabrielyan/autoloop

```text
Use autoloop to run iterative-optimization loops with any agent (Claude Code, Codex, Cursor, OpenCode, Gemini CLI). Point it at a task with a measurable goal; it drives the propose->try->measure->keep/revert loop for you. Inspired by Karpathy's autoresearch. (See the repo.)
```

### agentic-loop
*Autonomous Claude Code toolkit based on RALPH + PRD-driven development.*  
**Creator:** allierays · **Source:** https://github.com/allierays/agentic-loop

```text
Use agentic-loop with Claude Code: write a PRD, and the toolkit runs RALPH-style — executing each story through code->test->commit automatically until the PRD is complete. Good for mostly-autonomous builds. (See the repo.)
```

### agent-loop
*A guide + workflows for orchestrating specialized AI personas to build, test, and deploy in a loop.*  
**Creator:** Saik0s · **Source:** https://github.com/Saik0s/agent-loop

```text
Use agent-loop's guide to orchestrate specialized AI personas (e.g. planner, builder, tester, reviewer) where a human directs the personas through a build->test->deploy loop collaboratively. A blueprint for structuring multi-persona agentic engineering. (See the repo.)
```

### ralph
*An autonomous loop that runs until every item in a PRD is complete.*  
**Creator:** snarktank · **Source:** https://github.com/snarktank/ralph

```text
Use the ralph harness: give it a PRD and it runs an autonomous loop, completing each requirement item by item (implement->test->commit) until the whole PRD is done. (See the repo for setup.)
```

### ralph-claude-code
*A Ralph loop for Claude Code with intelligent exit detection.*  
**Creator:** Frank Bria · **Source:** https://github.com/frankbria/ralph-claude-code

```text
Use ralph-claude-code to run the Ralph loop with Claude Code, with smart exit detection so it stops when the work is genuinely done rather than looping forever. (See the repo for setup.)
```

### codex-autoresearch-harness
*Bash harness to run Karpathy's autoresearch with Codex CLI + an A/B framework.*  
**Creator:** SarahXC · **Source:** https://github.com/SarahXC/codex-autoresearch-harness

```text
Use this bash harness to run Karpathy's autoresearch loop with the Codex CLI, including an A/B framework to compare models/approaches across runs. (See the repo for setup.)
```

### autoresearch-guide
*3,000+ line guide teaching agents to autonomously optimize anything measurable.*  
**Creator:** Rkcr7 · **Source:** https://github.com/Rkcr7/autoresearch-guide

```text
Read the autoresearch-guide and apply its pattern: give an agent a file, a metric, and the guide, then let it autonomously optimize the metric overnight (propose->experiment->measure->keep/revert). A deep how-to for the autoresearch loop. (See the repo.)
```

### awesome-autoresearch
*A curated list of autoresearch resources.*  
**Creator:** yibie · **Source:** https://github.com/yibie/awesome-autoresearch

```text
Browse awesome-autoresearch for a curated set of autoresearch implementations, harnesses, and write-ups to learn or extend the autoresearch loop. (See the repo.)
```


## Patterns & theory

### ReAct
*Interleave Thought -> Action -> Observation so reasoning guides tool use and vice versa.*  
**Creator:** Yao et al. · **Source:** https://www.mindstudio.ai/blog/what-is-react-loop-ai-agent-reasoning

```text
Solve the task by interleaving reasoning and acting. Each step output: Thought (what you're reasoning and why), Action (the tool call to make), then read the Observation (the result). Use the observation to update your next Thought. Loop Thought->Action->Observation until you can give a final answer; then output Answer.
```

### Reflexion
*Actor + Evaluator + Self-Reflection; verbal self-feedback stored in memory across trials.*  
**Creator:** Shinn et al. · **Source:** https://proceedings.neurips.cc/paper_files/paper/2023/file/1b44b878bb782e6954cd888628510e90-Paper-Conference.pdf

```text
Attempt the task (Actor). Evaluate the outcome against the goal (Evaluator) — pass or fail with a reason. If it failed, write a short verbal SELF-REFLECTION on WHY it failed and what to do differently, and store it in memory. Retry the task, with all prior reflections in context. Repeat until you pass or hit the trial limit.
```

### Evaluator-Optimizer
*Generator proposes, evaluator scores, loop until a quality threshold — the generic critic loop.*  
**Creator:** Anthropic, Building Effective Agents · **Source:** https://www.anthropic.com/research/building-effective-agents

```text
Use two roles. GENERATOR produces a candidate answer. EVALUATOR scores it against explicit criteria and returns specific feedback. Feed the feedback back to the GENERATOR to produce an improved candidate. Loop until the EVALUATOR's score clears the threshold or improvement stalls. Keep generator and evaluator as distinct roles.
```

### Self-Consistency / Tree of Thoughts
*Sample many reasoning paths / search a tree of thoughts, then select the best.*  
**Creator:** Wang et al. / Yao et al. · **Source:** https://arxiv.org/pdf/2405.10467

```text
For a hard reasoning problem: (Self-Consistency) sample multiple independent reasoning paths and take the majority/most-consistent answer. Or (Tree of Thoughts) branch into several candidate intermediate 'thoughts', evaluate each branch's promise, expand the best, and prune dead ends — searching the tree until you reach a well-supported answer.
```

### Agent Design Pattern Catalogue
*A catalogue of architectural patterns for foundation-model agents.*  
**Creator:** Liu et al. · **Source:** https://arxiv.org/pdf/2405.10467

```text
Reference: a catalogue of architectural patterns for foundation-model agents (passive/active goal creation, reflection, tool use, voting, etc.). Use it to pick the right loop/pattern for your agent rather than reinventing one. (See the paper.)
```

### Anthropic's Agent Workflow Patterns
*The five canonical patterns: prompt chaining, routing, parallelization, orchestrator-worker, evaluator-optimizer.*  
**Creator:** Anthropic · **Source:** https://www.anthropic.com/research/building-effective-agents

```text
Reference for composing agent loops. Pick the simplest pattern that fits: PROMPT CHAINING (sequential steps), ROUTING (classify then dispatch), PARALLELIZATION (run subtasks concurrently then aggregate), ORCHESTRATOR-WORKER (a lead delegates dynamic subtasks), or EVALUATOR-OPTIMIZER (generate + critique loop). Prefer workflows (control flow in code) over fully autonomous agents unless you need the flexibility.
```


---

Credits to every original creator listed above. Curation + prompt wording: MIT. 
Contribute or correct attribution: https://github.com/keysersoose/loop-library/issues
