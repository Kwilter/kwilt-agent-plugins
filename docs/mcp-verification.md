# MCP Verification Log

Use this file to record clean-network checks before submission.

## Current Endpoint

```text
https://auth.kwilt.app/functions/v1/mcp
```

## Basic Reachability Check

Command:

```bash
curl -i https://auth.kwilt.app/functions/v1/mcp
```

Expected result:

- The endpoint is reachable over HTTPS.
- A plain `GET` may return `405 Method not allowed`, because MCP clients normally use the configured transport rather than a browser-style GET.
- The response must not expose secrets.

Observed on 2026-05-13 from a clean shell network:

```text
HTTP/2 405
{"error":{"message":"Method not allowed"}}
```

Command:

```bash
curl -i -X OPTIONS https://auth.kwilt.app/functions/v1/mcp
```

Observed on 2026-05-13 from a clean shell network:

```text
HTTP/2 200
access-control-allow-origin: *
access-control-allow-headers: authorization, x-client-info, apikey, content-type
access-control-allow-methods: GET, POST, OPTIONS
ok
```

## OAuth Metadata Checks

Run these before submission:

```bash
curl -i https://auth.kwilt.app/.well-known/oauth-authorization-server
curl -i https://auth.kwilt.app/.well-known/oauth-protected-resource/functions/v1/mcp
```

If either endpoint is intentionally hosted elsewhere or requires Supabase-specific routing, document that here and verify the MCP client still completes Dynamic Client Registration or OAuth discovery.

## MCP Inspector Check

Run the MCP Inspector from a clean machine or clean shell environment:

```bash
npx -y @modelcontextprotocol/inspector
```

In the Inspector:

1. Select the remote HTTP transport.
2. Enter `https://auth.kwilt.app/functions/v1/mcp`.
3. Complete OAuth.
4. Run initialize.
5. List tools.
6. Call each context tool with the demo account.
7. With write scope granted, create one controlled Goal and one controlled Activity, then verify the Activity appears under that Goal.

Expected result:

- OAuth completes without MFA or internal network access.
- The server lists context tools and the expected Goal/Activity write tools for the granted scope.
- Tool calls return summarized Kwilt context.
- Write tools create, update, or recoverably delete only user-owned Kwilt planning records.
- Tool results do not include tokens, secrets, unrelated account data, or unexpected raw records.

Non-interactive clean-shell check:

```bash
npx -y @modelcontextprotocol/inspector --cli https://auth.kwilt.app/functions/v1/mcp --transport http --method tools/list
```

Observed on 2026-05-13:

```text
Failed to connect to MCP server: Streamable HTTP error: Error POSTing to endpoint: {"error":{"message":"Missing Authorization","code":"unauthorized"}}
```

This is an expected unauthenticated result for a protected OAuth MCP server. A full reviewer-grade pass still requires an OAuth-capable interactive client or demo credentials.

## Pre-Submission Evidence

Before final public submission, capture:

- Date and platform tested.
- Client name and version.
- OAuth result.
- Tool list.
- One successful result for each reviewer test prompt.
- One successful controlled Goal and Activity write result, including the visible Goal and Activity names.
- Any known platform-specific callback URL.

Observed on 2026-06-26 from Codex against the hosted endpoint with an authenticated Kwilt MCP token:

- `initialize` returned server `Kwilt` version `0.1.0`.
- `tools/list` returned 26 tools.
- First read tools returned by the hosted server: `get_current_account`, `list_arcs`, `get_arc`, `list_goals`, `get_goal`, `list_recent_activities`, `get_current_chapter`, `get_show_up_status`.
- Step-level To-do write tools were present: `create_activity_step`, `update_activity_step`, `mark_activity_step_done`, `delete_activity_step`, `reorder_activity_steps`.
- Every listed tool included explicit `readOnlyHint`, `openWorldHint`, and `destructiveHint` annotations.
- The live hosted tool list matched `chatgpt-app-submission.json`: 26 tools, no missing tools, no extra tools, no hint mismatches.
- No listed tool declared an `outputSchema`; add output schemas in a future MCP hardening pass so models can use structured results more reliably.

## Sprint B Write Smoke

Observed on 2026-06-07 from Codex with the Kwilt MCP connector authenticated:

- Listed existing Goals before writing.
- Created Goal: `Agent plugin verification`.
- Created Activity under that Goal: `Verify control-plane write capture`.
- Fetched the Goal and verified the Activity appeared under it.
- Marked the Activity done.
- Marked the Goal completed.

This confirms the connector can perform the controlled Goal and Activity write flow needed by `skills/kwilt-control-plane/SKILL.md`.
