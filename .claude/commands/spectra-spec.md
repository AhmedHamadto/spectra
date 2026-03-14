Run a deep Alignment analysis — compare your original spec against what was actually built.

## Target

Spec alignment for: $ARGUMENTS

If no path is specified, analyse the current working directory.

## Spec Input

The user MUST provide their original spec or prompt. If they haven't, ask for it before proceeding. The spec can be:
- Pasted after running the command
- Provided inline: `/spectra-spec ./src I asked for a task API with auth and email notifications`
- A file path to a spec document

## Scope

- Skip: node_modules, dist, build, .git, __pycache__, vendor, lock files, binary files, cosmetic config.
- Include: runtime config that affects behaviour.
- Read the full codebase to understand what was built.

## Output Structure

```
# ⚡ Spectra Spec Alignment

**Spec Coverage:** X% of requirements fully implemented
```

Then a deep analysis in these sections:

### Faithful Implementations
Line-by-line mapping of spec requirements to implementations. For each requirement: what was asked → where it's implemented → assessment (complete/partial/missing).

### Silent Decisions
Every decision the AI made that wasn't in the spec. For EACH:
- **What was chosen**: e.g., "Express over Fastify"
- **What alternatives existed**: e.g., "Fastify, Hono, Koa"
- **Whether it's reasonable**: e.g., "Reasonable — largest ecosystem, most middleware"
- **When it might be wrong**: e.g., "If you need >50K req/sec, Fastify would be faster"

Be exhaustive. Check: database, ORM, auth strategy, framework, folder structure, error handling, API patterns, middleware, logging, config management, testing framework, validation library, deployment config.

### Gaps
Every spec requirement that isn't fully implemented. Classify each as:
- **Missing entirely**: no trace in the codebase
- **Partially implemented**: some code exists but it's incomplete
- **Stubbed out**: placeholder code, TODO comments, empty functions

### Extras
Everything built that wasn't in the spec. Classify each as:
- **Useful addition**: genuinely helpful, worth keeping
- **Premature optimisation**: not needed at current scale
- **Unnecessary complexity**: adds maintenance burden without current value

### Misinterpretations
Things built that don't match the spec's intent. For each: what was asked → what was built → how they differ.

### Spec Coverage Score
Calculate: (fully implemented requirements / total requirements) × 100%
List each requirement as ✅ implemented, ⚠️ partial, or ❌ missing.

## Rules

- NEVER mention AI or AI-generated code in the output.
- Be precise. "Email notifications: not implemented" is better than "some features may be missing."
- Silent decisions are not criticisms. Frame neutrally.
- If everything matches the spec, say so clearly.
