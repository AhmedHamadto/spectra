# Contributing to Spectra

Thanks for your interest in improving Spectra. The most impactful contributions right now come from real-world usage — telling us what worked, what didn't, and what was missing.

## How To Contribute

### Report a usage experience

Run Spectra on a real project and tell us what happened:
- Did the Blueprint accurately describe your system?
- Did the Alignment layer catch silent decisions you weren't aware of?
- Was the Trust rating fair and actionable?
- Could you use the Ownership output to present your system confidently?

Open an issue using the **Usage Report** template.

### Improve a layer prompt

Each command file in `.claude/commands/` contains the full instructions for its layers. If you find that a layer consistently misses something or produces unhelpful output, suggest a prompt improvement.

When suggesting changes:
- Describe the problem (what the current output looks like)
- Show what you expected instead
- Propose specific wording changes to the prompt

Open an issue using the **Prompt Improvement** template or submit a PR directly.

### Add stack-specific guidance

The "Questions you'll get asked" section in the Ownership layer benefits from stack-specific knowledge. If you use a particular tech stack frequently, contribute common questions and confident answers for that stack.

Examples: Next.js + Prisma, Django + PostgreSQL, FastAPI + SQLAlchemy, Rails, Laravel, Go + Chi, etc.

Open a PR adding a section to the relevant command file, or open an issue describing what you'd add.

### Report a broken briefing

If Spectra produces output that's factually wrong (misidentified framework, incorrect architecture description, false security finding), open an issue with:
- The command you ran
- The relevant parts of the output that were wrong
- What the correct output should be
- If possible, a description of your codebase structure

## Guidelines

- Keep PRs focused. One improvement per PR.
- Test changes on at least one real codebase before submitting.
- Prompt engineering is subtle — small wording changes can have large effects. Explain your reasoning.
- Be kind. We're all figuring this out.

## Code of Conduct

This project follows the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.
