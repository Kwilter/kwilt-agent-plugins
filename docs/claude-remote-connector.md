# Claude Remote MCP Connector Notes

This repo targets Claude's remote MCP connector path for public Claude distribution.

## Connector Details

- Connector name: `Kwilt`
- Connector URL: `https://auth.kwilt.app/functions/v1/mcp`
- Transport: HTTP remote MCP
- Authentication: OAuth
- Access level: Sprint B context plus Goal and Activity writes when OAuth write scope is granted
- Public docs: `https://github.com/Kwilter/kwilt-agent-plugins`
- Privacy policy: `https://kwilt.app/privacy`
- Terms: `https://kwilt.app/terms`

## Submission Framing

Short description:

```text
Connect Claude to your Kwilt account, Arcs, Goals, recent Activities, Chapter context, and show-up status.
```

Long description:

```text
Kwilt gives Claude access to summarized personal planning context from Kwilt. After OAuth consent, Claude can help users reflect on their Arcs, Goals, recent Activities, Chapter context, and show-up status. With write consent, Claude can also create or update durable Goals and Activities for build to-dos and deferred follow-ups.
```

## Anthropic Review Checklist

- Confirm the MCP server is reachable from Anthropic's cloud infrastructure.
- Confirm OAuth works without manual setup, MFA, SMS, email OTP, VPN, or internal network access.
- Confirm the connector does not expose unrelated account data.
- Confirm write actions are limited to user-owned Goals and Activities and require appropriate OAuth consent.
- Confirm destructive actions are absent from the public connector unless separately reviewed and documented.
- Confirm privacy and revocation documentation is public and accurate.
- Confirm demo account data is stable and non-sensitive.
- Confirm tool outputs stay concise enough for Claude review and normal chat use.

## Local Claude Testing

For Claude Code, add the remote MCP server as a project or user-scoped server and complete OAuth:

```bash
claude mcp add --transport http kwilt https://auth.kwilt.app/functions/v1/mcp
```

Then run:

```text
/mcp
```

Confirm the Kwilt server is connected, authenticated, and exposing the expected context tools plus Goal and Activity write tools when write scope is granted.

## Directory Submission

Use Anthropic's Connectors Directory review flow for public discoverability. The submission should reference the public MCP URL, privacy policy, revocation process, and demo account plan.

Official references:

- https://support.anthropic.com/en/articles/11596036-anthropic-mcp-directory-faq
- https://support.anthropic.com/en/articles/11175166-getting-started-with-custom-integrations-using-remote-mcp
- https://support.anthropic.com/en/articles/11503834-building-custom-integrations-via-remote-mcp-servers

## Desktop Extension Note

Claude Desktop also supports local desktop extensions, but this repo does not currently ship a `.mcpb` package. If Kwilt later needs one-click local Claude Desktop install, add a dedicated desktop extension package with a `manifest.json`, package it with `mcpb pack`, and test installation from Claude Desktop Settings > Extensions.
