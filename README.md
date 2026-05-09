# Kwilt Cursor Plugin

Connect Cursor to Kwilt through the Kwilt MCP server.

## What This Plugin Includes

- A remote MCP server config for `https://auth.kwilt.app/functions/v1/mcp`
- A Kwilt skill that teaches Cursor how to use Arcs, Goals, Activities, Chapters, and show-up status as personal context
- Read-only Sprint A access to Kwilt context

## Install Locally

Symlink this plugin into Cursor's local plugin directory:

```bash
mkdir -p ~/.cursor/plugins/local
ln -s /Users/andrewwatanabe/kwilt-cursor-plugin ~/.cursor/plugins/local/kwilt
```

Then restart Cursor or run **Developer: Reload Window**.

## Authenticate

1. Open Cursor Settings.
2. Go to **Tools & MCP**.
3. Find the `kwilt` MCP server.
4. Enable it and complete the OAuth flow.
5. Approve the Kwilt consent screen.

Cursor uses this OAuth callback:

```text
cursor://anysphere.cursor-mcp/oauth/callback
```

The Kwilt MCP server accepts that callback for Cursor OAuth.

## Try It

Ask Cursor Agent:

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

## Marketplace Prep

Before publishing, add:

- Final logo assets
- Marketplace copy and screenshots
- Clear privacy and revocation documentation

Public Marketplace submission starts at:

https://cursor.com/marketplace/publish
