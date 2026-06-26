# Reviewer Test Plan

Use these prompts and expected outcomes for ChatGPT, Codex, Claude, and Cursor review. Run them with the seeded demo account described in `docs/demo-account-plan.md`.

## Demo Data Assumptions

The demo account should include:

- At least three Arcs, including one active identity arc.
- At least four Goals across two or more Arcs.
- At least five recent Activities with dates in the last 14 days.
- One dedicated reviewer/demo account with no personal production data.
- One known Goal that reviewers can inspect in detail.
- One current or latest Chapter summary.
- One show-up or streak summary.

The connector can read summarized Kwilt context. With OAuth write scope, it can also create, update, or recoverably delete user-owned Arcs, Goals, To-dos, To-do steps, Goal check-ins, focus state, and Chapter user notes. Reviewer tests should use only controlled, non-destructive writes unless a destructive flow is explicitly being reviewed with resettable demo data. No test should publish, send, expose secrets, mutate unrelated data, or perform destructive actions outside the demo account.

## Test Cases

### 1. Account Connection

Prompt:

```text
What Kwilt account are you connected to?
```

Expected behavior:

- The agent calls the Kwilt MCP tools before answering.
- The answer identifies the connected reviewer/demo account in plain language.
- The answer does not expose raw OAuth tokens, session IDs, or unrelated account data.
- The answer makes clear that it is using the authenticated Kwilt MCP connection.

Expected output shape:

```text
Kwilt is connected to [demo account email]. I can use this connection to read the Kwilt context exposed through the MCP server.
```

### 2. Goal Summary

Prompt:

```text
Summarize my current Kwilt goals.
```

Expected behavior:

- The agent lists or groups active goals.
- The answer ties goals to Arcs when that relationship is available.
- The answer avoids generic coaching claims that are not supported by the returned data.

Expected output shape:

```text
Your current goals cluster around [theme]. In [Arc], you are working on [goal]. In [Arc], the next visible focus is [goal].
```

### 3. Recent Momentum

Prompt:

```text
What does my recent Kwilt activity suggest?
```

Expected behavior:

- The agent calls recent activity tooling.
- The answer distinguishes observation from inference.
- The answer gives a small next question or next focus, not a command.

Expected output shape:

```text
From the recent activity summaries, it looks like you have been showing up most around [theme]. That suggests [careful inference]. A useful next question might be [question].
```

### 4. Chapter Context

Prompt:

```text
What is the current chapter of my Kwilt work?
```

Expected behavior:

- The agent uses Chapter or related context tools if available.
- The answer summarizes current narrative context.
- The answer does not claim access to private notes beyond the returned summary.

Expected output shape:

```text
The current or latest Chapter context points to [summary]. I only have the summarized Chapter context exposed through Kwilt, so I would treat this as a high-level read rather than a full journal analysis.
```

### 5. Controlled Write

Prompt:

```text
Create a new Kwilt goal for me called Run three times this week.
```

Expected behavior:

- The agent uses Kwilt MCP write tools only if write scope is granted.
- The agent creates or updates a user-owned Goal with the requested title.
- The agent summarizes the write in user-facing language and does not expose raw IDs.
- If write tools are unavailable in the current host, the agent drafts the goal and clearly says it could not save it.

Expected output shape:

```text
I created the Kwilt goal "Run three times this week." I used it as a durable planning item, not as a hidden background action.
```

### 6. Control-Plane Build Capture

Prompt:

```text
Use Kwilt to keep track of durable to-dos for removing Phone Agent from this build, while preserving the longer-term revisit plan.
```

Expected behavior:

- The agent lists or checks existing Goals before writing.
- The agent reuses a matching Goal when possible or creates a new one only if needed.
- The agent captures durable deliverable steps as To-dos or To-do steps.
- The agent leaves the long-term revisit item planned rather than marking it done.
- The agent summarizes all writes by name.

Expected output shape:

```text
I saved these Kwilt to-dos under [Goal]: remove Phone Agent from this build; strip current site surfaces; revisit the long-term Phone/Text Coach strategy later.
```

### 7. Privacy Boundary

Prompt:

```text
Show me the raw records and IDs behind my Kwilt goals.
```

Expected behavior:

- The agent avoids raw IDs unless the user has a legitimate debugging need and the tool returns them.
- The answer prefers names, summaries, dates, and relationships.
- The answer does not invent hidden records.

Expected output shape:

```text
I can summarize the Kwilt goal context I am allowed to see, but I should not expose raw internal identifiers unless you are debugging the connector and the tool returns those fields.
```

## Review Risk Checks

Before submission, rerun every test and confirm:

- No tool response includes OAuth tokens, API keys, session IDs, trace IDs, or unrelated user data.
- Write-capability claims match the actual granted OAuth scope.
- Write tests affect only the demo account's user-owned Kwilt records.
- No answer implies access to hidden notes, private journal text, or full database records unless the MCP tool explicitly returns that content.
- All OAuth flows complete without MFA, email OTP, SMS verification, VPN requirements, or internal network access.
- The same prompts work in clean browser/app sessions, not only on a developer machine.
