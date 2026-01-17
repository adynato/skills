# Adynato Skills

A collection of AI agent skills for Adynato projects, following the [Agent Skills](https://agentskills.io/) specification.

## Installation

```bash
# Install all skills
npx add-skill adynato/skills

# Install specific skills
npx add-skill adynato/skills --skill seo --skill web

# Install globally (available across all projects)
npx add-skill adynato/skills -g

# Install to specific agents
npx add-skill adynato/skills -a claude-code -a cursor
```

## Available Skills

| Skill | Description |
|-------|-------------|
| **seo** | SEO requirements including LD+JSON schema.org, backlinks, further reading sections, meta tags, and Open Graph |
| **web** | Web development conventions, image optimization with img4web, component patterns, and styling |
| **mobile** | Mobile app development with React Native and Expo - navigation, native APIs, performance |
| **web-api** | Web API patterns for Next.js - route handlers, validation, auth, error handling |
| **mobile-api** | API integration for mobile apps - TanStack Query, auth flows, offline support |

## Usage

Skills activate automatically when your AI agent detects relevant tasks. No explicit invocation needed.

**Trigger phrases:**
- "Add an image to the hero section" → activates **web** skill (img4web guidance)
- "Create a blog post" → activates **seo** skill (LD+JSON, backlinks, further reading)
- "Build a new API endpoint" → activates **web-api** skill
- "Fetch data from the API" → activates **mobile-api** skill
- "Add a new screen to the app" → activates **mobile** skill

## Skill Structure

```
skills/
├── seo/
│   ├── SKILL.md
│   └── references/
│       └── SCHEMAS.md      # LD+JSON templates
├── web/
│   └── SKILL.md
├── mobile/
│   └── SKILL.md
├── web-api/
│   └── SKILL.md
└── mobile-api/
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
| **vercel-deploy** | Deploy apps to Vercel directly from conversations |

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

1. Create a new directory in `skills/` with your skill name
2. Add a `SKILL.md` with required frontmatter (`name`, `description`)
3. Optionally add `scripts/`, `references/`, or `assets/` directories
4. Submit a pull request

See the [Agent Skills Specification](https://agentskills.io/specification) for full format details.

## License

MIT
