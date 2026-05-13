# Codex Plugin

The Codex-specific manifest is:

```text
.codex-plugin/plugin.json
```

It reuses the shared Kwilt skill and shared MCP config:

- `skills/kwilt/SKILL.md`
- `.mcp.json`

## Local Install

```bash
mkdir -p ~/plugins
ln -s /path/to/kwilt-agent-plugins ~/plugins/kwilt
```

If your Codex setup uses a local marketplace index, adapt the sample in:

```text
docs/codex-marketplace-example.json
```

## Authentication

Enable the `Kwilt` MCP server in Codex and complete the hosted OAuth consent flow. Sprint A access is read-only and limited to summarized Kwilt context.

## Notes

Codex marketplace conventions may change. Keep Codex-specific metadata in `.codex-plugin/plugin.json`, and keep shared behavior in `.mcp.json` and `skills/kwilt/SKILL.md`.
