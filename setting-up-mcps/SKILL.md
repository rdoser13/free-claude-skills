---
name: setting-up-mcps
description: Guide users through connecting Claude Code to external tools via MCP (Model Context Protocol). Use when setting up new MCP servers, troubleshooting MCP connections, adding integrations like GitHub, Notion, Sentry, or databases, or when user mentions "MCP", "integrations", "connect to tools", or asks how to give Claude access to external services.
version: 1.0.0
# No API keys required - procedural guidance skill
---

# Setting Up MCPs

MCP (Model Context Protocol) connects Claude Code to external tools like GitHub, Notion, databases, and more.

## Quick Reference

| Action | Command |
|--------|---------|
| Add cloud service | `claude mcp add --transport http <name> <url>` |
| Add local tool | `claude mcp add --transport stdio <name> -- <command>` |
| List connections | `claude mcp list` |
| Check status | `/mcp` (inside Claude Code) |
| Authenticate | `/mcp` → select service → "Authenticate" |
| Remove connection | `claude mcp remove <name>` |

## Setup Workflow

Follow this checklist for any new MCP:

```
- [ ] Step 1: Identify the service type (cloud or local)
- [ ] Step 2: Get the MCP URL or command
- [ ] Step 3: Run the add command
- [ ] Step 4: Verify with `claude mcp list`
- [ ] Step 5: Authenticate if needed (`/mcp`)
- [ ] Step 6: Test with a simple request
```

### Step 1: Identify Service Type

**Cloud services** (GitHub, Notion, Sentry, etc.):
- Use `--transport http` or `--transport sse`
- Require a URL like `https://mcp.servicename.com/...`
- Usually need browser authentication

**Local tools** (databases, file servers, custom scripts):
- Use `--transport stdio`
- Require a command like `npx -y package-name`
- May need API keys via `--env`

### Step 2: Get Setup Information

Find the service's MCP documentation. Look for:
- **URL** for cloud services
- **npm package** or **command** for local tools
- **Required environment variables** (API keys)

For popular services, see [references/popular-services.md](references/popular-services.md).

### Step 3: Run the Add Command

**Cloud service (HTTP):**
```bash
claude mcp add --transport http <name> <url>
```

**Cloud service with auth header:**
```bash
claude mcp add --transport http <name> <url> --header "Authorization: Bearer <token>"
```

**Local tool (stdio):**
```bash
claude mcp add --transport stdio <name> -- <command>
```

**Local tool with API key:**
```bash
claude mcp add --transport stdio <name> --env API_KEY=<value> -- <command>
```

**Important:** All flags (`--transport`, `--env`, `--scope`, `--header`) must come before the server name. Use `--` to separate the name from the command.

### Step 4: Verify Connection

```bash
claude mcp list
```

Confirm the new connection appears in the list.

### Step 5: Authenticate (If Required)

Inside Claude Code:
1. Type `/mcp`
2. Select the service
3. Choose "Authenticate"
4. Complete browser login

### Step 6: Test

Ask Claude something that uses the tool:
- GitHub: "List my open pull requests"
- Notion: "Show my recent pages"
- Database: "List the tables"

## Scopes

| Scope | Flag | Use Case |
|-------|------|----------|
| local (default) | none | Personal, this project only |
| project | `--scope project` | Team-shared via `.mcp.json` in Git |
| user | `--scope user` | Personal, all your projects |

Example:
```bash
claude mcp add --transport http github --scope user https://api.githubcopilot.com/mcp/
```

## Management Commands

```bash
# List all connections
claude mcp list

# Get details for one
claude mcp get <name>

# Remove connection
claude mcp remove <name>

# Check status inside Claude Code
/mcp
```

## Troubleshooting

For common issues and solutions, see [references/troubleshooting.md](references/troubleshooting.md).

**Quick fixes:**
- **Windows "Connection closed"**: Add `cmd /c` before `npx` commands
- **Tools not appearing**: Restart Claude Code after adding MCPs
- **Auth failing**: Use `/mcp` → "Clear authentication" and retry
- **Timeout errors**: Set `MCP_TIMEOUT=30000 claude` for longer startup
