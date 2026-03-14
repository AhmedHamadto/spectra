Generate an architecture ownership cheat sheet — everything you need to present this system confidently.

## Target

Ownership cheat sheet for: $ARGUMENTS

If no path is specified, analyse the current working directory.

## Scope

- Skip: node_modules, dist, build, .git, __pycache__, vendor, lock files, binary files, cosmetic config.
- Include: runtime config (auth, CORS, middleware, Docker, CI/CD).
- Read the full codebase to understand the architecture, but only output the Ownership layer.

## Use Case

The user is about to:
- Present this system in a meeting
- Defend their architecture in a PR review
- Explain what they built to a tech lead or investor
- Walk someone through the codebase for the first time

## Output Structure

```
# ⚡ Spectra Ownership Cheat Sheet
```

Then the following sections:

**Elevator pitch**: "This is a [type] built with [stack] that [does what]" — one sentence they can say to anyone. Not jargon-heavy, not a paragraph.

**System diagram**: ASCII/text flow diagram showing how major components connect. Paste-ready for READMEs, slide decks, or PR descriptions.

**Architecture decisions**: Frame every technical choice as a deliberate decision with reasoning. For each major decision: what was chosen, why (as a deliberate choice), trade-off acknowledged. Cover at minimum: database, framework, auth strategy, API design, key libraries.

**How auth works**: Plain-English walkthrough from login to authenticated request. This is the #1 question people get asked.

**How data flows**: Step-by-step walkthrough of the most common user journey. Numbered steps, each one sentence.

**API surface** (if applicable): Concise summary of what endpoints exist and what they do.

**Known limitations**: What the system doesn't do, framed as deliberate scoping decisions. "We chose not to add X yet because Y" shows maturity.

**Questions you'll get asked**: 3-5 likely technical questions with confident, specific answers. ALWAYS include as the final Q&A:
**Q: "What would you change if you rebuilt this?"**
**A:** [2-3 specific, honest improvements framed as forward-looking, not regrets]

## Rules

- NEVER mention AI, AI-generated code, vibe coding, or any AI tool in the output. The entire point is ownership transfer. Say "We chose..." not "Claude chose..."
- Confident but not arrogant. Sound like someone who built the system thoughtfully and knows its strengths and weaknesses.
- Never defensive. Never apologetic.
- Frame limitations as deliberate scoping decisions, not oversights.
