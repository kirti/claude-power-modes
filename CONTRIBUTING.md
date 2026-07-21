# Contributing

Thanks for considering adding a mode. This repo stays useful only if new modes are as clear and reusable as the originals — here's how to submit one.

## Before you open a PR

Check the existing modes in `README.md` first. If your idea overlaps closely with one that already exists (e.g. a second security-focused mode), consider whether it should be a variant note under the existing mode instead of a new one.

## Format for a new mode

Every mode needs three things:

1. **A name** — one word, uppercase, ideally ending in `MODE` or a clear role name (e.g. `SECURITYMODE`, `STAFFENGINEER`). Keep it short enough to type quickly in a real session.
2. **A one-line description** — what it's for, in plain language. This goes in the summary table at the top of the README.
3. **An instruction block** — the actual prompt text, written as a direct instruction to Claude. Keep it to 2-4 sentences. Be specific about what the mode should prioritize or look for, not just a vague restatement of the name.

### Template

Add your mode to `README.md` under "Mode definitions," following this exact structure:

```markdown
<details>
<summary><strong>YOURMODE</strong> — one-line description</summary>

​```
Direct instruction text goes here. Be specific about what to prioritize,
what to look for, or what output format to use. 2-4 sentences.
​```
</details>
```

Also add a row to the summary table near the top:

```markdown
| `YOURMODE` | One-line description of when to use it |
```

## What makes a good mode

- **Specific over generic.** "Look for injection risks, authz gaps, and unsafe deserialization" is more useful than "check for security issues."
- **Prioritizes something.** Good modes tell Claude what to focus on first, not just what topic to think about.
- **Reusable across projects.** A mode should work whether it's applied to a Python script or a React component — avoid baking in assumptions about a specific stack.
- **Actually different from existing modes.** If your mode produces roughly the same output as `STAFFENGINEER` or `REVIEWMODE`, it's probably not adding value as a separate entry.

## Testing your mode before submitting

Try it on 2-3 different real pieces of code or requests before opening a PR. If the output feels inconsistent or too vague across different inputs, tighten the instruction text.

## Opening the PR

- One mode per PR, unless you're submitting a small closely-related set (e.g. a family of modes for a specific domain).
- In the PR description, include a short example of the mode's output on a real (or realistic) input, so reviewers can judge quality quickly.
- Be open to edits — mode wording often gets sharper through review, the same way a good prompt does through iteration.
