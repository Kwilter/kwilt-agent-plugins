# Kwilt AI Agent Plugins

Connect Cursor, Claude Code, and Codex to Kwilt through the Kwilt OAuth MCP server.

This repository intentionally contains all Kwilt agent plugin artifacts in one place. Cursor Marketplace can use this repository URL because the Cursor plugin manifest still lives at `.cursor-plugin/plugin.json`; Claude Code and Codex use their own manifests from the same repo.

## What This Includes

- A shared remote MCP server config for `https://auth.kwilt.app/functions/v1/mcp`
- Plugin manifests for Claude Code, Cursor, and Codex
- A Kwilt skill that teaches agents how to use Arcs, Goals, Activities, Chapters, and show-up status as personal context
- Read-only Sprint A access to Kwilt context

## Repository Layout

```text
.cursor-plugin/plugin.json   Cursor Marketplace/plugin manifest
.claude-plugin/plugin.json   Claude Code plugin manifest
.codex-plugin/plugin.json    Codex plugin manifest
.plugin/plugin.json          Generic shared plugin manifest
mcp.json                     Cursor-facing remote MCP config
.mcp.json                    Shared remote MCP config with context note
skills/kwilt/SKILL.md        Shared Kwilt agent skill
docs/                        Privacy, revocation, and platform notes
assets/logo.svg              Shared plugin logo
```

## Install Locally

### Cursor

Symlink this plugin into Cursor's local plugin directory:

```bash
mkdir -p ~/.cursor/plugins/local
ln -s /path/to/kwilt-cursor-plugin ~/.cursor/plugins/local/kwilt
```

Then restart Cursor or run **Developer: Reload Window**.

See `docs/cursor.md` for Cursor-specific submission and setup notes.

### Claude Code

Symlink this plugin into Claude's local plugin directory:

```bash
mkdir -p ~/.claude/plugins/local
ln -s /path/to/kwilt-cursor-plugin ~/.claude/plugins/local/kwilt
```

Then restart Claude Code.

See `docs/claude.md` for Claude-specific setup notes.

### Codex

Symlink this plugin into Codex's local plugin directory:

```bash
mkdir -p ~/plugins
ln -s /path/to/kwilt-cursor-plugin ~/plugins/kwilt
```

If you use a local Codex marketplace file, add the plugin entry from `docs/codex-marketplace-example.json`.

See `docs/codex.md` for Codex-specific setup notes.

## Authenticate

1. Open the agent's MCP or plugin settings.
2. Find the `Kwilt` MCP server.
3. Enable it and complete the OAuth flow.
4. Approve the Kwilt consent screen.

Known Cursor OAuth callback:

```text
cursor://anysphere.cursor-mcp/oauth/callback
```

The Kwilt MCP server must allow each client callback before the OAuth flow can complete. The hosted OAuth MCP server supports Dynamic Client Registration for compatible clients.

## Try It

Ask your agent:

```text
What Kwilt arcs can you see?
```

Then try:

```text
Summarize my current Kwilt goals and recent activity.
```

## Permissions

Sprint A is read-only. The MCP server can read limited Kwilt summaries for:

- Arcs
- Goals
- Recent Activities
- Current or latest Chapter context
- Show-up or streak status

It cannot create, edit, or delete Kwilt data.

See `docs/privacy.md` and `docs/revocation.md` for publishing-ready privacy and access guidance.

## Publishing Prep

Before publishing broadly, add final marketplace screenshots and verify OAuth callbacks for Claude Code and Codex.

Cursor Marketplace submission starts at:

https://cursor.com/marketplace/publish
