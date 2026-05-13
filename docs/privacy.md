# Privacy

The Kwilt plugin connects an AI agent to the Kwilt MCP server only after the user authorizes access through OAuth.

## Data Available To The Agent

Sprint A access is read-only and limited to summarized Kwilt context:

- Arcs
- Goals
- Recent Activities
- Current or latest Chapter context
- Show-up or streak status

The plugin should not expose raw database records, hidden notes, credentials, or unrelated account data.

## Data The Plugin Stores

This repository does not store user data. Authentication tokens and MCP connection state are handled by the host agent client and the Kwilt MCP OAuth flow.

## User Expectations

Agents should summarize Kwilt context in user-facing language and avoid implying access to private fields that the MCP server did not return.
