# CLAUDE.md

Project context and custom instructions for Claude Code.

## Custom review modes

These are shorthand modes you can invoke by name during a session. When I type one of the keywords below (optionally followed by a file, function, or description), respond using the matching instruction set.

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

> Want more modes (SYSTEMSMODE, PRINCIPALENGINEER, AGENTMODE, MCPMODE, ENTERPRISEMODE, VERIFYMODE, PROMPTENGINEER)? See the full library and copy-pasteable definitions in [`README.md`](./README.md).

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

## Project context

<!--
Fill this section in with details specific to your repo, e.g.:

- Stack: (e.g. Node.js, TypeScript, Postgres)
- Testing framework: (e.g. Jest, Vitest)
- Conventions: (e.g. no default exports, prefer functional components)
- Things Claude should always check before finishing a task:
  - Run the linter
  - Run the test suite
  - Update relevant docs
-->
