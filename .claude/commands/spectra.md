Run a full Spectra briefing — four layers that help you understand, verify, and own an AI-generated codebase.

## Target

Analyse: $ARGUMENTS

If no path is specified, analyse the current working directory.

## Scope

- Skip: node_modules, dist, build, .git, __pycache__, vendor, lock files, binary files, generated files, cosmetic config (ESLint, Prettier, editor settings).
- DO include: config files that affect runtime behaviour (auth, CORS, middleware, Docker, CI/CD, environment config).
- If more than 50 source files exist, inform the user and suggest narrowing scope before proceeding.
- For very large files (>500 lines), prioritise the most architecturally significant sections.
- Depth over breadth. Understanding 15 files deeply beats skimming 150.

## Handling Specs

If the user provides their original spec or prompt (e.g., "I asked Claude to build a task management API with auth"), use it for Layer 2 (Alignment). If no spec is provided, infer intent from README files, comments, package.json description, or the codebase structure itself — and note that alignment is based on inference, not an explicit spec.

## Output Structure

Start with:

```
# ⚡ Spectra Briefing

**Confidence:** Blueprint: ✅/⚠️ | Alignment: ✅/⚠️ | Trust: 🟢/🟡/🔴 (N issues) | Ownership: ✅/⚠️
```

Then each layer as its own ## section. Walk through all four layers in order. Do not skip layers. Do not combine them.

---

## Layer 1: Blueprint — "What did your AI build?"

Produce a plain-English architecture summary that a junior developer can read once and explain to someone else.

**Start with a system diagram.** Before the narrative, create an ASCII/text flow diagram showing how the major components connect. Simple boxes and arrows — not UML.

Then cover in narrative form (not bullet lists):
- What the app does in one sentence
- Tech stack: languages, frameworks, databases, external services
- Architecture shape: monolith, API + frontend, microservices, serverless, etc.
- Data flow: how does a request enter, what happens, where does data live
- Key components: the 3-5 most important files/modules and what role each plays
- Entry points: where the app starts, what routes/endpoints exist
- Auth model: how users are identified and what's protected (if applicable)
- External dependencies: what third-party services it talks to

Write like you're explaining the system to a smart colleague joining tomorrow. They know how to code but they've never seen this codebase.

---

## Layer 2: Alignment — "Does it match what you asked for?"

Compare what was built against what the user intended. Output as SEPARATE subsections with ### headers.

### Faithful Implementations
Things the spec asked for that were built correctly. Be specific.

### Silent Decisions
Things the AI decided without being asked. This MUST be its own clearly separated section. For EACH silent decision, use this exact format:
- **What was chosen**: e.g., "PostgreSQL with Prisma ORM"
- **What alternatives existed**: e.g., "MongoDB, SQLite, raw SQL, Drizzle"
- **Whether it's reasonable**: e.g., "Reasonable — relational data, type safety, migrations"
- **When it might be wrong**: e.g., "If you need flexible schemas or document storage"

Common silent decisions to look for: database/ORM choice, auth strategy, framework selection, folder structure, error handling strategy, API design patterns, middleware stack, logging approach, environment/config management.

### Gaps
Things the spec asked for that aren't implemented. Classify each as: missing entirely, partially implemented, or stubbed out.

### Extras
Things built but never requested: premature abstractions, unrequested features, over-engineered infrastructure.

### Misinterpretations
Things built that don't match the intent. If none, omit this section.

---

## Layer 3: Trust — "Can you ship this?"

Evaluate production readiness across five dimensions. This is a readiness assessment, not a bug hunt.

**Security posture**: Secrets hardcoded? Auth actually protecting things? Inputs validated? Users accessing things they shouldn't?

**Error resilience**: What happens when things go wrong? Crash, hang, or degrade gracefully? Errors caught or silently swallowed?

**Data integrity**: Database operations safe? Could you lose data on crash? Race conditions on concurrent access?

**Scalability signals**: Works for 10 users? 100? 1,000? Where does it break first?

**Deployment readiness**: Env vars for config? No hardcoded localhost? Logging present? Health checks? Can someone clone and run this?

Rate overall:
- 🟢 **Ship it** — Production ready for its intended scale
- 🟡 **Fix first** — Works but has specific issues
- 🔴 **Not ready** — Fundamental issues

For 🟡 and 🔴, present fixes as a priority table:

| Priority | Issue | Fix | Effort |
|----------|-------|-----|--------|
| P0 | [critical] | [specific fix] | [e.g., 5 min] |
| P1 | [high] | [specific fix] | [e.g., 2 hours] |

Effort MUST be specific: "5 min", "30 min", "2 hours", "half day". Never vague.

---

## Layer 4: Ownership — "How to talk about this"

Generate an architecture cheat sheet that prepares the user to present this system confidently.

**Elevator pitch**: "This is a [type] built with [stack] that [does what]" — one sentence.

**System diagram**: Reproduce/refine the ASCII diagram from Blueprint. This is paste-ready for READMEs, slide decks, or PR descriptions.

**Architecture decisions**: Frame every technical choice as a deliberate decision. For each: what was chosen, why (frame as deliberate), trade-off acknowledged. Cover at minimum: database, framework, auth strategy, API design, key libraries.

**How auth works**: Plain-English walkthrough of the auth flow from login to authenticated request.

**How data flows**: Step-by-step walkthrough of the most common user journey.

**API surface** (if applicable): Concise summary of endpoints.

**Known limitations**: What the system doesn't do, framed as deliberate scoping decisions. Shows technical maturity.

**Questions you'll get asked**: 3-5 likely technical questions with confident answers. ALWAYS include as the final Q&A:
**Q: "What would you change if you rebuilt this?"**
**A:** [2-3 specific, honest improvements framed as forward-looking, not regrets]

## Rules

- Write for a junior developer. Clear beats clever.
- NEVER mention AI, AI-generated code, vibe coding, or any AI tool in the output. Frame everything as if the user made the decisions. Layer 4 is ownership transfer.
- Be honest in Trust. "This will lose data on concurrent writes" beats "consider improving data handling."
- Silent decisions are not criticisms. Frame neutrally.
- If the codebase is genuinely well-built, say so. Not every briefing needs problems.
- After generating Trust findings, verify each one by re-reading the code in context. Remove anything that doesn't hold up.
