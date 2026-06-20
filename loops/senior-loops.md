<!-- SENIOR-LOOPS v1.1 — last updated 2026-06-19 -->

# SENIOR-ENGINEER BUILD LOOPS

A drop-in set of loop prompts. Paste this whole file into your project's
`CLAUDE.md` (or keep it as `LOOPS.md` and tell Claude "follow LOOPS.md").
From then on, whatever you ask it to build, these loops force the work up to
the quality a senior/staff engineer would ship — catching the things a junior
forgets (security, edge cases, tests, "what breaks at scale").

You describe the idea. The loops bring in the expert.

---

## HOW THESE LOOPS ARE BUILT (so you can write more of your own)

Every loop here follows the same five-part shape, because that's what makes an
LLM follow a loop reliably instead of spinning or quitting early:

- **ENTER** — the one condition that starts the loop.
- **EACH ITERATION** — the concrete steps, small enough to do in one pass.
- **CONTINUE** — a *measurable* reason to go around again (not "until it's good").
- **EXIT** — an *observable* finish line (a command passes, a box is verified).
- **SAFETY EXIT** — a hard cap (max N rounds / no-progress) that stops the loop
  and asks you, so it can never run forever or ping-pong.

Two rules make the difference between a loop that works and one that lies to you:
1. **Every EXIT must be checkable by an artifact** — a passing command, a diff, a
   tool's output — never a prose judgment the agent grades itself on.
2. **The writer never grades its own work.** Any "review/verify" step is done by a
   FRESH reviewer (separate subagent / new session) — see the box in Loop 5.

---

## PRIME DIRECTIVE (read before every build)

1. **Treat all generated code as untrusted external input.** Every check you'd
   run on an unknown vendor's code applies to your own. Plausible ≠ correct.
2. **"Done" is not when it runs — it's when the DEFINITION-OF-DONE LOOP passes,
   box by box, each backed by an artifact.** Never say it's finished before then.
3. **Think in failure modes and blast radius before correctness.** Ask "what
   breaks if this fails, and can I undo it?" before "is this elegant?"
4. **Non-functional requirements are decided up front, not retrofitted.** Auth,
   data isolation, error handling, observability, and scale are part of the
   design — not a later pass.
5. **The writer never grades its own work.** "Review" and "verify" steps use a
   FRESH reviewer with no memory of writing the code (see Loop 5's invocation
   block). Self-review is theatre — do not do it.
6. **One fix at a time, reversible.** Atomic commits. If a change makes things
   worse — or breaks a previously-passing test — revert it before trying again.

---

## MASTER BUILD LOOP — run this for any "build me X" request

```
ENTER when: the user asks to build, add, or change a feature.

For the whole request, and again for EACH feature inside it, walk this chain.
A stage may only start when the previous stage's EXIT condition is met.

  1. SPEC LOOP                — lock down what "correct" means
  2. PLAN & BLAST-RADIUS LOOP — decide the approach + what could break
       └─ MIGRATION GATE      — fires if the plan touches the database schema
  3. TEST-FIRST LOOP         — write the test, then the code
  4. SECURITY LOOP           — harden it (the #1 thing juniors miss)
  5. CRITIC / REVIEW LOOP    — a FRESH reviewer tries to break it
  6. DEBUG / SELF-HEAL LOOP  — fired whenever anything fails; root-cause it
  7. DEFINITION-OF-DONE LOOP — the final gate; only this declares "100%"

RE-ENTRY RULE: when a later loop sends you back to an earlier one, you must
  re-run every loop from that point FORWARD before returning. A fix made in
  TEST-FIRST must pass TEST-FIRST → SECURITY → CRITIC again before DONE.

"NO PROGRESS" is defined as: no acceptance criterion moved from failing to
  passing during a full chain pass. (Finding new issues is not progress.)

CONTINUE: if the request has more features/phases, return to step 1 for the next.
EXIT: every feature has passed the DEFINITION-OF-DONE LOOP.
SAFETY EXIT: if one feature shows NO PROGRESS for 2 full chain passes, QUARANTINE
  it — log it as BLOCKED with one specific question, skip to the next feature,
  and surface all blocked items to the user at the end. Never spin on one feature.
```

---

## LOOP 1 — SPEC LOOP

*Closes the gap: vague ideas → code that does the wrong thing.*

```
ENTER when: about to build anything not yet specified.

Each iteration:
  1. Restate the idea as concrete, TESTABLE acceptance criteria
     ("Given X, when the user does Y, then Z happens").
  2. Force the non-functional questions a junior skips. Get an explicit answer
     (a sensible default is fine, but it must be STATED) for each that applies:
       - Who is allowed to do this? Who must be blocked? (auth / authz)
       - Whose data can each user see? (data isolation)
       - What are the inputs, and what's the invalid/malicious version of each?
       - What happens on failure / empty / huge input / concurrent use?
       - How big does this get (users, rows, requests)? What breaks at 100x?
       - What must be observable when it goes wrong in production?
  3. List what is explicitly OUT of scope (YAGNI — cut it now).

CONTINUE while: any acceptance criterion is not testable, OR any non-functional
                question above is unanswered/ambiguous.
EXIT when: the spec is unambiguous and testable. If the user is present, get
           their explicit confirmation. If running AUTONOMOUSLY (no interactive
           session), proceed on labeled assumptions and put the assumption list
           at the top of the first commit message — do not stall waiting.
SAFETY EXIT: if two scope/NFR questions stay ambiguous after asking, present the
             best-guess spec, label the assumptions, and ask the user to confirm.
```

---

## LOOP 2 — PLAN & BLAST-RADIUS LOOP

*Closes the gap: jumping straight to code; not seeing what a change endangers.*

```
ENTER when: the SPEC LOOP has passed for this feature.

Each iteration:
  1. Read the relevant existing code FIRST (don't edit yet). Note the patterns
     and conventions already in use — follow them.
  2. Write the plan: the files/functions to touch, the data flow, and the
     interfaces between pieces (each unit = one clear purpose).
  3. State explicitly:
       - What "done" looks like (ties back to the spec's acceptance criteria).
       - BLAST RADIUS: what else depends on what you're changing? What breaks
         if this is wrong? (check imports, callers, tests, configs)
       - REVERSIBILITY: how do you undo this if it goes bad? Prefer changes you
         can roll back over edits you can't.
  4. Pick the SMALLEST change that satisfies the spec. No bonus features.

CONTINUE while: the plan has an unknown ("not sure how X works") — go read it.
EXIT when: the plan is concrete, blast radius is understood, and the change is
           the smallest one that works.
SAFETY EXIT: if the blast radius is large or the change is irreversible, STOP and
             surface this to the user before writing any code.
```

### MIGRATION GATE (fires inside Loop 2 when the plan changes the DB schema)

*Closes the gap: a rolled-back migration against live data is NOT the same as
never running it — the single most irreversible thing a junior does.*

```
Before writing any schema change, answer all four — if any is "no", redesign:
  [ ] DOWN PATH: is there a reversible down migration (or a documented manual
      undo)? A destructive change (drop/rename column) must be staged as
      add-new → backfill → switch reads → drop-old, never an in-place rename.
  [ ] MIXED-VERSION SAFE: during a rolling deploy the DB may be one step ahead
      of the code (or behind). Does the app tolerate both states?
  [ ] LOCK RISK: does this lock a table that has live write traffic? At what row
      count does it become a problem?
  [ ] DATA LOSS: does any step drop or overwrite data that can't be recovered?
EXIT: all four answered safely, with the up AND down migration written.
```

---

## LOOP 3 — TEST-FIRST LOOP

*Closes the gap: no tests; happy-path-only code; silent regressions.*

```
ENTER when: the PLAN LOOP (and MIGRATION GATE if relevant) passed.

Each iteration (per acceptance criterion):
  1. Write a test that encodes the criterion — INCLUDING the edge/error cases
     named in the spec (empty, invalid, too large, unauthorized, concurrent).
  2. Run it. Confirm it FAILS FOR THE RIGHT REASON: the assertion itself fails,
     NOT an import error, syntax error, or fixture crash. The error message must
     reference the behavior under test. (A test that errors on import is not a
     real failing test — fix the test harness first.)
  3. Write the minimal code to make it pass. Nothing extra.
  4. Run the FULL test suite — not just the new test — to catch regressions.
  5. Refactor for clarity while green. Keep units small and single-purpose.

CONTINUE while: any acceptance criterion (incl. its edge cases) lacks a passing
                test, OR any existing test is now broken.
EXIT when: every criterion has a passing test and the whole suite is green
           (paste the green test-runner output as the artifact).
SAFETY EXIT: if a criterion genuinely can't be tested automatically, say so
             explicitly and write a manual verification step instead — never
             silently skip it.
```

---

## LOOP 4 — SECURITY LOOP

*Closes the gap: the #1 failure mode. Auth holes, leaked data, secrets, injection.*

```
ENTER when: a feature's tests are green (after TEST-FIRST LOOP).

Each iteration — go down this checklist and FIX every hit before moving on:
  1. AUTH/AUTHZ: is every sensitive action checked server-side? Is any check
     client-side-only or invertible? Can an anonymous user reach it?
  2. DATA ISOLATION: can user A read/modify user B's data? Is row-level
     security / ownership actually enforced on every query?
  3. SECRETS: any API key, token, or password in code, config, or the frontend
     bundle? Move to env/secret store. Confirm none reach the client.
     → VERIFY by running a secret scanner (gitleaks / trufflehog) and reading
       the output. If none is installed, install one.
  4. INPUT VALIDATION: is every input validated and every query parameterized?
     (SQLi, XSS, command injection, path traversal). No string-concatenated SQL.
  5. INSECURE DEFAULTS: over-broad permissions (IAM `*`, open buckets), missing
     rate limiting, missing security headers, weak crypto (MD5/ECB)?
  6. DEPENDENCIES: → VERIFY by running `pip audit` (Python) or
     `npm audit --audit-level=high` (Node) and pasting the output. If a package
     cannot be found in the public registry, that is a CRITICAL finding
     (hallucinated / typosquatted package). Install the audit tool if missing.
  7. EXCESSIVE AGENCY: does this code/agent have more access than it needs
     (e.g. prod write access, delete rights)? Apply least privilege.

CONTINUE while: any checklist item has an open finding.
EXIT when: zero critical/high findings remain AND the scanner + audit outputs are
           clean (those tool outputs are the artifact). Document anything
           deliberately accepted, with the reason.
SAFETY EXIT: if a finding needs a product decision (e.g. "should guests see
             this?"), stop and ask the user rather than guessing.
```

---

## LOOP 5 — CRITIC / REVIEW LOOP

*Closes the gap: self-graded code that "looks right" but is wrong. This is the
most important — and most easily faked — loop in the file. Do it for real.*

```
ENTER when: a feature passed TEST-FIRST + SECURITY.

Each iteration:
  1. Hand the diff to a FRESH reviewer (see invocation block below). It must NOT
     be the instance/context that wrote the code.
  2. The reviewer's job is to BREAK it, checking against the spec + rubric:
       - Does it actually meet every acceptance criterion?
       - Bugs, off-by-one, unhandled errors, race conditions?
       - Does it match the codebase's existing patterns? Any dead code?
       - Did the SECURITY LOOP miss anything? Try the adversarial cases:
         cross-user access, auth bypass, malicious input, tool misuse.
       - What breaks at 100x scale / under partial failure?
  3. Collect findings. Fix the real ones — run each fix back through TEST-FIRST
     (and forward per the RE-ENTRY RULE) so every fix gets a test.

CONTINUE while: the fresh reviewer reports a real, in-scope issue — UP TO 3 ROUNDS.
EXIT when: a fresh reviewer returns no real findings, OR 3 rounds are reached —
           at which point log any remaining findings, triage each as
           Critical / Non-critical, FIX all Critical, and DEFER Non-critical
           with a written note. Never loop past 3 rounds.
SAFETY EXIT: if reviewer and author disagree on the SAME point across 2 rounds
             with no convergence, surface both views to the user to decide.
```

```
HOW TO GET A FRESH REVIEWER IN CLAUDE CODE (pick one, in priority order):
  A. Subagent:  Agent({ subagent_type: "reviewer",
                        prompt: "You did NOT write this code. Break-it review of
                                 this diff against this spec + rubric. <paste>" })
  B. Skill:     run /code-review (or /review) if available in this project.
  C. New session: open a fresh Claude Code session with ZERO context and paste
                  only the material below.
  NEVER: ask the same session that wrote the code to "now review it." That is
         role-play, not independence, and gives zero epistemic distance.

CONTEXT HANDOFF — the reviewer receives ONLY these three things, nothing else:
  1. the git diff,
  2. the acceptance criteria from Loop 1,
  3. the Loop 5 rubric above.
  Do NOT pass the implementation plan, the author's reasoning, or prior chat —
  that contamination makes the review non-independent regardless of who runs it.
```

---

## LOOP 6 — DEBUG / SELF-HEAL LOOP

*Closes the gap: guess-and-patch debugging that masks bugs instead of fixing them.*

```
ENTER when: any test fails, any error appears, or behavior is wrong — at ANY stage.

Each iteration (scientific method — no random changes):
  1. Reproduce the failure reliably. If you can't reproduce it, that's step one.
  2. Form ONE hypothesis about the root cause. State it.
  3. Find the cheapest test/log that would confirm or kill that hypothesis.
  4. Run it. Hypothesis killed? Discard it and form the next one.
  5. Confirmed? Fix the ROOT CAUSE (not the symptom). One atomic change.
  6. Re-run the failing case AND the full suite. Revert immediately if it
     didn't help or made things worse. REGRESSION GUARD: if a previously-green,
     unrelated test is now failing, that is a NEW regression you introduced —
     revert the last atomic change at once and count it as a killed hypothesis.
     Do not try to "also fix" it inside this loop.

CONTINUE while: the failure still reproduces, OR you fixed a symptom not a cause.
EXIT when: the original failure is gone, the full suite is green, and you can
           explain WHY it broke and why the fix works.
SAFETY EXIT: after 3 killed hypotheses with no progress, stop and report what
             you've ruled out — ask the user before flailing further.
```

---

## LOOP 7 — DEFINITION-OF-DONE LOOP

*Closes the gap: "it runs" mistaken for "it's finished." The only loop that may
declare the work 100%. Every box needs an ARTIFACT, not a prose opinion.*

```
ENTER when: a feature has passed CRITIC / REVIEW.

Each iteration — verify every box WITH ITS ARTIFACT; if one fails, go back to
the loop that owns it (and re-run forward per the RE-ENTRY RULE):

  [ ] TESTS: every acceptance criterion has a passing test; full suite green.
      ARTIFACT: paste the green test-runner output (e.g. `pytest -q` / `npm test`).
  [ ] SECURITY: no open critical/high findings; no secrets in code.
      ARTIFACT: clean secret-scan + dependency-audit output.
  [ ] ERROR HANDLING: failure, empty, and invalid paths are handled and don't
      leak internals. ARTIFACT: name the tests that exercise these paths.
  [ ] OBSERVABILITY: key actions log structured fields (≥ timestamp, operation,
      user/request id, outcome); external calls log upstream failures; a health
      check / smoke test exists. ARTIFACT: name the specific log lines + endpoint.
  [ ] SCALE SANITY: no obvious N+1 / unbounded query; behaves at the scale the
      spec named. ARTIFACT: name the query/loop reviewed or the benchmark run.
  [ ] DOCS: how to run/use it is written; config + env vars documented.
      ARTIFACT: the doc/README section.
  [ ] REVERSIBILITY: a clear rollback path exists (and a down-migration if the
      schema changed). ARTIFACT: name the rollback step.
  [ ] CLEAN: no dead code, no leftover debug, no blocker TODOs.
      ARTIFACT: the diff scanned for these.

CONTINUE while: any box lacks a verified artifact → return to the owning loop.
EXIT when: every box has its artifact. ONLY NOW report the feature as done.
SAFETY EXIT: never check a box without producing its artifact. If you can't
             produce one, say so plainly instead of declaring done.
```

---

## CHEAT SHEET

    build request
       └─ per feature ───────────────────────────────────────────
          SPEC ▸ PLAN/BLAST-RADIUS (▸MIGRATION GATE) ▸ TEST-FIRST
               ▸ SECURITY ▸ CRITIC ▸ DONE
                      (DEBUG/SELF-HEAL fires on any failure, any stage)

- A stage can't start until the previous one's EXIT condition is met.
- "Review" and "verify" always use a FRESH reviewer, never the author.
- Every EXIT needs an artifact (passing command / tool output / diff), not a vibe.
- Nothing is "done" until LOOP 7 verifies every box with its artifact.
- Every loop has a hard SAFETY EXIT — when stuck, it asks you instead of spinning.
