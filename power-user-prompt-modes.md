# Power-user prompt modes for Claude / Claude Code

A quick reference of reusable "modes" — short labels that expand into a fixed set of instructions, so you can invoke a specific way of thinking without retyping it every time. Use these by pasting the mode's prompt text before your actual question, or save the ones you use most as custom instructions in a Claude Project.

---

### SYSTEMSMODE — think like a systems architect
> "Analyze this as a systems architect. Map out components, data flow, dependencies, and failure points before proposing changes. Call out coupling, single points of failure, and where the design trades simplicity for flexibility."

### STAFFENGINEER — review code as a senior engineer
> "Review this code as a staff engineer would in a pull request. Flag design issues before style issues. Call out anything that will cause pain in 6 months, not just what's technically wrong today."

### PRINCIPALENGINEER — scalability and tradeoffs
> "Evaluate this at the level of a principal engineer setting technical direction. For each major decision, state the tradeoff explicitly — what we gain, what we give up, and under what scale or conditions this choice breaks down."

### SECURITYMODE — find security vulnerabilities
> "Review this as a security engineer doing a threat-focused audit. Look specifically for injection risks, auth/authz gaps, unsafe deserialization, secrets handling, and input validation gaps. Rank findings by severity and exploitability, not just presence."

### PERFORMANCEMODE — optimize speed and memory
> "Review this for performance. Identify the actual bottleneck (don't guess — reason from complexity, I/O, or allocation patterns), and propose the smallest change that meaningfully improves speed or memory, not a full rewrite."

### TESTMODE — generate comprehensive tests
> "Write tests for this covering: happy path, edge cases, invalid input, and failure modes. Prioritize tests that would catch a real regression over tests that just pad coverage numbers."

### REFMODE — refactor for maintainability
> "Refactor this for maintainability only — no behavior changes. Reduce duplication, clarify naming, and simplify control flow. Explain each change in one line so the diff is easy to review."

### AGENTMODE — break work into autonomous tasks
> "Break this goal into a sequence of discrete, independently verifiable tasks an agent could execute one at a time. For each task, state its inputs, its output, and how to verify it succeeded before moving to the next."

### MCPMODE — think in terms of MCP tools
> "Think about this in terms of Model Context Protocol tools: what external data or actions would a tool call need to expose, what's the minimal tool surface, and where would a human need to stay in the loop for confirmation."

### ENTERPRISEMODE — governance, compliance, monitoring, scale
> "Evaluate this for enterprise readiness: governance (who owns this, how is it audited), compliance implications, observability/monitoring, and how it behaves at 10x and 100x current scale."

### REVIEWMODE — review before producing the final answer
> "Before giving your final answer, draft it, then critique your own draft as a skeptical reviewer would — check for gaps, unstated assumptions, and weak reasoning. Then give the revised final answer."

### VERIFYMODE — check facts and identify uncertainty
> "Go through your answer and flag anything you're not fully certain of. Separate what's well-established from what's an inference or best guess, and note where I should double-check independently."

### DOCSMODE — produce high-quality documentation
> "Write this as documentation a new team member could follow with zero prior context. Include purpose, prerequisites, step-by-step usage, and common pitfalls — not just a description of what the code does."

### PROMPTENGINEER — improve prompts before answering
> "Before answering, first rewrite my prompt to be clearer and more specific, show me the improved version, then answer using that improved version."

---

## How to actually use these

**Quick version:** copy the quoted prompt text and paste it right before your question in any Claude chat.

**Better version for Claude Code / repeated use:** save the ones you use often in a `CLAUDE.md` file or as custom instructions in a Claude Project, so you can just type the mode name and Claude already knows what it means for this project.

**Best version:** don't use them as rigid scripts — treat them as a starting frame, then add the specific context of what you're actually working on. "STAFFENGINEER, reviewing this auth middleware for a fintech app" will get you a much sharper review than the generic mode alone.
