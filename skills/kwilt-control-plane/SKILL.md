---
name: kwilt-control-plane
description: Use when coding agents are asked to build, enhance, remove, or plan features; capture roadmap or deferred follow-up work; maintain project to-dos; or keep long-running implementation work aligned with Kwilt Goals and Activities.
---

# Kwilt Control Plane

Kwilt is the durable control plane for work that should survive a single agent thread. Use the agent's native planning tools for immediate execution state, and use Kwilt Goals and Activities for durable outcomes, deferred follow-ups, and cross-thread continuity.

## When To Use

Use this skill when the user asks the agent to:

- Build a new feature or enhance an existing one.
- Remove, pause, or strip out a feature while preserving the longer-term follow-up.
- Capture roadmap, product, review, or implementation follow-up work.
- Keep track of to-dos, goals, objectives, or build steps in Kwilt.
- Continue work that could otherwise lose durable to-dos across threads.

Do not use it for tiny cosmetic edits, one-command questions, or pure explanation unless the user asks to capture follow-up work.

## Start Of Work

1. Confirm the Kwilt MCP tools are available. If they are not visible, use tool discovery for Kwilt MCP tools before assuming Kwilt is unavailable.
2. Read current Kwilt state before writing:
   - `list_goals` for planned and in-progress Goals.
   - `list_recent_activities` with rich fields when available.
   - `get_goal` for likely matching Goals.
3. Select the best matching Goal by title, description, current status, and the user's requested work.
4. Create a new Goal only when no existing Goal is a reasonable fit.
5. Use stable idempotency keys for all writes. Include the repo or project name, a short request slug, and the Goal or Activity title.

## Goal Mapping

Prefer reusing an existing Goal over creating a new one.

Create a Goal when the work represents a new durable workstream, such as a new product initiative, plugin capability, release effort, or strategic follow-up. Keep Goal titles human and product-facing.

Avoid unassigned Activities unless the user explicitly asks for loose capture or the connector lacks Goal write support.

## To-do Capture

Capture durable deliverable steps as Kwilt Activities. Do not mirror every tiny implementation checklist item.

Good Activities:

- "Add Sprint B control-plane skill to kwilt-agent-plugins"
- "Verify Kwilt MCP write path from Codex"
- "Revisit long-term Phone Agent strategy after next build removal"

Too small for Kwilt:

- "Open README"
- "Run rg"
- "Rename one local variable"

For each Activity, include concise notes that state the desired outcome, acceptance signal, and any known constraints. Use tags such as `agent-work`, `codex`, `plugin`, `follow-up`, or the repo name when useful.

## During Work

- Keep the agent's native plan/checklist as the short-lived execution surface.
- Update Kwilt only when durable deliverables change materially.
- If the user changes scope, adjust or add Activities so deferred work does not disappear.
- If a task is intentionally deferred, leave it planned and say why in the Activity notes.
- If a task is abandoned, mark it skipped or cancelled rather than deleting it.

## Completion

Before handing work back:

1. Reconcile the Kwilt Activities touched during the run.
2. Mark an Activity done only after the relevant implementation and verification have actually passed.
3. Leave long-term follow-ups planned, with clear notes.
4. Summarize Kwilt writes in the final response using names, not raw IDs, unless the user asks for debugging details.

## Safety

- Do not invent Kwilt data. If a Goal or Activity is not visible, say so.
- Do not expose raw IDs unless the user asks for connector debugging.
- Treat Kwilt data as personal planning context, not generic project-management data.
- Respect tool availability. If write tools are not exposed in the current client, draft the intended Goal or Activity for the user instead of claiming it was saved.
