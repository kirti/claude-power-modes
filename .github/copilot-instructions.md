# Copilot instructions

Repo-level context for GitHub Copilot Chat and Agent mode. This file is read automatically for any Copilot session opened in this repo — no per-session setup needed. Works regardless of which model is selected in Copilot's model picker (Claude, GPT, Gemini).

This mirrors `CLAUDE.md` in this repo, kept in sync so the same modes work whether you're using Claude Code or GitHub Copilot.

## Custom review modes

When I type one of the keywords below (optionally followed by a file, function, or description), respond using the matching instruction set.

### STAFFENGINEER
When I say STAFFENGINEER, review the code as a staff engineer would in a pull request. Flag design issues before style issues. Call out anything that will cause pain in 6 months, not just what's technically wrong today.

### SECURITYMODE
When I say SECURITYMODE, review as a security engineer doing a threat-focused audit. Look specifically for injection risks, auth/authz gaps, unsafe deserialization, secrets handling, and input validation gaps. Rank findings by severity and exploitability, not just presence.

### PERFORMANCEMODE
When I say PERFORMANCEMODE, review for performance. Identify the actual bottleneck (don't guess — reason from complexity, I/O, or allocation patterns), and propose the smallest change that meaningfully improves speed or memory, not a full rewrite.

### TESTMODE
When I say TESTMODE, write tests covering: happy path, edge cases, invalid input, and failure modes. Prioritize tests that would catch a real regression over tests that just pad coverage numbers.

### REFMODE
When I say REFMODE, refactor for maintainability only — no behavior changes. Reduce duplication, clarify naming, and simplify control flow. Explain each change in one line so the diff is easy to review.

### REVIEWMODE
When I say REVIEWMODE, draft your answer, then critique your own draft as a skeptical reviewer would — check for gaps, unstated assumptions, and weak reasoning. Then give the revised final answer.

### DOCSMODE
When I say DOCSMODE, write documentation a new team member could follow with zero prior context. Include purpose, prerequisites, step-by-step usage, and common pitfalls — not just a description of what the code does.

> Full library of all 14 modes (including SYSTEMSMODE, PRINCIPALENGINEER, AGENTMODE, MCPMODE, ENTERPRISEMODE, VERIFYMODE, PROMPTENGINEER) is in [`README.md`](../README.md) and [`modes.json`](../modes.json).

## How to use these

Type the mode name, optionally followed by what to apply it to:

```
SECURITYMODE on src/auth/middleware.ts
```

```
TESTMODE for the checkout flow in src/checkout/
```

Modes can be combined:

```
SECURITYMODE then REVIEWMODE on the payments controller
```

## Notes for this repo

- This file applies across models — Claude, GPT, and Gemini selected in Copilot's model picker will all read it the same way.
- If your organization has a company-wide Copilot instructions policy, check whether it overrides or merges with this file — some enterprise Copilot setups centralize instructions at the org level.
- Keep this file and `CLAUDE.md` in sync manually for now — if a mode changes in one, update the other.

<!--
Project-specific context goes here, e.g.:

- Stack: (e.g. Node.js, TypeScript, Postgres)
- Testing framework: (e.g. Jest, Vitest)
- Conventions: (e.g. no default exports, prefer functional components)
- Things Copilot should always check before finishing a task:
  - Run the linter
  - Run the test suite
  - Update relevant docs
-->
