---
name: kwilt
description: Use when the user asks about their Kwilt Arcs, Goals, Activities, Chapters, show-up status, life-planning context, identity work, personal goals, or what they are building in Kwilt.
---

# Kwilt

Kwilt is a personal life-coaching system organized around Arcs, Goals, Activities, Chapters, and show-up status. Use only the Kwilt MCP tools exposed in the current session; if a host has not refreshed the full hosted tool surface yet, say which context types are unavailable instead of inventing details.

## Use Kwilt Context

When the user asks about their Kwilt context, use the Kwilt MCP tools before answering from memory.

Prefer this read order:

1. Start with `get_current_account` when account identity matters.
2. Use `list_arcs` to understand the user's high-level identity arcs when that tool is available.
3. Use `list_goals` to find active or relevant goals.
4. Use `list_recent_activities` when recency, momentum, or current behavior matters.
5. Use `get_arc` or `get_goal` when the user asks about a specific item or when a listed item needs more context.
6. Use Chapter or show-up tools when the question is about narrative, reflection, streak, or recent continuity.

## Response Style

- Summarize in user-facing language, not database terminology.
- Treat Kwilt data as personal context, not generic task data.
- Preserve uncertainty. If Kwilt exposes only summaries, do not imply access to private notes or hidden fields.
- Prefer "what this suggests" over overconfident coaching claims.
- If there is little or no data, say that clearly and suggest the smallest useful next question.

## Safety

This skill is read-first and context-focused. Use `kwilt-control-plane` for durable Goal and To-do writes during agent build work.

Do not create, edit, or delete Kwilt data as part of a context-summary answer unless the user explicitly asks for a write and the current client exposes the relevant Kwilt MCP write tools.

Do not reveal raw IDs unless the user asks for debugging details. Prefer names, summaries, dates, and relationships that help the user reason about their goals.
