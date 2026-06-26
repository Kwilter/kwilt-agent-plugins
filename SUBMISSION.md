# Kwilt Agent Plugin Submission Plan

This repo packages the Kwilt remote MCP connector for agent clients. The core artifact is the hosted OAuth MCP server:

```text
https://auth.kwilt.app/functions/v1/mcp
```

Sprint B exposes summarized Kwilt context for account inspection, Arcs, Goals, recent Activities, Chapter context, and show-up status. With OAuth write scope, the connector can also create, update, or recoverably delete user-owned Arcs, Goals, Activities, Activity steps, Goal check-ins, focus state, and Chapter user notes so agents can preserve durable build to-dos and deferred follow-ups in Kwilt.

## Submission Tracks

### ChatGPT / OpenAI Apps SDK

OpenAI's public submission path is an Apps SDK app submitted through the OpenAI Platform Dashboard after testing in Developer Mode. A published, approved ChatGPT app can also create Codex plugin distribution.

Current repo status:

- MCP server URL is present in `.mcp.json`.
- Submission import data is present in `chatgpt-app-submission.json`.
- Privacy and revocation notes are present in `docs/privacy.md` and `docs/revocation.md`.
- PNG logo and screenshot assets are present in `assets/png/` and `assets/screenshots/`.
- Reviewer prompts and expected outputs are present in `docs/reviewer-test-plan.md`.

Before submitting:

- Create or update the Apps SDK app draft in the OpenAI Platform Dashboard.
- Add MCP server details and OAuth settings.
- Configure CSP for all domains used by the app and UI, including `https://auth.kwilt.app` and `https://kwilt.app`.
- Upload logo and screenshots from `assets/png/` and `assets/screenshots/`.
- Add privacy policy and terms URLs:
  - `https://kwilt.app/privacy`
  - `https://kwilt.app/terms`
- Use the reviewer prompts and expected outputs from `docs/reviewer-test-plan.md`.
- Provide the demo account described in `docs/demo-account-plan.md`.

Useful official docs:

- https://developers.openai.com/apps-sdk/deploy/submission
- https://developers.openai.com/apps-sdk/app-submission-guidelines

### Codex Plugin Directory

Codex plugin packaging is represented by:

```text
.codex-plugin/plugin.json
```

The current official OpenAI path for public distribution is tied to ChatGPT app submission: when an approved app is published, OpenAI creates the Codex plugin distribution. Self-serve public Codex plugin publishing is not yet the primary public route.

Current repo status:

- `.codex-plugin/plugin.json` points to `./skills/` and `./.mcp.json`.
- `docs/codex-marketplace-example.json` provides a local marketplace entry for testing.
- PNG icons and screenshots are referenced by the Codex manifest.

Before submitting publicly:

- Test the plugin locally through a Codex local marketplace.
- Confirm OAuth works from a clean Codex install.
- Confirm every Kwilt MCP tool response matches the granted scope and does not leak tokens, hidden notes, or unrelated account data; agents should not reveal raw item IDs in user-facing answers unless the user is debugging the connector.
- Confirm write tools create, update, or recoverably delete only user-owned Kwilt planning records, and that agents summarize those writes before handoff.
- Keep release notes for any update after approval.

Useful official docs:

- https://developers.openai.com/codex/plugins/build

### Claude

Claude has two practical routes:

- Remote MCP connector for Claude, Claude Desktop, and mobile surfaces that support custom connectors.
- Desktop extension package for Claude Desktop when local one-click installation is desired.

This repo currently targets the remote MCP connector route. Claude-specific submission notes live in:

```text
docs/claude-remote-connector.md
```

Before submitting to Anthropic:

- Verify the MCP server is reachable from a public network.
- Verify OAuth from Claude using the final callback behavior.
- Provide a clear privacy policy and revocation instructions.
- Submit to the Anthropic Connectors Directory review process if Kwilt should be discoverable publicly.

Useful official docs:

- https://support.anthropic.com/en/articles/11596036-anthropic-mcp-directory-faq
- https://support.anthropic.com/en/articles/11175166-getting-started-with-custom-integrations-using-remote-mcp
- https://support.anthropic.com/en/articles/11503834-building-custom-integrations-via-remote-mcp-servers

### Cursor

Cursor public distribution is represented by:

```text
.cursor-plugin/plugin.json
mcp.json
```

Current repo status:

- Cursor manifest points at the shared Kwilt skill and Cursor-facing MCP config.
- Cursor OAuth callback is documented in `README.md` and `docs/cursor.md`.
- PNG logo and screenshot assets are present for marketplace review.

Before submitting:

- Validate `.cursor-plugin/plugin.json` against Cursor's latest marketplace schema.
- Confirm `mcp.json` uses the production MCP server URL.
- Verify OAuth with a clean Cursor profile.
- Confirm write tools are visible only after appropriate consent and work as described in the reviewer test plan.
- Submit through Cursor Marketplace using the repository URL.

Useful official docs:

- https://cursor.com/marketplace/publish
- https://docs.cursor.com/en/tools/mcp

## Review Packet

Use these files for review and submission:

- `docs/reviewer-test-plan.md`: Prompts, expected behavior, and rejection-risk checks.
- `chatgpt-app-submission.json`: OpenAI Apps submission import data with app info, tool hint justifications, and test cases.
- `docs/openai-demo-recording.md`: Demo recording runbook for the required OpenAI Platform recording URL.
- `docs/demo-account-plan.md`: Demo OAuth account and seeded data requirements.
- `docs/privacy.md`: Privacy and data exposure notes.
- `docs/revocation.md`: User revocation notes.
- `docs/claude-remote-connector.md`: Claude-specific connector submission notes.
- `assets/png/logo-512.png`: Primary PNG logo.
- `assets/png/icon-128.png`: Compact PNG icon.
- `assets/png/icon-64.png`: Small PNG icon.
- `assets/screenshots/kwilt-context-review.png`: Marketplace screenshot.
- `assets/screenshots/kwilt-goals-summary.png`: Marketplace screenshot.

## Pre-Submission Gate

Complete this checklist before sending any public submission:

- [ ] Public MCP endpoint responds correctly to MCP initialize and tool listing.
- [ ] OAuth succeeds from a clean reviewer account with no MFA or extra verification step.
- [ ] Demo account contains stable seeded data.
- [ ] All test prompts pass on the target client.
- [ ] OpenAI demo recording URL shows the real Developer Mode connector flow with the demo account.
- [ ] One controlled Goal and Activity write has been created and verified in Kwilt.
- [ ] Tool metadata and annotations match actual behavior.
- [ ] User-facing answers omit raw item IDs unless needed for connector debugging.
- [ ] Privacy policy discloses every user-related field returned by tools.
- [ ] Revocation instructions are accurate for both client-side disconnect and server-side OAuth revocation.
- [ ] PNG assets are uploaded instead of relying only on SVG.
- [ ] App/plugin descriptions do not imply OpenAI, Anthropic, or Cursor endorsement.
