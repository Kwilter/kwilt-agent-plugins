# Cursor Plugin

Cursor Marketplace can use this repository URL directly. The Cursor-specific manifest is:

```text
.cursor-plugin/plugin.json
```

The manifest points at:

- `skills/` for the shared Kwilt context and control-plane skills
- `mcp.json` for the hosted OAuth MCP server at `https://auth.kwilt.app/functions/v1/mcp`
- `assets/logo.svg` for the plugin logo

## Local Install

```bash
mkdir -p ~/.cursor/plugins/local
ln -s /path/to/kwilt-agent-plugins ~/.cursor/plugins/local/kwilt
```

Restart Cursor or run **Developer: Reload Window**.

## OAuth Callback

Cursor uses this callback:

```text
cursor://anysphere.cursor-mcp/oauth/callback
```

The Kwilt MCP server allows that callback and completes OAuth through the hosted Kwilt consent screen.

## Control-Plane Behavior

The `kwilt-control-plane` skill teaches Cursor Agent to use Kwilt as durable storage for build Goals and To-dos. It should reuse matching Goals, create a new Goal only for a new durable workstream, capture deliverable steps as Activities, and mark Activities done only after verification.

## Marketplace Checklist

- Verify `.cursor-plugin/plugin.json` validates against Cursor's current plugin schema.
- Confirm `mcp.json` points to the production OAuth MCP server.
- Confirm OAuth consent includes write capability before advertising Goal or To-do writes in marketplace copy.
- Use PNG marketplace screenshots from `assets/screenshots/`.
- Confirm `docs/privacy.md` and `docs/revocation.md` are linked from the marketplace listing.
- Run `docs/reviewer-test-plan.md` against a clean Cursor profile before submitting.
