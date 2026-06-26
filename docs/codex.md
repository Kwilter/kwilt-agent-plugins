# Codex Plugin

The Codex-specific manifest is:

```text
.codex-plugin/plugin.json
```

It reuses the shared Kwilt skill and shared MCP config:

- `skills/kwilt/SKILL.md`
- `skills/kwilt-control-plane/SKILL.md`
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

Enable the `Kwilt` MCP server in Codex and complete the hosted OAuth consent flow. Sprint B access reads summarized Kwilt context and, when write scope is granted, lets Codex create or update Goals and Activities for durable build to-dos.

## Control-Plane Behavior

Use `skills/kwilt-control-plane/SKILL.md` when Codex is building features, removing features with deferred follow-up, capturing roadmap work, or keeping long-running implementation to-dos aligned with Kwilt Goals. Codex should summarize any Kwilt writes before handing work back.

## Notes

Codex marketplace conventions may change. Keep Codex-specific metadata in `.codex-plugin/plugin.json`, and keep shared behavior in `.mcp.json`, `skills/kwilt/SKILL.md`, and `skills/kwilt-control-plane/SKILL.md`.

For public OpenAI distribution, start from `SUBMISSION.md`. The current public route is OpenAI Apps SDK submission for ChatGPT; approved published apps can create the corresponding Codex plugin distribution.
