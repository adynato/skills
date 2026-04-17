---
name: adynato-omp-mcp
description: Configure MCP servers for Oh My Pi using repo-local `.omp/mcp.json` without polluting teammates. Covers preferred OMP config locations, adding `.omp/` to `.gitignore` when absent, and common setup patterns with an Atlassian Rovo example. Use when adding or updating MCP servers for a project in OMP.
---

# OMP MCP Setup Skill

Use this skill when setting up MCP servers for Oh My Pi in a repository.

## Default to OMP-Native Config

- Prefer `.omp/mcp.json` for repo-local MCP setup
- Use `~/.omp/mcp.json` only when the server should apply across many projects for your user
- Do not default to root `mcp.json` or `.mcp.json` unless the user explicitly wants a portable cross-client config
- Include the OMP MCP schema at the top of repo-local config for autocomplete and validation

## Keep Repo-Local MCP Out of Git

- Before creating `.omp/mcp.json`, check whether the repo already ignores `.omp/`
- If not, add `.omp/` to `.gitignore`
- Treat `.omp/` as local machine or user setup by default so credentials, auth state, and teammate-specific MCP choices are not committed
- Only keep `.omp/` tracked if the user explicitly asks for shared project-level OMP config

## Base File Template

```json
{
  "$schema": "https://raw.githubusercontent.com/can1357/oh-my-pi/main/packages/coding-agent/src/config/mcp-schema.json",
  "mcpServers": {}
}
```

## Atlassian Rovo Example

Use the official remote endpoint:

```text
https://mcp.atlassian.com/v1/mcp
```

```json
{
  "$schema": "https://raw.githubusercontent.com/can1357/oh-my-pi/main/packages/coding-agent/src/config/mcp-schema.json",
  "mcpServers": {
    "atlassian": {
      "type": "http",
      "url": "https://mcp.atlassian.com/v1/mcp"
    }
  }
}
```

Notes:
- Atlassian Rovo MCP normally authenticates with OAuth 2.1
- API token auth is only available if the organization admin has enabled it
- Prefer `/mcp` for new setups; Atlassian is deprecating `/sse`

## Setup Checklist

- [ ] `.omp/` is ignored in `.gitignore`
- [ ] `.omp/mcp.json` exists with the schema URL
- [ ] The MCP server is added with the correct transport and endpoint
- [ ] Authentication is completed in OMP before relying on the server
