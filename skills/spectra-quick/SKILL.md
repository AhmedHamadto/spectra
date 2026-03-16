---
name: spectra-quick
description: Run a quick Spectra briefing — Blueprint and Trust only. A 2-minute read.
---

Run a quick Spectra briefing — Blueprint and Trust only. A 2-minute read.

## Target

Quick briefing: $ARGUMENTS

If no path is specified, analyse the current working directory.

## Scope

- Maximum 25 files. If more exist, pick highest-impact: entry points, auth, data layer, API routes.
- Skip: node_modules, dist, build, .git, __pycache__, vendor, lock files, binary files, cosmetic config.
- Include: runtime config (auth, CORS, middleware, Docker, CI/CD).
- Only flag critical and high-severity trust issues.

## Output Structure

```
# ⚡ Spectra Quick Briefing

**Confidence:** Blueprint: ✅/⚠️ | Trust: 🟢/🟡/🔴 (N issues)
```

Then two sections only.

---

## Layer 1: Blueprint — "What did your AI build?"

Keep it to 2-3 tight paragraphs plus a system diagram.

**Start with an ASCII/text flow diagram** showing how major components connect.

Then cover in narrative: what the app does (one sentence), tech stack, architecture shape, how data flows, the 3-5 most important files, auth model (if applicable).

Write like you're explaining to a colleague. Clear, not clever.

---

## Layer 2: Trust — "Can you ship this?"

Assess across: security posture, error resilience, data integrity, scalability signals, deployment readiness.

Rate: 🟢 **Ship it** / 🟡 **Fix first** / 🔴 **Not ready**

For 🟡 and 🔴, present critical/high fixes only as a priority table:

| Priority | Issue | Fix | Effort |
|----------|-------|-----|--------|
| P0 | [critical] | [specific fix] | [e.g., 5 min] |
| P1 | [high] | [specific fix] | [e.g., 2 hours] |

Effort must be specific. Skip medium/low/info findings.

---

End with: *For the full four-layer briefing including Alignment and Ownership, run `/spectra`.*

## Rules

- NEVER mention AI or AI-generated code in the output.
- Be honest in Trust. Don't soften bad news.
- Verify each finding by re-reading the code in context before reporting.
