# Loop Library — All Prompts

> A curated, credited collection of AI-agent loops — repeatable workflows for coding agents (Claude Code, Cursor, Codex, Gemini CLI) that iterate until a stopping condition is met. Each loop ships with a ready-to-paste prompt.

**148 loops** · repo: https://github.com/keysersoose/loop-library · site: https://keysersoose.github.io/loop-library/

_Prompts are original implementations of each loop's technique, written for this library so they are copy-paste ready and license-clean. Credit each creator if you share._

---


## Categories

- [Foundational](#foundational) (3)
- [Engineering](#engineering) (25)
- [Testing & evaluation](#testing--evaluation) (18)
- [Prompt & model optimization](#prompt--model-optimization) (4)
- [Research & data science](#research--data-science) (5)
- [Security & red-teaming](#security--red-teaming) (2)
- [Writing & content](#writing--content) (6)
- [Design](#design) (6)
- [Accessibility](#accessibility) (2)
- [Data & analytics](#data--analytics) (2)
- [Marketing & growth](#marketing--growth) (1)
- [Support & sales](#support--sales) (1)
- [Operations](#operations) (6)
- [DevOps & infrastructure](#devops--infrastructure) (6)
- [Autonomous coding agents](#autonomous-coding-agents) (5)
- [Tools & harnesses](#tools--harnesses) (9)
- [Patterns & theory](#patterns--theory) (12)
- [Loop frameworks (GitHub)](#loop-frameworks-github) (30)
- [International (translated)](#international-translated) (5)


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

### Timebox / Ultimatum Loop
*Give an assistant's suggestion a hard time budget; if it does not yield value with minimal extra effort, abandon and code manually.*  
**Creator:** Birgitta Bockeler (Thoughtworks) · **Source:** https://martinfowler.com/articles/exploring-gen-ai/08-how-to-tackle-unreliability.html

```text
Timebox the assistant. Give its suggestion a hard time/effort budget. If it does not produce real value within that budget with only minimal extra effort from you, abandon it and write the code manually. Do not sink more time into coaxing a bad suggestion -- the stop condition is the first clear sign of non-value.
```

### Guardrails Correction Loop
*Generate -> validate via guardrails; if a check fails, filter or regenerate; stop when output passes all validators or a max-retry cap.*  
**Creator:** Eugene Yan · **Source:** https://eugeneyan.com/writing/llm-patterns/

```text
Wrap generation in validators. Generate the output, then run it through your guardrails (schema, safety, format, factuality checks). If any check fails, either filter the bad part or regenerate with the failure noted. Loop until the output passes all validators or you hit a max-retry cap, then return the best passing result.
```

### Explore-Fix + Blind Audit Loop
*Loop explore->fix until two consecutive 'all clear' passes, then a FRESH-context blind audit; if it finds issues, re-enter the loop; stop only when the blind audit is also clear.*  
**Creator:** dern_throw_away (r/ClaudeAI) · **Source:** https://www.reddit.com/r/ClaudeCode/comments/1to6hen/

```text
Harden this codebase in two phases. PHASE 1 (Explore-Fix): hunt bugs, security issues, and logic errors; fix every finding; record a 'pass' when you find nothing. Repeat until you get TWO consecutive passes. PHASE 2 (Blind Audit): in a FRESH context with no memory of Phase 1, audit the same code independently. If it finds anything, return to Phase 1. Stop only when the blind audit also returns zero findings. Report total rounds and all fixes.
```

### Reverse-PRD + MCP Blast-Radius Loop
*Parse the repo into framework-aware graphs, generate reverse-PRDs, expose via MCP (who_calls/impact_of/diff_spec_vs_code); query blast radius before every change; stop when spec-vs-code drift is zero.*  
**Creator:** KeyUnderstanding9124 (r/ClaudeCode) · **Source:** https://www.reddit.com/r/ClaudeCode/comments/1ngxlqg/

```text
Before ANY change, query the codebase graph via MCP: call who_calls(<symbol>) and impact_of(<change>) to get the full blast radius with citations. Then propose the change. After implementing, call diff_spec_vs_code(<feature_id>) to confirm the code matches its reverse-PRD spec. If drift is detected, fix and re-check. Only open a PR when diff_spec_vs_code returns zero drift. Never change code without first querying the graph.
```

### Tool-Observable Output Loop
*Give the agent a tool to observe its OWN output (start a server, hit an endpoint, read a log, run a headless check); write code -> observe -> fix; stop when the observation confirms correctness.*  
**Creator:** Boris Cherny (Claude Code creator) · **Source:** https://www.reddit.com/r/ClaudeAI/comments/1q2c0ne/

```text
You have a `run_and_observe` tool that starts the process and returns its real output (HTTP response, logs, test result). Implement <feature>. After each change, call the tool and read the ACTUAL behavior. If it doesn't match the expected behavior below, diagnose the discrepancy, fix the code, and observe again. Stop only when the observation confirms the expected behavior. Expected: <description>. Don't claim done from reading the code -- prove it by observing.
```

### Spec-First Lock
*Before any execution, the agent writes an IMMUTABLE spec (what it does, what it won't do, what done looks like); execution is blocked until committed and no mid-run revisions allowed; stop on spec violation.*  
**Creator:** dannwaneri (freeCodeCamp) · **Source:** https://www.freecodecamp.org/news/how-to-build-a-production-safe-agent-loop-from-exit-conditions-to-audit-trails/

```text
Before writing any code or taking any action, produce a FROZEN spec with three fields: (1) what this task does, (2) what it explicitly will NOT do, (3) the exact observable condition that means 'done'. Record it as an immutable artifact for this session. Do not proceed until it's committed. If a later step would require changing the spec, STOP and surface it as a new task -- never silently revise the spec.
```

### Production Circuit Breaker
*A dual-ceiling pre-flight guard (max turns AND max cumulative tokens) checked before every LLM call; trips immediately when either is hit, halts the loop, and logs the breach reason; stop on turn_limit OR token_limit.*  
**Creator:** dannwaneri (freeCodeCamp) · **Source:** https://www.freecodecamp.org/news/how-to-build-a-production-safe-agent-loop-from-exit-conditions-to-audit-trails/

```text
You operate inside a strict circuit breaker. Before EACH step, check: have you exceeded N turns or T total tokens? If either ceiling is hit, STOP immediately -- do not attempt the step, do not retry or self-heal past it. Report turns used, tokens used, which ceiling tripped, and the last completed action, then log the breach as your final output so a human can decide whether to reopen the budget and resume.
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

### Plan-Execute-Validate (PEV)
*Planner -> executor -> LLM-scorer loop; route to retry, replan, or complete based on a quality score; stop on pass or budget.*  
**Creator:** Manjunath G · **Source:** https://dev.to/manjunathgovindaraju/building-a-reliable-langgraph-workflow-plan-execute-validate-pev-automated-retries-and-mcp-1pik

```text
Run a Plan-Execute-Validate loop. PLAN the steps. EXECUTE the current step. VALIDATE the result with an LLM scorer against criteria. Based on the score, route to: RETRY (same step), REPLAN (rethink the approach), or COMPLETE. Stop when the final step passes the quality bar (e.g. score >= 0.80) or retries/replans are exhausted.
```

### The Iteration Flywheel
*Three-activity cycle -- evaluate quality -> debug issues -> change behaviour; tightening the eval step speeds every other step.*  
**Creator:** Hamel Husain · **Source:** https://hamel.dev/blog/posts/evals/

```text
Spin the eval flywheel: (1) EVALUATE output quality on real examples, (2) DEBUG the issues you find, (3) CHANGE the system to fix them -- then repeat. The leverage point is making the EVALUATE step fast and cheap, because it accelerates every other turn. Keep going until quality is consistently acceptable on your eval set.
```

### Model-Human Alignment Loop
*Iterate the LLM-judge critique prompt until model grades agree with human grades on 25-50 examples.*  
**Creator:** Hamel Husain · **Source:** https://hamel.dev/blog/posts/evals/

```text
Calibrate your LLM-as-judge. Grade 25-50 examples with both the model and a human; compare. Iterate the judge's critique prompt to close the gaps. Repeat until model/human agreement stabilizes at an acceptable correlation. Only then trust the judge to scale. Re-check periodically as data drifts.
```

### TDD Red-Green-Refactor (AI-assisted)
*Red-Green-Refactor wheel for AI coding; each phase gates on a hard condition; fall back to manual if regeneration fails twice.*  
**Creator:** Paul Sobocinski (Thoughtworks) · **Source:** https://martinfowler.com/articles/exploring-gen-ai/06-tdd-with-coding-assistance.html

```text
Drive AI-assisted coding with TDD. RED: only advance once you have a correctly failing test. GREEN: have the assistant write minimal code to pass it -- if regeneration fails twice, fall back to coding it by hand. REFACTOR: clean up while green. Loop per behavior. The hard gates keep the assistant honest.
```

### autonomy-loop (trust-nothing)
*A coding loop that refuses to trust 'the tests pass' — it proves it by mutating/breaking the test; if the test still passes, the test is worthless and gets fixed.*  
**Creator:** @inferencegod · **Source:** https://x.com/i/status/2068008938440663411

```text
Don't trust 'the tests pass.' After they're green, prove the tests are real: mutate the code under test (break it on purpose) and confirm a test now FAILS. If everything still passes after you broke the behavior, the test is worthless — strengthen it. Only trust a green suite that you've shown can go red. Loop this mutation check on the critical paths.
```

### Artifact-Gated Review Cap
*Multi-model review loop capped at N rounds where each review must produce a concrete diff, a new failing test, or an explicit LGTM -- prose-only counts as LGTM; stops at first LGTM or round N.*  
**Creator:** r/ClaudeAI (Perfect_Tangerine432, Dependent_Policy1307) · **Source:** https://www.reddit.com/r/ClaudeCode/comments/1to6hen/

```text
You are the reviewer in a capped review loop (round {round} of {max}). Review the diff and output EXACTLY ONE of: (a) a concrete unified diff fixing the most important issue, (b) a new failing test that proves a real bug, or (c) the single word LGTM. No prose, no style nits, no lists. If this is round {max}, output LGTM unless there's a security/correctness blocker. The implementer fixes your output and calls you again. Stop at the first LGTM or round {max} -- this prevents an LLM reviewer from inventing findings forever.
```

### ABCD Adversarial Criteria Loop
*Four agents: A defines criteria, B implements, C reviews in a sub-loop until clear, then D (non-implementing) independently verifies against A's ORIGINAL criteria; stops when D approves + A signs off.*  
**Creator:** cc_apt107 (r/ClaudeAI) · **Source:** https://www.reddit.com/r/ClaudeCode/comments/1to6hen/

```text
Run a four-agent quality pipeline. A: define explicit acceptance criteria. B: implement against them. C: review B's work in a loop until no findings remain. D (adversarial, did NOT implement): independently verify the output against A's ORIGINAL criteria, ignoring C's verdict -- list any criterion not provably met; output APPROVED or FAIL+reason, no fixes. Final gate: D APPROVED and A signs off. The separation (D never saw the implementation reasoning) is the point.
```

### Clavix Verify-or-Redo Gate
*PRD -> plan -> implement -> verify -> archive, where verify enforces 'no completion without evidence' — a failed check triggers fix + re-verify, repeating until verify passes (Iron Law: issues found = issues fixed + re-verified).*  
**Creator:** Bob5k · **Source:** https://clavix.dev

```text
Run the pipeline for this feature. (1) Elicit requirements -> PRD. (2) Break the PRD into ordered tasks. (3) Implement each task. (4) VERIFY every task against its success criteria with evidence -- if any criterion fails, fix it and re-verify before marking done; never advance on an unverified task (Iron Law: issues found = issues fixed + re-verified). (5) Archive outputs. Stop only when the verify phase exits clean.
```

### PostToolUse Meta-Analyzer
*After every Write/Edit, a sub-agent semantically reviews the change against project conventions/anti-patterns and injects findings before the next turn; stops when it returns CLEAN with no outstanding violations.*  
**Creator:** JokeGold5455 (r/ClaudeAI) · **Source:** https://www.reddit.com/r/ClaudeAI/comments/1oivjvm/

```text
Wire a PostToolUse hook that fires after every Write/Edit. It spawns a lightweight reviewer sub-agent: 'You are a semantic code reviewer. Here is the file just modified: [DIFF]. Check it against the conventions/anti-patterns in CLAUDE.md. List any violations, inconsistencies, or regressions; if none, respond CLEAN.' Inject the report as a system reminder into the next turn. The main agent must resolve every flagged issue before starting new work. The loop settles when the reviewer returns CLEAN with nothing outstanding.
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

### DeepSearch Loop
*Iterative search -> read -> reason cycle over vector/FTS/ripgrep tools; stop when the optimal answer is found.*  
**Creator:** Han Xiao (Jina AI) · **Source:** https://simonwillison.net/2025/Mar/4/deepsearch-deepresearch/

```text
Answer hard questions by looping search -> read -> reason. Each pass: run the best search (vector, full-text, or ripgrep), read the top results, reason about what is still missing, and issue a sharper next query. Keep going until you have found the optimal, well-supported answer -- not just the first plausible one.
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

### The Screenshot Feedback Loop
*Agent renders its output headless, screenshots it, a vision model critiques the image, and it fixes the code — loop until the visual matches the goal.*  
**Creator:** r/LocalLLaMA (community) · **Source:** https://www.reddit.com/r/LocalLLaMA/comments/1u89f2q/headless_screenshot_loops_let_a_local_30b_agent/

```text
Close the visual feedback loop. After each code change, render the output headless and capture a screenshot. Feed the screenshot to a vision-capable model and ask it to critique against the goal (layout, artifacts, correctness — not the code, the actual pixels). Apply the fixes and re-render. Loop until the rendered result matches the target. Great for UI, games, and graphics where 'it compiles' != 'it looks right'.
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

### Nightly Meditation -> Soul Promotion Loop
*A nightly cron meditation: append dated reflections per topic -> if one recurs 5+ nights AND changes behavior, distill to 1-2 sentences into SOUL.md and archive it; stops promoting when resolved.*  
**Creator:** SIGH_I_CALL (r/OpenClaw) · **Source:** https://www.reddit.com/r/OpenClaw/comments/1rs7yns/

```text
Run a nightly meditation loop. Each night: (1) open meditations.md for active reflection topics; (2) append a dated entry to each reflections/<topic>.md; (3) check whether any reflection has recurred 5+ consecutive nights AND would change your actual operating behavior; (4) if yes, distill it to 1-2 sharp sentences, append to SOUL.md under 'Core Truths', mark the topic archived, and log the breakthrough. Promote ONLY behavioral rules -- never mere sentiment.
```

### Codex Manager/Worker Loop
*A persistent 'manager' session monitors a separate 'worker' session, detects stalls, reviews output, prompts fixes, and advances through ordered tasks; stop when every task passes manager review.*  
**Creator:** albertgao · **Source:** https://x.com/albertgao/status/2068361449072648479

```text
You are the MANAGER agent over a list of N tasks (some must run in a fixed order). Monitor a separate WORKER session per task. After each worker session: (a) review its output against the task spec; (b) if unsatisfactory, send a targeted fix prompt and wait for the worker to re-run; (c) if satisfactory, commit it and advance to the next task. Repeat until all tasks pass review. Stop when every task has a passing review; report a per-task commit summary for human sign-off.
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

### CI-Gated Automated Review Loop
*An agent runs as a CI job on every PR, doing a full review and posting inline comments, iterating until zero blocking findings — before a human is ever assigned.*  
**Creator:** Boris Cherny / Anthropic · **Source:** https://www.reddit.com/r/ClaudeAI/comments/1q2c0ne/

```text
You are an automated code reviewer running in CI on PR #<number>. Fetch the diff (`gh pr diff`). For each changed file check correctness bugs, security issues, broken contracts, and missing tests; post inline comments on blocking issues. Then re-read the diff + latest commit: if all blocking issues are resolved, output REVIEW_PASSED; otherwise output REVIEW_FAILED: <summary> and the job re-triggers on the next push. A human is assigned only after REVIEW_PASSED.
```

### Human Attestation Gate
*After the loop completes, assemble a five-part review frame (promise, acceptance criteria, input-vs-output diff, full evidence ledger, unresolved assumptions) and freeze it; nothing goes downstream until a human signs off.*  
**Creator:** dannwaneri (freeCodeCamp) · **Source:** https://www.freecodecamp.org/news/how-to-build-a-production-safe-agent-loop-from-exit-conditions-to-audit-trails/

```text
You've finished the task loop. Before ANY downstream action (merge, deploy, send, write), assemble a review frame: (1) your original promise/spec, (2) the acceptance criteria, (3) a diff of first input vs final output with turn + token totals, (4) a row-by-row evidence log of every step, (5) any unresolved assumptions or breaches. Present it and HALT. No downstream action happens until a human explicitly signs off; record that attestation as an audit receipt.
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

### Basic Reflection (generator + reflector)
*Generator LLM paired with a reflector LLM playing 'teacher'; generate -> reflect -> revise; stop at an iteration cap.*  
**Creator:** Ankush Gola / LangChain · **Source:** https://www.langchain.com/blog/reflection-agents

```text
Pair two roles. GENERATOR produces the output. REFLECTOR acts as a critical teacher, giving specific feedback on what is weak or wrong. Feed the reflection back to the generator to revise. Loop generate -> reflect -> revise, capping at ~6 iterations so it terminates. Return the final revised output.
```

### Language Agent Tree Search (LATS)
*Reflection + Monte-Carlo tree search: Select -> Expand -> Reflect/Evaluate -> Backpropagate; stop when solved or depth cap.*  
**Creator:** Zhou et al. / LangChain · **Source:** https://www.langchain.com/blog/reflection-agents

```text
For hard multi-step problems, search instead of guessing. Run MCTS over actions: SELECT a promising node, EXPAND candidate next steps, REFLECT/EVALUATE each, and BACKPROPAGATE the value up the tree. Expand the best branches, prune dead ones. Stop when the root is solved or you hit a depth cap (e.g. 5).
```

### On-the-Loop (Harness Loop)
*Humans improve the HARNESS that produces artifacts rather than fixing artifacts directly; agents run the inner loop.*  
**Creator:** Kief Morris (Thoughtworks) · **Source:** https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html

```text
Work ON the loop, not just IN it. Instead of hand-fixing each artifact the agent produces, improve the HARNESS (prompts, checks, scaffolding) that generates them, so the whole class of outputs gets better. Let agents run the inner code loop; you steer the middle loop. Stop investing in the harness when improvements hit diminishing returns.
```

### The 20-Line Agent Loop
*Replace a heavy framework with a tiny hand-rolled loop: call model -> run the tool it asks for -> feed the result back -> repeat until no tool call.*  
**Creator:** r/AI_Agents (community) · **Source:** https://www.reddit.com/r/AI_Agents/comments/1p227ra/i_deleted_400_lines_of_langchain_and_replaced_it/

```text
Don't reach for a framework. Hand-roll the loop: (1) send the messages to the model, (2) if it returns a tool call, execute the tool and append the result to the messages, (3) if it returns a plain answer, you're done. Loop steps 1-2 until the model stops asking for tools. Add a max-iteration cap. Most 'agent' needs are ~20 lines of this, not a library.
```

### Heterogeneous Model Routing Loop
*Orchestrator decomposes a goal into typed subtasks and routes each to the cheapest capable model (strong=plan, cheap=implement, mid=review); validate each, escalate tier on failure; stop when all validators pass or retries exhausted.*  
**Creator:** r/ClaudeAI community (impl: robertgumeny/doug) · **Source:** https://www.reddit.com/r/ClaudeAI/comments/1s3vwy1/

```text
You are an orchestrator for goal: <goal>. (1) Use a strong reasoning model to produce a plan of TYPED subtasks (planning / implementation / review). (2) Route each subtask to a model tier: planning->strong, implementation->cheap/fast, review->mid. (3) Run each subtask in its assigned tier. (4) Run a deterministic validator for that type (lint, tests, diff check). On failure, retry; after 2 failures escalate to the next model tier. Stop when all validators pass or max-retries are exhausted. Report status per subtask. Routing the right model per task type is the point -- don't use one model for everything.
```

### Code-Orchestrated Workflow
*A workflow.js defines phases with structured output schemas; sub-agent outputs flow phase-to-phase WITHOUT re-entering the main context; control flow lives in code, not the model; stops when all phases reach a terminal state.*  
**Creator:** r/ClaudeAI (alphastar777, willwashburn) · **Source:** https://www.reddit.com/r/ClaudeCode/comments/1tkjy4u/

```text
Define a workflow in code (workflow.js), not in the model. Each phase specifies: a model-invocation step (the judgment call), a structured JSON output schema, and a next-phase routing rule. Sub-agents run each phase in their OWN isolated context; outputs pass forward as structured data, never raw text. Put conditionals, retries, and parallelism in the JS -- never ask the model to decide control flow. Stop when the final phase's completion condition is met and all structured outputs are written to disk.
```


## Loop frameworks (GitHub)

### ralph-loop-agent
*Wraps the AI SDK's generateText in an outer loop: run -> verifyCompletion -> inject feedback if not done -> repeat until success or a cost/iteration cap. ~800 stars.*  
**Creator:** vercel-labs · **Source:** https://github.com/vercel-labs/ralph-loop-agent

```text
Use ralph-loop-agent (Vercel AI SDK) to wrap a model call in a Ralph-style outer loop: it runs the LLM, calls a verifyCompletion check, and if not done, injects the feedback and loops — stopping on success or a cost/iteration threshold. Good for adding 'keep going until verified' autonomy to an AI SDK app. (See the repo.)
```

### continuous-claude
*Runs Claude Code in a continuous loop that autonomously opens PRs, waits for CI, merges, then starts the next task — context carried in a markdown handoff file. ~1.4k stars.*  
**Creator:** AnandChowdhary · **Source:** https://github.com/AnandChowdhary/continuous-claude

```text
Use continuous-claude to run Claude Code in a continuous loop: it picks the next task, implements it, opens a PR, waits for CI, merges when green, and carries context forward via a shared markdown handoff file — then starts the next task. Set a task list and a stop condition. (See the repo.)
```

### loki-mode
*Multi-agent autonomous SDLC orchestrator running Reason-Act-Reflect-Verify cycles with quality gates, from PRD or one-line brief to deployed app. ~982 stars.*  
**Creator:** asklokesh · **Source:** https://github.com/asklokesh/loki-mode

```text
Use loki-mode to run a multi-agent autonomous SDLC: give it a PRD or one-line brief and it runs Reason -> Act -> Reflect -> Verify cycles across specialized agents, passing through quality gates toward a deployed app. (See the repo for setup.)
```

### ouroboros
*Spec-first loop: a Socratic interview crystallizes an immutable spec, tasks are decomposed and executed, an evaluator scores outputs, and the loop runs until similarity to spec is high. ~4.6k stars.*  
**Creator:** Q00 · **Source:** https://github.com/Q00/ouroboros

```text
Use ouroboros ('stop prompting, start specifying'): it runs a Socratic interview to crystallize an immutable spec, decomposes the work, executes tasks, and has an evaluator score outputs against the spec — looping until the spec is satisfied to a high similarity threshold. (See the repo.)
```

### claude-code-harness
*Enforces a Plan -> Work -> Review -> Ship cycle for Claude Code: specs approved before implementation, review gated separately, evidence packaged before release. ~2.8k stars.*  
**Creator:** Chachamaru127 · **Source:** https://github.com/Chachamaru127/claude-code-harness

```text
Use claude-code-harness to enforce a Plan -> Work -> Review -> Ship loop in Claude Code: the spec must be approved before implementation, review is a separate gate, and evidence is packaged before release — so quality gates can't be skipped. (See the repo.)
```

### EvoAgentX
*Self-evolving agent framework: evaluators score agents, then TextGrad/AFlow/EvoPrompt optimization evolves both prompts and workflow structure across iterations. ~3.1k stars.*  
**Creator:** EvoAgentX · **Source:** https://github.com/EvoAgentX/EvoAgentX

```text
Use EvoAgentX to build self-evolving agents: automated evaluators score your agents on benchmarks, then optimization algorithms (TextGrad / AFlow / EvoPrompt) evolve both the prompts and the workflow structure across iterations — improving the system automatically. (See the repo.)
```

### self_improving_coding_agent
*Four-step self-referential loop: evaluate the agent on benchmarks -> archive -> let it improve its OWN codebase -> repeat, stacking measured gains. ~353 stars.*  
**Creator:** MaximeRobeyns · **Source:** https://github.com/MaximeRobeyns/self_improving_coding_agent

```text
Use self_improving_coding_agent to run a self-referential loop: evaluate the agent on benchmarks, archive the results, then point the agent at its OWN codebase to improve it, and repeat — stacking only improvements that measurably raise benchmark performance. (See the repo.)
```

### helixent
*Minimal TypeScript library for ReAct-style agent loops (think -> act -> observe) on Bun, with parallel tool calls and observation injection. ~582 stars.*  
**Creator:** MagicCube · **Source:** https://github.com/MagicCube/helixent

```text
Use helixent (TypeScript/Bun) to build a ReAct-style loop: the agent thinks, acts (calls tools, in parallel where possible), observes the results, and feeds observations back into the next reasoning step — looping until done. A small library, not a full framework. (See the repo.)
```

### millrace
*Configurable governed agentic-loop runtime: explicit stage gates, durable queues, compiled execution plans, and recovery rules that persist state across context windows. ~48 stars.*  
**Creator:** tim-osterhus · **Source:** https://github.com/tim-osterhus/millrace

```text
Use millrace to run a governed agentic loop: define explicit stage gates, durable queues, and recovery rules so the loop's state persists across individual agent context windows and execution is reliable rather than ad-hoc. (See the repo for setup.)
```

### foreman
*Boris-style TUI supervisor for headless Claude Code agents: plan -> ADR/PRD -> issues -> TDD build -> e2e, with human review gates and per-worktree budget caps. ~56 stars.*  
**Creator:** VisionForge-OU · **Source:** https://github.com/VisionForge-OU/foreman

```text
Use foreman, a TUI supervisor for headless Claude Code agents: it drives plan -> ADR/PRD -> issues -> TDD build -> e2e with human review gates at the design stages and per-worktree budget caps, so multiple agents run under control. (See the repo.)
```

### llm-loop
*Plugin for Simon Willison's `llm` CLI that runs a turn-based autonomous loop (configurable --max-turns, default 25) with optional manual tool-call approval. ~17 stars.*  
**Creator:** nibzard · **Source:** https://github.com/nibzard/llm-loop

```text
Use the llm-loop plugin for the `llm` CLI to run a turn-based autonomous loop: the agent chains observations into the next turn, bounded by --max-turns (default 25), with optional manual approval of tool calls. (See the repo.)
```

### awesome-harness-engineering
*Awesome-list of agent-loop design primitives: planning, context mgmt, MCP, permissions, memory, orchestration, verification, observability, HITL. ~1.9k stars.*  
**Creator:** ai-boost · **Source:** https://github.com/ai-boost/awesome-harness-engineering

```text
Browse awesome-harness-engineering — the reference index for the whole agent-harness space: planning, context management, MCP integration, permissions, memory, orchestration, verification, observability, and human-in-the-loop patterns. Use it to design your own loops. (See the repo.)
```

### agent-skills (Addy Osmani)
*Production Claude Code slash-command suite (/spec /plan /build /test /review /ship) implementing a verifiable multi-phase loop; `/build auto` removes human stepping. ~64k stars.*  
**Creator:** addyosmani · **Source:** https://github.com/addyosmani/agent-skills

```text
Use Addy Osmani's agent-skills: a slash-command suite for Claude Code (/spec, /plan, /build, /test, /review, /ship) that implements a verifiable multi-phase development loop. Run them in order, or `/build auto` to remove human stepping between tasks. (See the repo.)
```

### Boomerang Tasks (Roo Code)
*Parent task delegates subtasks to specialist modes; each runs in isolated context and signals attempt_completion; ends when all return.*  
**Creator:** RooCodeInc · **Source:** https://roocodeinc.github.io/Roo-Code/features/boomerang-tasks

```text
Use an orchestrator that delegates. The parent task breaks the goal into subtasks and hands each to a specialist mode (Code, Debug, Architect), each running in its OWN isolated context. Each subtask signals attempt_completion when done and 'boomerangs' back. The orchestrator synthesizes the results once all subtasks return. (Roo Code feature.)
```

### Forge
*Idea -> R-numbered spec -> dependency-ordered task DAG -> TDD per git worktree -> reviewer + 4-level verifier; stop on FORGE_COMPLETE or budget. ~29 stars.*  
**Creator:** LucasDuys · **Source:** https://github.com/LucasDuys/forge

```text
Use Forge: it turns an idea into an R-numbered spec, builds a dependency-ordered task DAG, then executes each task TDD-style in its own git worktree, with a reviewer plus a 4-level verifier. It stops on a FORGE_COMPLETE promise signal or when the budget is exhausted (writing .forge/resume.md to continue later). (See the repo.)
```

### Cavekit
*grill -> spec -> research -> review -> build over a durable SPEC.md; test failures back-propagate into spec invariants. ~1k stars.*  
**Creator:** JuliusBrussee · **Source:** https://github.com/JuliusBrussee/cavekit

```text
Use Cavekit's spec-driven loop: grill -> spec -> research -> review -> build, all centered on a single durable SPEC.md. When tests fail, the failures back-propagate into the spec's invariants (a 'backprop reflex'), so the spec tightens over time. Stop when tests satisfy all invariants in the spec. (See the repo.)
```

### ORCH
*CTO agent splits goal into tasks; parallel engineering agents in isolated worktrees; QA verifies; state machine todo->in_progress->review->done. ~83 stars.*  
**Creator:** oxgeneral · **Source:** https://github.com/oxgeneral/orch

```text
Use ORCH: a CTO agent breaks the goal into tasks, parallel engineering agents work in isolated git worktrees, and QA agents verify. Tasks move through a state machine (todo -> in_progress -> review -> done). Run with --once to exit when all tasks reach a terminal status. (See the repo.)
```

### Bernstein
*Manager decomposes goal -> agents in isolated worktrees -> janitor verifies (tests/lint/types) -> verified work merges; loop nodes re-fire until a bash predicate exits 0. ~574 stars.*  
**Creator:** Alex Chernysh · **Source:** https://github.com/chernistry/bernstein

```text
Use Bernstein for audit-grade multi-agent work: a manager decomposes the goal, agents run in isolated worktrees, and a 'janitor' verifies each (tests, lint, types) before verified work merges. Workflow loop nodes re-fire until a bash predicate exits 0. Stop with `bernstein stop` or when all agents exit clean. (See the repo.)
```

### GreatCTO
*Spec synthesis -> single human approval gate -> scaffold/backend/frontend/test/deploy; risk-tiered gates; stop when a live URL ships. ~41 stars.*  
**Creator:** avelikiy · **Source:** https://github.com/avelikiy/great_cto

```text
Use GreatCTO: it synthesizes a spec, pauses at a single human 'CTO' approval gate, then runs scaffold -> backend -> frontend -> test -> deploy automatically. Gates are risk-tiered (maintenance = no gate; irreversible changes = full gate + frontier model). Stops when a live URL ships. (See the repo.)
```

### pi-ralph
*Agent cycles through named 'hats' (roles) triggered by emitted events; stop on a completion_promise string or max_iterations/runtime. ~13 stars.*  
**Creator:** samfoy · **Source:** https://github.com/samfoy/pi-ralph

```text
Use pi-ralph: the agent cycles through named 'hats' (roles), each triggered by emitted events. It stops on a configurable completion_promise string (e.g. LOOP_COMPLETE) or on the max_iterations / max_runtime_seconds guard rails. A role-cycling take on the Ralph loop. (See the repo.)
```

### CCG Workflow
*Classify -> parallel Codex+Gemini analysis -> plan -> hard-stop user approval -> parallel impl -> dual-model cross-review -> quality gates. ~5.6k stars.*  
**Creator:** fengshao1227 · **Source:** https://github.com/fengshao1227/ccg-workflow

```text
Use CCG: /ccg:go classifies the task, runs parallel Codex + Gemini analysis, produces a plan, then HARD-STOPS at a user approval gate. On approval, parallel implementation agents build it, followed by dual-model cross-review and quality gates. Stops when all phase gates pass or the user rejects the plan. (See the repo.)
```

### Claude Engineer v3 (tool-creation loop)
*Agent detects a capability gap, generates a new tool, validates, hot-reloads it, and chains tools; bounded by MAX_CONVERSATION_TOKENS. ~11k stars.*  
**Creator:** Doriandarko · **Source:** https://github.com/Doriandarko/claude-engineer

```text
Use Claude Engineer v3's self-expanding loop: when the agent hits a capability gap, it designs and generates a NEW tool via its toolcreator, validates it, hot-reloads it dynamically, and chains tools automatically to finish the task. It stops when it judges the task complete; MAX_CONVERSATION_TOKENS is the hard bound. (See the repo.)
```

### Autoharness Loop
*An outer agent proposes changes to your agent HARNESS (prompts, params, context), benchmarks each on a fixed eval, keeps only wins; stops when gains stall or N candidates run. ~295 stars.*  
**Creator:** Lucky_Historian742 / kayba-ai · **Source:** https://github.com/kayba-ai/autoharness

```text
You are a harness optimizer improving the agent system described in GUIDE.md. Loop: (1) propose ONE targeted change to a harness parameter -- a prompt section, a value, a context injection, or a scoring rule; (2) apply it to a staging copy; (3) run the benchmark suite and record the score; (4) if it improved, promote it as the new baseline, else revert. Continue until three consecutive proposals fail to improve or you hit N candidates. Report the change log with before/after scores.
```

### Mutable-Queue Worktree Loop
*Drains a LIVE task queue; each task runs implement->review->fix in its own git worktree and auto-merges; the queue can be edited mid-run; stops when the queue is empty. ~9 stars.*  
**Creator:** AmandEnt / ofux · **Source:** https://github.com/ofux/lauren

```text
Run a mutable task queue. For each task at the head: (1) create an isolated git worktree; (2) implement it; (3) review the result with a separate review agent; (4) fix any blocking issues; (5) merge the worktree back and delete it; (6) mark it complete. After each task, RE-READ the queue file -- the operator may have appended or reordered tasks mid-run. Never merge while the reviewer has outstanding blockers; loop back to step 4. Stop when the queue is empty.
```

### ACE: Skill-Injection Reflection Loop
*Run task -> a Reflector analyzes the trace -> a SkillManager updates a persistent 'Skillbook' of heuristics -> restart with them injected; stops when tests pass clean or after N epochs. ~2.5k stars.*  
**Creator:** cheetguy / kayba-ai · **Source:** https://github.com/kayba-ai/agentic-context-engine

```text
Run a multi-epoch learning loop. Each epoch: (1) run the task using the current Skillbook heuristics injected into your system prompt; (2) hand the full execution trace to a Reflector that extracts what worked and what failed; (3) pass those findings to a SkillManager that adds/refines/removes entries in a persistent Skillbook file; (4) start the next epoch with the updated Skillbook. Stop when the build is error-free and all tests pass, or after N epochs. Only the SkillManager may write the Skillbook -- never edit it yourself.
```

### Taskmaster Next-Task Driver
*Parse a PRD into a dependency-ordered task graph; `next` returns the immediately-unblocked task; implement -> done -> next; stop when no task has unmet dependencies. ~27.6k stars.*  
**Creator:** eyaltoledano · **Source:** https://github.com/eyaltoledano/claude-task-master

```text
Parse the PRD with `task-master parse-prd` to build a dependency-ordered task graph. Then loop: call `task-master next` to get the next UNBLOCKED task, implement it (use `task-master expand` to split it into subtasks if complex), mark it done, and call `next` again. Stop when `task-master next` returns nothing -- that means every dependency chain is resolved. Let the graph, not your guesses, decide order.
```

### feature-dev 7-Phase Gate Loop
*Seven phases (discovery -> codebase exploration -> clarifying Qs -> architecture -> implement -> review -> summary) with hard human-approval gates before architecture and implementation. ~133k stars.*  
**Creator:** Anthropic (Claude Code team) · **Source:** https://github.com/anthropics/claude-code/blob/main/plugins/feature-dev/commands/feature-dev.md

```text
Run feature-dev. Phase 1: ask clarifying questions about the problem + constraints. Phase 2: spawn parallel agents to map the codebase (architecture, similar patterns, relevant files). Phase 3: surface every gap/ambiguity and WAIT for my answers. Phase 4: propose 2-3 architecture approaches with trade-offs -- do NOT proceed until I pick one. Phase 5: implement the chosen design. Phase 6: launch reviewer agents, consolidate findings, present them, and ask fix-now-or-defer. Phase 7: write a summary of decisions. The human gates before phases 4 and 5 are mandatory.
```

### SpecPulse CLI-First Execute Loop
*CLI scaffolds the feature spec first, then /sp-execute runs pick-next -> implement -> validate -> mark-complete continuously until /sp-validate confirms the whole spec is met. ~389 stars.*  
**Creator:** abdullahazad / specpulse · **Source:** https://github.com/specpulse/specpulse

```text
Initialize with `/sp-pulse <feature>`, then `/sp-spec` for requirements and `/sp-plan` + `/sp-task` to break them into tasks. Then `/sp-execute all`: for each pending task, implement it, validate against its success criteria, mark it complete, move on. Repeat until no pending tasks remain, then run `/sp-validate` to confirm the full spec is met. Stop when validate exits clean.
```

### REAP Generational Loop
*Five phases (learning -> planning -> implement<->validate -> completion) that evolve a project 'Genome' across generations; the Genome is read-only mid-generation; stops at human fitness approval. ~43 stars.*  
**Creator:** casamia123 / c-d-cc · **Source:** https://github.com/c-d-cc/reap

```text
Start a new REAP generation. Work the five phases in order: LEARNING (read .reap/genome/ + current state), PLANNING (write 02-planning.md), IMPLEMENTATION, VALIDATION (loop back to implementation if checks fail), COMPLETION (write 05-completion.md with fitness notes + proposed Genome changes). Do NOT modify .reap/genome/ during the generation -- log issues to the backlog. Stop and present the completion document for my approval before any Genome change.
```

### APM (Agentic Project Management)
*Tripartite Planner -> Manager -> Worker loop with human checkpoints and context-overflow Handoff docs; stops when the Manager verifies all plan tasks complete. ~2.3k stars.*  
**Creator:** sdi2200262 · **Source:** https://github.com/sdi2200262/agentic-project-management

```text
Run an APM session. (1) As PLANNER: decompose the project into a structured plan.md with numbered tasks + acceptance criteria. (2) A MANAGER conversation takes plan.md and assigns ONE task at a time to a WORKER conversation, then reviews the returned output. (3) Each WORKER runs its task in isolation and writes a structured completion report. When a Worker's context nears capacity, produce a HANDOFF doc summarizing accumulated knowledge so a fresh Worker continues without loss. Loop ends when the Manager confirms all plan tasks are verified complete.
```


## International (translated)

### Loop Engineering (循环工程)
*Write the program that drives the agent: goal -> execute -> judge -> re-prompt with errors -> repeat; stop on budget or judge pass. [translated from Chinese]*  
**Creator:** Omar (omarsar0); ThinkInAI community · **Source:** https://www.53ai.com/news/tishicijiqiao/2026062001243.html

```text
Stop hand-writing prompts; engineer the loop. Define the goal and a JUDGE that decides done. Each pass: execute the step, have the judge score the result, and if not done, re-prompt the agent with the specific errors. Set a hard budget (max attempts, time, files changed, or spend) as the safety stop. Exit when the judge passes or the budget is exhausted.
```

### MetaSkills Self-Bootstrap Loop (元技能自举)
*Agent generates new reusable workflow templates for itself: match -> fill -> DAG conflict check -> quality gate -> sandbox dry-run -> human approval. [translated from Chinese]*  
**Creator:** geffzhang; via 53AI · **Source:** https://www.53ai.com/news/Assistant/2026061894560.html

```text
Let the agent build its own reusable skills. Loop: match the task to an existing template (or none), have the LLM fill in the steps, run a DAG conflict check, pass a quality gate, then a sandbox dry-run. Gate on human Accept / Dismiss / Revise before saving the new template. Over time the agent bootstraps new MetaSkills using its existing ones.
```

### Judge-Model Termination Loop (法官模型)
*Pursue a persistent goal across turns with a SEPARATE judge model deciding completion (not self-declaration); parallel tool calls. [translated from Chinese]*  
**Creator:** Youming Zhang, Tencent Cloud · **Source:** https://cloud.tencent.com/developer/article/2669097

```text
Pursue the goal across multiple turns. Crucially, do NOT let the acting agent declare itself done -- use a SEPARATE judge model to decide completion each turn. Execute tool calls in parallel where safe. Stop only when the judge declares the goal met (or a human pauses). This removes the self-grading bias that makes agents quit early or loop forever.
```

### Self-Repair Loop (pass@t)
*Four roles: generator -> executor (unit tests) -> feedback model -> repair model; separate feedback model from actor; stop when a sample passes all tests. [translated from Chinese]*  
**Creator:** Jianfeng Gao & Chenglong Wang, Microsoft Research · **Source:** https://cloud.tencent.com/developer/article/2308702

```text
Repair code with four distinct roles: GENERATOR writes a candidate, EXECUTOR runs the unit tests, a separate FEEDBACK model explains why it failed, and a REPAIR model fixes it using that feedback. Keep the feedback model DIFFERENT from the actor (a stronger feedback model repairs weaker code far better). Loop until a sample passes all tests.
```

### Prefix-Caching Agent Loop (前缀缓存)
*Tool-call loop with the invariant that the old prompt is always an exact prefix of the new one, making per-token cost linear via KV-cache reuse. [translated from Chinese]*  
**Creator:** OpenAI Eng; via Synced (机器之心) · **Source:** https://cloud.tencent.com/developer/article/2624854

```text
Run the tool-call loop (input -> infer -> decode -> decide -> execute) but enforce one structural invariant: the previous prompt must always be an exact PREFIX of the next prompt, so the KV-cache is reused and per-token cost stays linear instead of quadratic. Compact context past a threshold rather than rewriting earlier turns. Stop when the model returns an assistant message with no tool calls.
```


---
Credits to every original creator listed. Curation + prompt wording: MIT. Contribute / fix attribution: https://github.com/keysersoose/loop-library/issues
