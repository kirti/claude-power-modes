# Power-user prompt modes for Claude & Claude Code

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)
![Made for Claude Code](https://img.shields.io/badge/made%20for-Claude%20Code-D97757)
![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

A small, practical library of reusable "modes" — named instruction sets you invoke by keyword instead of retyping the same context every time you ask Claude to review, refactor, secure, or document your code.

If you're using Claude Code, ChatGPT, or any LLM day-to-day for engineering work, this pattern saves you from writing the same paragraph of instructions over and over, and makes your prompting more consistent across a team.

---

## Demo

> 🎥 *Add a short terminal recording or GIF here showing a mode in action — e.g. typing `SECURITYMODE on src/auth.ts` in Claude Code and the review streaming in.*
>
> Easiest way to make one: record with [asciinema](https://asciinema.org) or [Terminalizer](https://github.com/faressoft/terminalizer) for a terminal GIF, or a quick screen recording converted to GIF with `ffmpeg` or [Gifski](https://gif.ski). Keep it under ~15 seconds — one mode, one clear result.
>
> Once you have the file, drop it in `examples/demo.gif` and replace this block with:
> `![demo](./examples/demo.gif)`

---

## Why this exists

Most developers start by typing free-form requests: *"can you check this for bugs"*, *"clean this up"*, *"is this secure"*. That works, but the results are inconsistent — the model's depth and focus shift depending on how the request happens to be phrased that day.

A **mode** fixes that. It's a short label mapped to a specific, repeatable instruction set, so `SECURITYMODE` always means the same rigorous security pass, whether you invoke it on a Monday or three weeks later.

This is just applied prompt engineering — but naming and saving your prompts turns one-off phrasing into a reusable tool.

---

## The modes

| Mode | Use it when you want to... |
|---|---|
| `SYSTEMSMODE` | Think through architecture, data flow, and failure points |
| `STAFFENGINEER` | Get a senior-level code review, not a style pass |
| `PRINCIPALENGINEER` | Weigh scalability tradeoffs on a big decision |
| `SECURITYMODE` | Find real vulnerabilities, ranked by severity |
| `PERFORMANCEMODE` | Find the actual bottleneck, not guess at one |
| `TESTMODE` | Generate tests that would catch real regressions |
| `REFMODE` | Refactor for maintainability with zero behavior change |
| `AGENTMODE` | Break a goal into verifiable, independent tasks |
| `MCPMODE` | Design around Model Context Protocol tool calls |
| `ENTERPRISEMODE` | Check governance, compliance, monitoring, scale |
| `REVIEWMODE` | Force a self-critique pass before the final answer |
| `VERIFYMODE` | Separate what's certain from what's inferred |
| `DOCSMODE` | Write docs a new hire could follow with no context |
| `PROMPTENGINEER` | Have Claude sharpen your prompt before answering |

Full prompt text for each mode is in [`MODES.md`](#mode-definitions) below — copy what you need.

---

## Quick start

**Option 1 — copy-paste (works anywhere, zero setup)**
Copy a mode's prompt text from the definitions below and paste it directly above your question in any Claude conversation.

```
STAFFENGINEER: review this code as a staff engineer would in a PR.
Flag design issues before style issues.

[paste your code here]
```

**Option 2 — save to `CLAUDE.md` (best for Claude Code)**
Claude Code automatically reads a `CLAUDE.md` file in your repo root for project context. Add your most-used modes there once, and just reference them by name afterward.

```markdown
<!-- CLAUDE.md -->
## Custom review modes

When I say SECURITYMODE, review as a security engineer doing a
threat-focused audit. Look specifically for injection risks,
authz gaps, unsafe deserialization, and input validation gaps.
Rank findings by severity and exploitability.

When I say REFMODE, refactor for maintainability only — no
behavior changes. Reduce duplication, clarify naming, simplify
control flow. Explain each change in one line.
```

Then in a session, just type:
```
SECURITYMODE on src/auth/middleware.ts
```

**Option 3 — Claude Project custom instructions (best for teams)**
If you're using claude.ai, add your team's standard modes to a Project's custom instructions so everyone on the team gets the same review depth and focus, without copy-pasting prompts between people.

---

## Mode definitions

<details>
<summary><strong>SYSTEMSMODE</strong> — think like a systems architect</summary>

```
Analyze this as a systems architect. Map out components, data flow,
dependencies, and failure points before proposing changes. Call out
coupling, single points of failure, and where the design trades
simplicity for flexibility.
```
</details>

<details>
<summary><strong>STAFFENGINEER</strong> — review code as a senior engineer</summary>

```
Review this code as a staff engineer would in a pull request. Flag
design issues before style issues. Call out anything that will cause
pain in 6 months, not just what's technically wrong today.
```
</details>

<details>
<summary><strong>PRINCIPALENGINEER</strong> — focus on scalability and tradeoffs</summary>

```
Evaluate this at the level of a principal engineer setting technical
direction. For each major decision, state the tradeoff explicitly —
what we gain, what we give up, and under what scale or conditions
this choice breaks down.
```
</details>

<details>
<summary><strong>SECURITYMODE</strong> — find security vulnerabilities</summary>

```
Review this as a security engineer doing a threat-focused audit. Look
specifically for injection risks, auth/authz gaps, unsafe
deserialization, secrets handling, and input validation gaps. Rank
findings by severity and exploitability, not just presence.
```
</details>

<details>
<summary><strong>PERFORMANCEMODE</strong> — optimize speed and memory</summary>

```
Review this for performance. Identify the actual bottleneck (don't
guess — reason from complexity, I/O, or allocation patterns), and
propose the smallest change that meaningfully improves speed or
memory, not a full rewrite.
```
</details>

<details>
<summary><strong>TESTMODE</strong> — generate comprehensive tests</summary>

```
Write tests for this covering: happy path, edge cases, invalid
input, and failure modes. Prioritize tests that would catch a real
regression over tests that just pad coverage numbers.
```
</details>

<details>
<summary><strong>REFMODE</strong> — refactor for maintainability</summary>

```
Refactor this for maintainability only — no behavior changes. Reduce
duplication, clarify naming, and simplify control flow. Explain each
change in one line so the diff is easy to review.
```
</details>

<details>
<summary><strong>AGENTMODE</strong> — break work into autonomous tasks</summary>

```
Break this goal into a sequence of discrete, independently verifiable
tasks an agent could execute one at a time. For each task, state its
inputs, its output, and how to verify it succeeded before moving to
the next.
```
</details>

<details>
<summary><strong>MCPMODE</strong> — think in terms of Model Context Protocol tools</summary>

```
Think about this in terms of Model Context Protocol tools: what
external data or actions would a tool call need to expose, what's
the minimal tool surface, and where would a human need to stay in
the loop for confirmation.
```
</details>

<details>
<summary><strong>ENTERPRISEMODE</strong> — governance, compliance, monitoring, scale</summary>

```
Evaluate this for enterprise readiness: governance (who owns this,
how is it audited), compliance implications, observability/
monitoring, and how it behaves at 10x and 100x current scale.
```
</details>

<details>
<summary><strong>REVIEWMODE</strong> — review before producing the final answer</summary>

```
Before giving your final answer, draft it, then critique your own
draft as a skeptical reviewer would — check for gaps, unstated
assumptions, and weak reasoning. Then give the revised final answer.
```
</details>

<details>
<summary><strong>VERIFYMODE</strong> — check facts and identify uncertainty</summary>

```
Go through your answer and flag anything you're not fully certain
of. Separate what's well-established from what's an inference or
best guess, and note where I should double-check independently.
```
</details>

<details>
<summary><strong>DOCSMODE</strong> — produce high-quality documentation</summary>

```
Write this as documentation a new team member could follow with zero
prior context. Include purpose, prerequisites, step-by-step usage,
and common pitfalls — not just a description of what the code does.
```
</details>

<details>
<summary><strong>PROMPTENGINEER</strong> — improve prompts before answering</summary>

```
Before answering, first rewrite my prompt to be clearer and more
specific, show me the improved version, then answer using that
improved version.
```
</details>

---

## Tips for developers

- **Stack modes when useful.** `SECURITYMODE` + `REVIEWMODE` on the same request gets you a security audit that's also self-checked before you see it.
- **Add context, don't rely on the label alone.** `STAFFENGINEER` reviewing generic code is fine; `STAFFENGINEER, this is auth middleware for a fintech app handling PII` gets a sharper, more relevant review.
- **Keep `CLAUDE.md` modes short.** Long, over-specified instructions dilute focus — one clear paragraph per mode is enough.
- **Version your modes with your repo.** Since `CLAUDE.md` is just a file, it gets code-reviewed and improved over time like anything else — treat mode definitions as living documentation, not a one-time setup.
- **These aren't magic words.** A mode is a compressed instruction, not a special model capability — you'll get the same quality of result as if you'd typed the full instruction out each time. The value is consistency and speed, not new capability.

---

## Examples

See `/examples` for real before/after transcripts:
- [`securitymode-example.md`](./examples/securitymode-example.md) — a login route with SQL injection, plaintext passwords, and a hardcoded JWT secret, caught and ranked by severity
- [`refmode-example.md`](./examples/refmode-example.md) — a tangled function cleaned up with zero behavior change
- [`testmode-example.md`](./examples/testmode-example.md) — a small utility function given happy-path, edge-case, and failure-mode test coverage

## Machine-readable version

All modes are also available as structured JSON in [`modes.json`](./modes.json) — useful if you want to build a CLI, VS Code extension, or Claude Code plugin on top of this list rather than copy-pasting from markdown.

## Contributing

Got a mode that's useful for your team's workflow? Add it to this file following the same format: name, one-line description, and a copy-pasteable instruction block.
