# Privacy

The Kwilt plugin connects an AI agent to the Kwilt MCP server only after the user authorizes access through OAuth.

## Data Available To The Agent

Sprint B access can read summarized Kwilt context:

- Arcs
- Goals
- Recent Activities
- Current or latest Chapter context
- Show-up or streak status

When the user grants OAuth write scope, the agent can also create or update user-owned Goals and Activities. The intended write use is durable planning capture: build to-dos, deferred follow-ups, and implementation outcomes that should persist in Kwilt.

The plugin should not expose raw database records, hidden notes, credentials, or unrelated account data.

## Data The Plugin Stores

This repository does not store user data. Authentication tokens and MCP connection state are handled by the host agent client and the Kwilt MCP OAuth flow.

Kwilt server-side systems may keep audit records for MCP tool usage, such as the authenticated user, tool name, timestamp, item identifiers when applicable, and short summaries. Audit records are for security, support, and abuse prevention, not for storing agent transcripts in this repository.

## User Expectations

Agents should summarize Kwilt context in user-facing language and avoid implying access to private fields that the MCP server did not return.

Agents should summarize write actions before handoff, including the Goal or Activity names they created or updated. They should avoid writing every tiny implementation step and should mark Activities done only after verification.
