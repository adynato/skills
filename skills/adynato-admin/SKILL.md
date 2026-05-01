---
name: adynato-admin
description: Admin and operations work standards for forms, data entry, document drafting, setup tasks, CRM/admin consoles, and building features or content that require factual details. Use when completing admin work, filling fields, configuring systems, creating records, writing operational copy, or building anything that depends on private, account-specific, customer-specific, or otherwise unavailable facts; ask for missing information instead of inventing placeholders.
---

# Adynato Admin

Use this skill when a task requires factual inputs that may not be present in the conversation or accessible files/tools.

## Missing Facts

- Treat factual gaps as blockers, not blank spaces to decorate.
- Ask the user for specific missing information before completing a field, record, configuration, document, or build output that depends on it.
- Do not invent names, addresses, dates, prices, account IDs, policies, URLs, emails, customer details, credentials, analytics, legal terms, financial terms, or business rules.
- Do not use placeholders such as `TBD`, `TODO`, `example.com`, lorem ipsum, fake people, fake emails, or dummy IDs in final work unless the user explicitly requests a template/scaffold or approves placeholders.
- If the user asks for a scaffold or template, make placeholder status explicit and use obvious bracketed labels like `[company legal name]`.

## Before Asking

- Search the provided repo, files, docs, issue/thread, and connected tools that are already in scope.
- If the fact is public and the task permits browsing, verify it from a reliable source instead of asking.
- If the fact is private, account-specific, current credentials, or unavailable behind auth, ask the user.

## Asking for Data

- Ask concise, enumerated questions only for the facts needed to proceed.
- Group related fields into a short checklist the user can fill in.
- Explain which output is blocked by the missing facts.
- Continue with parts of the task that do not depend on unknown facts.

## Admin Output

- Prefer a "needs input" status over silent guesses.
- If partial output is useful, mark unknown fields as missing outside the deliverable or in a clearly labeled draft section.
- Before finalizing admin records, emails, contracts, settings, landing pages, or customer-facing copy, verify that all factual claims came from provided context, accessible sources, or explicit user confirmation.
