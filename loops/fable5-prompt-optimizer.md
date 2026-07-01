# The Fable 5 Prompt Optimizer

> Every substantive prompt you type is silently rewritten into a Fable-5-optimized prompt — intent, definition of done, boundaries — shown back in a 2–5-line block, then executed immediately. A per-turn refine → execute loop.

**Creator:** [keysersoose](https://github.com/keysersoose) · **Category:** Prompt & model optimization · **Source:** distilled from Anthropic's "Prompting Claude Fable 5" guide

## The loop

```
ENTER when: the user submits a substantive prompt in a Claude Fable 5 session
            (skip: short follow-ups like "continue", slash commands, harness payloads,
             prompts that are already precise)

Each iteration (one per user prompt):
  1. Rewrite the raw prompt internally against the checklist below —
     preserve the user's intent exactly; add structure, never new scope.
  2. Show a short "Optimized prompt:" block (2–5 lines) — PROOF of what
     will actually be executed, visible to the user before work starts.
  3. Execute the optimized prompt immediately — no approval step for the rewrite.

CONTINUE while: the session runs on Fable 5 — every new user prompt re-enters the loop
EXIT when: the session ends (each iteration completes within its own turn)
SAFETY EXIT: at most ONE clarifying question, only if the answer materially changes
             execution; pause only for destructive/irreversible actions, real scope
             changes, or input only the user can provide
```

## The refinement checklist

| Axis | Add to the prompt |
|---|---|
| Intent | why + who it's for + what the output enables |
| Done | definition of done + how it will be verified (tests / live check / screenshot); long tasks: self-verify at intervals with fresh-context subagents |
| Boundaries | smallest change; no unrequested refactors, features, or abstractions; validate only at system boundaries |
| Autonomy | act when enough info exists; recommendation, not a survey of options; never end the turn on a promise ("I'll…") |
| Evidence | audit every progress claim against a tool result; report failures faithfully with output |
| Output style | lead with the outcome/TLDR; complete sentences, no arrow-chain shorthand |
| Delegation | independent subtasks → parallel subagents; keep working while they run |

## Ready-to-paste prompt (works anywhere — CLAUDE.md, system prompt, Cursor rules)

```text
Before acting on any substantive user prompt (skip short follow-ups like "continue", slash commands, and prompts that are already precise): silently rewrite it into an optimized prompt that adds (1) intent — why + who it's for + what the output enables; (2) definition of done + how it will be verified (tests, live check, screenshot); (3) boundaries — smallest change, no unrequested refactors or scope; (4) autonomy — act when enough info exists, give a recommendation not a survey, never end the turn on a promise; (5) evidence — audit every progress claim against a tool result; (6) output style — lead with the outcome, complete sentences. Show a short "Optimized prompt:" block (2-5 lines), then execute it immediately with no approval step. Preserve the user's intent exactly — refine form, never add scope. Ask at most ONE clarifying question, and only if the answer materially changes execution.
```

## Auto-trigger install for Claude Code (optional, fires on every prompt)

Three pieces make it automatic — a skill, a `UserPromptSubmit` hook, and one settings entry. Requires Node.js.

**1. Skill** — save the checklist + procedure above as `~/.claude/skills/fable5/SKILL.md` (frontmatter: `name: fable5`, `description: Use when running on Claude Fable 5 and the user's raw prompt needs shaping before execution`).

**2. Hook** — save as `~/.claude/hooks/fable5-optimize.mjs`:

```js
// UserPromptSubmit hook: when the session model is Claude Fable 5, inject an
// instruction to refine the user's raw prompt per the fable5 skill, then execute it.
import { readFileSync } from "node:fs";
import { homedir } from "node:os";
import { join } from "node:path";

function readStdin() {
  try { return readFileSync(0, "utf8"); } catch { return ""; }
}

function currentModel() {
  const settingsPath =
    process.env.FABLE5_SETTINGS || join(homedir(), ".claude", "settings.json");
  try {
    return String(JSON.parse(readFileSync(settingsPath, "utf8")).model || "");
  } catch { return ""; }
}

const ACK_RE =
  /^(y|yes|no|nope|ok(ay)?|k|sure|yep|continue|go( ahead)?|(yes )?do it( end to end)?|proceed|next|stop|cancel|done|thanks?( you)?|try again|retry|resume|why\??|how\??|what\??)[.!]?$/i;

function main() {
  let prompt = "";
  try {
    prompt = String(JSON.parse(readStdin() || "{}").prompt || "").trim();
  } catch { return; } // unparseable input -> stay silent, never block the prompt

  if (!prompt) return;
  if (prompt.startsWith("/")) return; // slash commands
  if (prompt.startsWith("<")) return; // harness payloads (<task-notification>, ...)
  if (prompt.length < 20) return;     // too short to benefit
  if (ACK_RE.test(prompt)) return;    // acks / follow-ups

  if (!/fable/i.test(currentModel())) return; // only steer Fable 5 sessions

  console.log(
    "[fable5] Before acting on the user's prompt above: per the fable5 skill " +
      "(~/.claude/skills/fable5/SKILL.md), silently rewrite it into a Fable-5-optimized prompt — " +
      "intent (why/who for), definition of done + verification, boundaries (smallest change, no unrequested scope), " +
      "autonomy (act when enough info; don't end the turn on a promise), evidence-grounded reporting, " +
      "lead-with-outcome output. Show a short 'Optimized prompt:' block (2-5 lines), then execute it immediately — " +
      "no approval step for the rewrite. If the prompt is conversational, a quick question, or already precise, " +
      "skip refinement and just proceed."
  );
}

main();
```

**3. Settings** — add to the `"hooks"` object in `~/.claude/settings.json`:

```json
"UserPromptSubmit": [
  { "hooks": [ { "type": "command",
      "command": "node \"$HOME/.claude/hooks/fable5-optimize.mjs\"",
      "timeout": 10, "statusMessage": "Shaping prompt for Fable 5..." } ] }
]
```

(Windows: use the full path, e.g. `node "C:\\Users\\<you>\\.claude\\hooks\\fable5-optimize.mjs"`.) Restart Claude Code or open `/hooks` once to reload.

## Notes

- **Proof:** the visible `Optimized prompt:` block — the user sees exactly what the agent decided to execute before any work starts; every later progress claim must trace to a tool result.
- **Memory:** none needed per-turn; the skill file IS the doctrine — edit it and the next prompt picks it up.
- **Why it works / gotchas:** Fable 5's instruction-following is strong enough that one compact, well-shaped instruction beats enumerating behaviors; front-loading intent + done-criteria prevents overplanning and scope drift. Built TDD-style: piped-JSON unit tests for the hook (fires on substantive prompts; silent on acks, slash commands, harness payloads, non-Fable models) plus a fresh-agent behavioral test (refines, shows the block, starts work, asks no permission). Gotcha: don't let the refinement become interrogation — one clarifying question max.
