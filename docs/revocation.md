# Revoking Access

Users can revoke Kwilt plugin access by disabling or removing the Kwilt MCP server from their agent client.

Revocation stops both read access and any granted write access for creating or updating Kwilt Goals and Activities.

## Client-Side Steps

1. Open the agent's MCP or plugin settings.
2. Find the `Kwilt` MCP server.
3. Disable or remove the server.
4. Restart the agent if it does not immediately refresh MCP connections.

## Server-Side Steps

If Kwilt exposes an account-level connected apps page, revoke the agent client there as well. This invalidates the OAuth grant even if the local plugin files remain installed.

If the user granted write scope, server-side revocation should invalidate that write grant along with read access. Existing Goals and Activities created before revocation remain in Kwilt unless the user changes or deletes them in Kwilt.

## Reconnecting

To reconnect, enable the `Kwilt` MCP server again and complete the OAuth flow.
