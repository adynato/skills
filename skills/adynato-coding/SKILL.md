---
name: adynato-coding
description: General coding conventions for any repository. Covers writing for the human who owns the code, clear naming, clean structure, comments that explain why, and following existing linting and formatting rules. Use when writing or modifying code in any language, especially for refactors, utilities, tests, and business logic. Prefer this as baseline guidance unless a more specific skill applies.
---

# Coding Skill

Use this skill as the default baseline when writing or changing code in any project.

## Write for the Human Owner

Assume the human using the AI is responsible for the code after you leave.
They must be able to read it, review it, debug it, and safely change it later.

Optimize for readability before cleverness. If a shorter solution is harder to understand, do not use it.

## Keep Code Clean

- Prefer straightforward control flow over dense expressions
- Keep functions focused on one job at one level of abstraction
- Prefer improving existing code over adding wrappers that preserve confusing structure
- Remove dead branches, stale helpers, and duplicated patterns when touching an area
- Avoid speculative abstractions and premature generalization
- If the same pattern appears twice, extract a shared helper or shared type

## Name Things Clearly

Names should tell the reader what something is and why it exists.

- Prefer explicit names over short or clever names
- Avoid unexplained abbreviations unless they are already standard in the project or domain
- Use short names only in tight local scopes where the meaning is obvious
- Use descriptive names for exported values, public APIs, and cross-file concepts
- Follow the language and project naming conventions already in use

## Follow Project Conventions

- Match the repository's existing style, architecture, and file organization unless the task is to refactor them
- Improve code structure inside the area you touch; do not preserve confusing code just for consistency
- Avoid unnecessary file or module reshuffling when the real fix is local cleanup
- Treat the project's formatter, linter, and type checker as the source of truth for uniformity
- When lint or formatting rules disagree with local preference, follow the repo
- If a collaborative project appears to lack linting or formatting, suggest adding it instead of relying on personal taste

## Comment for Intent

- Use comments to explain intent, invariants, tradeoffs, and non-obvious behavior
- Do not restate what clear code already says
- Prefer better names and smaller functions before adding comments

## Review Before You Stop

Before finishing, read the result as a teammate would:

- Leave the touched code simpler than you found it
- Rename anything unclear
- Remove leftover debugging code, commented-out code, and stale TODOs
- Make sure touched files conform to existing lint and format rules
- Call out missing linting or formatting setup when the repository would benefit from it
