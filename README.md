# Kwilt AI Agent Plugins

Connect Cursor, Claude Code, and Codex to Kwilt through the Kwilt OAuth MCP server.

This repository intentionally contains all Kwilt agent plugin artifacts in one place. Cursor Marketplace can use this repository URL because the Cursor plugin manifest still lives at `.cursor-plugin/plugin.json`; Claude Code and Codex use their own manifests from the same repo.

## What This Includes

- A shared remote MCP server config for `https://auth.kwilt.app/functions/v1/mcp`
- Plugin manifests for Claude Code, Cursor, and Codex
- A Kwilt context skill that teaches agents how to use account, Arc, Goal, Activity, Chapter, and show-up context
- A Kwilt control-plane skill that teaches agents to capture durable build Goals and To-dos during coding work
- Sprint B access to read Kwilt context and, with OAuth write consent, create, update, or recoverably delete user-owned planning records
- A submission packet for ChatGPT/OpenAI, Codex, Claude, and Cursor review
- PNG marketplace assets for review surfaces that do not accept SVG-only assets

## Repository Layout

```text
.cursor-plugin/plugin.json   Cursor Marketplace/plugin manifest
.claude-plugin/plugin.json   Claude Code plugin manifest
.codex-plugin/plugin.json    Codex plugin manifest
.plugin/plugin.json          Generic shared plugin manifest
mcp.json                     Cursor-facing remote MCP config
.mcp.json                    Shared remote MCP config with context note
skills/kwilt/SKILL.md        Shared Kwilt read/context skill
skills/kwilt-control-plane/  Shared Goal and To-do control-plane skill
docs/                        Privacy, revocation, and platform notes
assets/logo.svg              Shared plugin logo
assets/png/                  PNG icon and logo exports
assets/screenshots/          PNG marketplace screenshots and editable SVG sources
SUBMISSION.md                Public submission plan and per-platform checklist
```

## Install Locally

### Cursor

Symlink this plugin into Cursor's local plugin directory:

```bash
mkdir -p ~/.cursor/plugins/local
ln -s /path/to/kwilt-agent-plugins ~/.cursor/plugins/local/kwilt
```

Then restart Cursor or run **Developer: Reload Window**.

See `docs/cursor.md` for Cursor-specific submission and setup notes.

### Claude Code

Symlink this plugin into Claude's local plugin directory:

```bash
mkdir -p ~/.claude/plugins/local
ln -s /path/to/kwilt-agent-plugins ~/.claude/plugins/local/kwilt
```

Then restart Claude Code.

See `docs/claude.md` for Claude-specific setup notes.

### Codex

Symlink this plugin into Codex's local plugin directory:

```bash
mkdir -p ~/plugins
ln -s /path/to/kwilt-agent-plugins ~/plugins/kwilt
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
What Kwilt account are you connected to?
```

Then try:

```text
Summarize my current Kwilt goals and recent activity.
```

For control-plane behavior, try:

```text
Use Kwilt to keep track of the durable to-dos for this build.
```

## Permissions

Sprint B can read limited Kwilt summaries for:

- Authenticated account identity
- Arcs
- Goals
- Recent Activities
- Current or latest Chapter context
- Show-up or streak status

When the user grants OAuth write scope, the MCP server can create, update, or recoverably delete user-owned Arcs, Goals, To-dos, To-do steps, Goal check-ins, focus state, and Chapter user notes. Agents should use that write path only for durable planning records, not for every tiny implementation checklist item.

Expected write behavior:

- Reuse an existing Goal when one clearly fits.
- Create a new Goal only for a new durable workstream.
- Capture deliverable steps and deferred follow-ups as To-dos or To-do steps.
- Mark To-dos or steps done only after the implementation and verification have passed.
- Summarize all Kwilt writes at handoff.

See `docs/privacy.md` and `docs/revocation.md` for publishing-ready privacy and access guidance.

## Publishing Prep

Before publishing broadly, verify OAuth callbacks for Claude Code and Codex, run the reviewer test plan, and confirm the demo account is seeded.

Start with:

- `SUBMISSION.md`
- `docs/reviewer-test-plan.md`
- `docs/demo-account-plan.md`
- `docs/claude-remote-connector.md`
- `docs/mcp-verification.md`

Cursor Marketplace submission starts at:

https://cursor.com/marketplace/publish
