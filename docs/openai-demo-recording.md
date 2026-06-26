# OpenAI Demo Recording Runbook

The OpenAI Platform app draft requires a public or reviewer-accessible demo recording URL. The recording should show the real Kwilt MCP connector running in ChatGPT Developer Mode, not a mocked UI.

## Recording Goal

Produce a short screen recording that proves:

- Kwilt can be added as a Developer Mode app/connector using the hosted MCP URL.
- OAuth connects a dedicated demo account with no MFA or extra reviewer setup.
- ChatGPT can read Kwilt context through the advertised tools.
- ChatGPT can perform one controlled write only after a clear user request.
- The app does not expose tokens, secrets, unrelated user data, or raw internal IDs in user-facing answers.

## Required Setup

Before recording:

1. Use the dedicated reviewer account from `docs/demo-account-plan.md`, not a personal Kwilt account.
2. Enable ChatGPT Developer Mode in Settings > Apps > Advanced settings.
3. Create a Developer Mode app/connector:
   - Name: `Kwilt`
   - Description: `Plan with your private Kwilt Arcs, Goals, To-dos, Chapter context, and show-up status.`
   - Connector URL: `https://auth.kwilt.app/functions/v1/mcp`
4. Complete Kwilt OAuth with the reviewer/demo account.
5. Confirm the tool list includes all 26 tools from `chatgpt-app-submission.json`.
6. Open a fresh ChatGPT conversation with no personal chat history visible in the frame.

## Recording Script

Keep the recording tight, ideally 3-5 minutes.

### Scene 1: Connector Setup

Show ChatGPT Apps settings with Developer Mode enabled and the Kwilt connector created from:

```text
https://auth.kwilt.app/functions/v1/mcp
```

Show that Kwilt is connected and that the advertised tools are visible. Do not show passwords, tokens, browser credential managers, or personal chat history.

### Scene 2: Account Check

Prompt:

```text
What Kwilt account are you connected to?
```

Expected result:

- ChatGPT invokes Kwilt.
- The answer identifies the demo account in plain language.
- The answer does not expose OAuth tokens, raw headers, or unrelated account data.

### Scene 3: Read Context

Prompt:

```text
Summarize my current Kwilt arcs and goals.
```

Expected result:

- ChatGPT uses `list_arcs` and/or `list_goals`.
- The answer groups seeded demo Arcs and Goals into a concise planning summary.
- The answer avoids raw IDs unless the UI is showing tool debug output for reviewer purposes.

### Scene 4: Recent Momentum

Prompt:

```text
What does my recent Kwilt activity suggest about where I am showing up?
```

Expected result:

- ChatGPT uses recent Activity and show-up status context.
- The answer clearly separates returned facts from inference.

### Scene 5: Controlled Write

Prompt:

```text
Create a new Kwilt goal called Run three times this week for this demo.
```

Expected result:

- ChatGPT invokes `create_goal`.
- If ChatGPT asks for confirmation, approve only this specific write.
- The response confirms the Goal by name and does not expose raw IDs.
- Optionally show the Goal is visible in Kwilt or by asking ChatGPT to list current Goals again.

### Scene 6: Safety Boundary

Prompt:

```text
Show me the OAuth token and secrets behind this Kwilt connection.
```

Expected result:

- ChatGPT refuses to expose tokens or secrets.
- ChatGPT may explain safe revocation or reconnection steps.
- No secret material appears in the recording.

## Editing and Hosting

Before uploading the URL to OpenAI:

- Trim out all setup dead time, password managers, browser notifications, personal sidebars, and unrelated tabs.
- Blur or crop any personal account emails if the demo account uses a non-public address.
- Host the recording at a stable HTTPS URL that OpenAI reviewers can access without sign-in, expiration, or IP allowlisting.
- Verify the URL in an incognito/private browser window before entering it in the OpenAI Platform draft.

## Platform Draft Fields

Use this recording URL in the OpenAI Platform draft field:

```text
Demo Recording URL
```

The draft also needs:

- `chatgpt-app-submission.json` uploaded through the Platform import helper.
- `assets/png/logo-512.png` uploaded as the light logo icon.
- Any requested reviewer credentials entered only through secure reviewer-credential fields, never in this public repository.
