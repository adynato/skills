# Adynato Skills

A collection of AI agent skills for Adynato projects, following the [Agent Skills](https://agentskills.io/) specification.

## Installation

```bash
# Install all skills
npx add-skill adynato/skills

# Install specific skills
npx add-skill adynato/skills --skill adynato-seo --skill adynato-web

# Install globally (available across all projects)
npx add-skill adynato/skills -g

# Install to specific agents
npx add-skill adynato/skills -a claude-code -a cursor
```

## Available Skills

| Skill | Description |
|-------|-------------|
| **adynato-seo** | SEO requirements including LD+JSON schema.org, backlinks, further reading sections, meta tags, and Open Graph |
| **adynato-web** | Web development conventions, image optimization with img4web, component patterns, and styling |
| **adynato-mobile** | Mobile app development with React Native and Expo - navigation, native APIs, performance |
| **adynato-web-api** | Web API patterns for Next.js - route handlers, validation, auth, error handling |
| **adynato-mobile-api** | API integration for mobile apps - TanStack Query, auth flows, offline support |
| **adynato-github** | GitHub workflow using gh CLI - thorough PR descriptions, stacked PRs for large deliverables |
| **adynato-vercel** | Vercel deployment and configuration - env vars, vercel.json, common errors, CI/CD setup |
| **adynato-cloudflare** | Cloudflare Workers/Pages deployment - wrangler CLI, reading logs, KV/D1/R2, debugging |

## Usage

Skills activate automatically when your AI agent detects relevant tasks. No explicit invocation needed.

**Trigger phrases:**
- "Add an image to the hero section" → activates **adynato-web** skill (img4web guidance)
- "Create a blog post" → activates **adynato-seo** skill (LD+JSON, backlinks, further reading)
- "Build a new API endpoint" → activates **adynato-web-api** skill
- "Fetch data from the API" → activates **adynato-mobile-api** skill
- "Add a new screen to the app" → activates **adynato-mobile** skill
- "Create a PR for this feature" → activates **adynato-github** skill (stacked PRs, descriptions)
- "Deploy to Vercel" → activates **adynato-vercel** skill (env vars, errors, CI/CD)
- "Debug this Cloudflare Worker" → activates **adynato-cloudflare** skill (wrangler tail, logs)

## Skill Structure

```
skills/
├── adynato-seo/
│   ├── SKILL.md
│   └── references/
│       └── SCHEMAS.md      # LD+JSON templates
├── adynato-web/
│   └── SKILL.md
├── adynato-mobile/
│   └── SKILL.md
├── adynato-web-api/
│   └── SKILL.md
├── adynato-mobile-api/
│   └── SKILL.md
├── adynato-github/
│   └── SKILL.md
├── adynato-vercel/
│   └── SKILL.md
└── adynato-cloudflare/
    └── SKILL.md
```

---

## Recommended Third-Party Skills

We recommend also installing these skills from the community:

### Vercel

```bash
npx add-skill vercel-labs/agent-skills
```

| Skill | Description |
|-------|-------------|
| **react-best-practices** | 40+ performance optimization rules for React and Next.js |
| **frontend-design** | 100+ UI code audit rules for accessibility, performance, and UX |

[View on GitHub](https://github.com/vercel-labs/agent-skills)

### Expo

```bash
npx add-skill expo/skills
```

Skills for building, deploying, and debugging Expo apps. Fine-tuned for Claude but works with any AI agent.

[View on GitHub](https://github.com/expo/skills)

### Anthropic (Official Examples)

```bash
npx add-skill anthropics/skills
```

Official example skills from the creators of the Agent Skills specification.

[View on GitHub](https://github.com/anthropics/skills)

---

## Supported Agents

These skills work with:

- Claude Code
- Cursor
- Codex
- OpenCode
- Windsurf
- Gemini CLI
- GitHub Copilot
- And more...

## Contributing

1. Create a new directory in `skills/` with `adynato-` prefix
2. Add a `SKILL.md` with required frontmatter (`name`, `description`)
3. Optionally add `scripts/`, `references/`, or `assets/` directories
4. Submit a pull request

See the [Agent Skills Specification](https://agentskills.io/specification) for full format details.

## License

MIT
