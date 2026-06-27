<p align="center">
  <img src="https://raw.githubusercontent.com/kt-aicoding/.github/main/assets/logo.svg" alt="KT AI Coding logo" width="96" />
</p>

# KT AI Coding MCP Servers

Model Context Protocol servers for AI coding workflows.

中文说明见 [README.zh-CN.md](README.zh-CN.md)。

## Scope

This repository is a staging area for small or related MCP servers that support coding agents: code context, review, search, browser/devtools automation, project indexing, and developer workflow automation.

Mature servers can graduate into standalone repositories under `kt-aicoding`.

## Layout

```text
docs/
  local-mcp-system.md
servers/
  <server-name>/
```

## Operating References

| Document | Notes |
| --- | --- |
| [Local MCP System](docs/local-mcp-system.md) | Default MCP surface, CLI/MCP boundary, disabled MCP categories, and maintenance commands. |

## Guidelines

- Keep each server installable and documented independently.
- Include client configuration examples for Codex and Claude Code when applicable.
- Prefer explicit tool names and small, composable MCP surfaces.
