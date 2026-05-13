# Claude Code Plugin

The Claude Code-specific manifest is:

```text
.claude-plugin/plugin.json
```

It reuses the shared Kwilt skill and shared MCP config:

- `skills/kwilt/SKILL.md`
- `.mcp.json`

## Local Install

```bash
mkdir -p ~/.claude/plugins/local
ln -s /path/to/kwilt-cursor-plugin ~/.claude/plugins/local/kwilt
```

Restart Claude Code after installing.

## Authentication

Enable the `Kwilt` MCP server in Claude Code and complete the hosted OAuth consent flow. Sprint A access is read-only and limited to summarized Kwilt context.

## Notes

Keep this manifest in the same repository as the Cursor and Codex manifests so shared skills, MCP config, privacy copy, and revocation guidance stay consistent across platforms.
