<p align="center">
  <h1 align="center">Spectra</h1>
  <p align="center">
    <strong>See your AI-built codebase from every angle.</strong>
  </p>
  <p align="center">
    <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License"></a>
    <a href="https://docs.anthropic.com/en/docs/claude-code/overview"><img src="https://img.shields.io/badge/built%20for-Claude%20Code-7C3AED" alt="Claude Code"></a>
    <a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome"></a>
  </p>
</p>

Unlike code reviewers that find bugs or linters that enforce style, Spectra gives you the confidence to ship AI-built code and speak to it like you built it yourself.

## Quick Start

```bash
# Install globally (30 seconds)
git clone https://github.com/ahmedhamadto/spectra.git
mkdir -p ~/.claude/commands
cp -r spectra/.claude/commands/ ~/.claude/commands/

# Run it
/spectra ./src
```

That's it. No dependencies, no API keys, no config.

## The Problem

AI coding tools let you build fast. But they leave you with a codebase you don't fully understand, full of decisions you didn't make, with no way to know if it's production-ready or held together with duct tape.

You can't confidently:
- Explain how the auth system works
- Answer "why did you use PostgreSQL instead of MongoDB?"
- Know if your API is accidentally exposing user data
- Tell your tech lead what would break if traffic doubled

Spectra fixes this.

## The Four Layers

```
/spectra  ->  Blueprint  ->  Alignment  ->  Trust  ->  Ownership
                  |              |            |            |
                  v              v            v            v
              What was       Spec vs      Can you      How to
               built?       reality?     ship it?    talk about it?
```

| Layer | Question | What you get |
|-------|----------|-------------|
| **Blueprint** | What did the AI build? | Plain-English architecture summary with system diagram |
| **Alignment** | Does it match what you asked for? | Every silent decision surfaced with alternatives |
| **Trust** | Can you ship this? | Production readiness rated across 5 dimensions |
| **Ownership** | How do you talk about this? | Architecture cheat sheet for meetings and PRs |

## Install

### Per-project (recommended)

```bash
git clone https://github.com/ahmedhamadto/spectra.git

mkdir -p your-project/.claude/commands
cp -r spectra/.claude/commands/ your-project/.claude/commands/
```

### Global (all projects)

```bash
git clone https://github.com/ahmedhamadto/spectra.git

mkdir -p ~/.claude/commands
cp -r spectra/.claude/commands/ ~/.claude/commands/
```

### Verify

Start a new Claude Code session, then type `/spectra` — you should see it in autocomplete.

## Usage

| Command | What it does | When to use |
|---------|-------------|-------------|
| `/spectra [path]` | Full four-layer briefing | Before shipping, during PR review, onboarding to your own code |
| `/spectra-quick [path]` | Blueprint + Trust only | Quick sanity check mid-development |
| `/spectra-own [path]` | Ownership cheat sheet | Preparing for a meeting, interview, or presentation |
| `/spectra-spec [path]` | Deep spec vs reality comparison | After a vibe-coding session to check what was actually built |

### With your original spec

The Alignment layer is most powerful when you provide your original prompt:

```bash
/spectra-spec ./src
# Then paste: "I asked Claude to build a task management API with JWT auth,
# PostgreSQL, and email notifications"
```

This gives you a line-by-line comparison of what was asked for vs what exists, with a coverage score.

## Example Output

<details>
<summary><strong>Click to expand a full Spectra briefing</strong></summary>

```
# Spectra Briefing

**Confidence:** Blueprint: fully mapped | Alignment: inferred | Trust: Fix first (3 issues) | Ownership: ready

## Blueprint — What Was Built

    User Browser -> React SPA (Vercel)
                      |
                  Express API (Railway)
                      |-- PostgreSQL (Supabase)
                      +-- Stripe (payments)

This is a task management API built with Express and PostgreSQL. When a
request comes in, Express routes it through auth middleware (JWT-based),
then to the appropriate handler...

## Alignment — Spec vs Reality

### Faithful Implementations
Task CRUD, JWT auth, team management — all implemented as specified.

### Silent Decisions
**Database: PostgreSQL with Prisma ORM**
Alternatives: MongoDB, SQLite, raw SQL, Drizzle
Reasonable: Yes — relational data, type safety, migrations
Might be wrong if: You need flexible schemas or document storage

### Gaps
Email notifications: not implemented. No email service configured.

## Trust — Can You Ship This?

**Overall: Fix First**

| Priority | Issue | Fix | Effort |
|----------|-------|-----|--------|
| P0 | JWT tokens never expire | Add expiresIn: '24h' to jwt.sign() | 5 min |
| P1 | No input validation on /api/tasks | Add Zod schema validation | 30 min |
| P2 | No rate limiting | Add express-rate-limit middleware | 15 min |

## Ownership — How To Talk About This

**Elevator pitch:** "A REST API for team task management built with
Express and PostgreSQL, with JWT auth and role-based permissions."

**Q: What would you change if you rebuilt this?**
A: Move to Fastify for better performance defaults, add Redis
for session caching, and use a proper job queue instead of
setTimeout for async notifications.
```

</details>

## How It Works

Spectra is a set of self-contained [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) slash commands. No external services, no API keys, no dependencies, no data leaving your machine. Each command contains all the instructions needed — just copy the `.claude/commands/` directory and go.

```
spectra/
├── .claude/commands/
│   ├── spectra.md         <- /spectra (full four-layer briefing)
│   ├── spectra-quick.md   <- /spectra-quick (blueprint + trust)
│   ├── spectra-own.md     <- /spectra-own (ownership cheat sheet)
│   └── spectra-spec.md    <- /spectra-spec (deep spec alignment)
├── .github/ISSUE_TEMPLATE/
│   ├── bug-report.md
│   ├── prompt-improvement.md
│   └── usage-report.md
├── .editorconfig
├── .gitignore
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines. The most valuable contributions are:
- Real-world usage reports (what worked, what didn't, what was missing)
- Improvements to layer prompts based on testing
- Stack-specific "Questions you'll get asked" additions
- Translations for non-English developer audiences

## License

[MIT](LICENSE) — use it however you want.
