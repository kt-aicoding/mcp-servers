# Local MCP System

Last refreshed: 2026-06-27.

This document captures the MCP operating model for Kevin's AI coding environment. It is a public, sanitized snapshot and must not contain tokens, API keys, OAuth secrets, browser cookies, machine-local private paths, or private project context.

## Default MCP Surface

| MCP server | Status | Purpose |
| --- | --- | --- |
| `context7` | enabled | Current library/framework/API documentation |
| `playwright` | enabled | Browser automation and QA |

The default MCP surface is intentionally small. Most cloud, source-control, and database workflows are handled by local CLIs.

## MCP Versus CLI Boundary

| Workflow | Default tool | Reason |
| --- | --- | --- |
| GitHub repo, CI, PR, issue work | `gh` CLI | Keyring auth is reliable; commands are deterministic and auditable |
| Vercel projects/deployments/env | `vercel` CLI | Mature provider CLI; lower auth/session overhead |
| Supabase projects/database operations | `supabase` CLI | Mature provider CLI and project-local workflows |
| Cloudflare Workers/Pages/D1/KV/R2/Queues | `wrangler` CLI | Broad provider coverage and direct resource visibility |
| CloudBase environment/function work | `tcb` CLI | Existing authenticated provider CLI |
| Current library/framework docs | `context7` MCP | Agent-native retrieval of fresh docs |
| Browser QA and automation | `playwright` MCP or Playwright CLI | Use MCP for agent-controlled browser workflows; use CLI/tests for deterministic checks |
| Figma/design files | no default MCP | Use exported screenshots/files unless the user explicitly asks for Figma MCP |

## Disabled Or Non-Default MCP Categories

| Category | Default stance |
| --- | --- |
| Provider MCPs for GitHub/Vercel/Supabase/Cloudflare | Do not default-enable when mature CLIs cover the workflow |
| Filesystem MCP | Not needed when local filesystem access is already available |
| Memory MCP | Do not enable without a defined workflow and retention policy |
| Sequential-thinking MCP | Avoid by default; use normal planning unless explicitly needed |
| Security MCP | Use explicit security-review skills and local scanners unless a task needs a remote security connector |

## Design Principles

- Keep global MCP minimal: `context7` and `playwright`.
- Prefer explicit, composable MCP tool surfaces.
- Avoid broad provider MCP auth unless it adds concrete agent-native value beyond a CLI.
- Do not store secrets or private machine state in MCP docs.
- Test MCP servers per project before making them global defaults.
- Promote mature MCP servers into standalone repositories only after their API surface stabilizes.

## Maintenance Commands

```bash
codex mcp list
codex doctor --json
```

When testing browser MCP behavior:

```bash
playwright --version
```

When reviewing whether a provider MCP is necessary, first check the equivalent CLI:

```bash
gh auth status --active
vercel whoami
supabase projects list
wrangler whoami
tcb env list
```

## Repository Placement

| Content | Preferred repository |
| --- | --- |
| MCP server staging | `kt-aicoding/mcp-servers` |
| Mature standalone MCP server | dedicated `kt-aicoding/<server-name>` repository |
| CLI utilities | `kt-aicoding/cli-tools` |
| Skills and agent instructions | `kt-aicoding/skills` |
| Cross-category index | `kt-aicoding/registry` |
