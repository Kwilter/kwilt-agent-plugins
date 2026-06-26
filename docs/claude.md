# Claude Code Plugin

The Claude Code-specific manifest is:

```text
.claude-plugin/plugin.json
```

It reuses the shared Kwilt skill and shared MCP config:

- `skills/kwilt/SKILL.md`
- `skills/kwilt-control-plane/SKILL.md`
- `.mcp.json`

## Local Install

```bash
mkdir -p ~/.claude/plugins/local
ln -s /path/to/kwilt-agent-plugins ~/.claude/plugins/local/kwilt
```

Restart Claude Code after installing.

## Authentication

Enable the `Kwilt` MCP server in Claude Code and complete the hosted OAuth consent flow. Sprint B access reads summarized Kwilt context and, when write scope is granted, lets Claude Code create, update, or recoverably delete user-owned Arcs, Goals, To-dos, To-do steps, Goal check-ins, focus state, and Chapter user notes for durable planning capture.

## Control-Plane Behavior

Use `skills/kwilt-control-plane/SKILL.md` when Claude Code is doing feature work, preserving deferred follow-up, or keeping implementation to-dos aligned with Kwilt Goals. Claude should summarize any Kwilt writes before handing work back.

## Notes

Keep this manifest in the same repository as the Cursor and Codex manifests so shared skills, MCP config, privacy copy, and revocation guidance stay consistent across platforms.

For public Claude distribution, use the remote MCP connector route documented in `docs/claude-remote-connector.md`. That path is a better fit for Kwilt's hosted OAuth MCP server than treating this repository as only a local Claude Code plugin.
