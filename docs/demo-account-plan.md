# Demo Account Plan

Reviewers need a stable OAuth account that demonstrates Kwilt context without exposing a real user's private data.

## Account Requirements

- Dedicated reviewer account, not a personal or production user account.
- No MFA, SMS, email OTP, VPN, or internal allowlist requirement.
- Password or OAuth credentials should remain valid throughout review.
- Account should be clearly labeled internally as a demo/reviewer account.
- Account should have access only to seeded demo data.

## Seeded Data

Create stable, non-sensitive data that exercises every context tool and leaves room for controlled write tests.

Suggested fixture:

- Account identity:
  - A dedicated reviewer/demo account with a non-personal email address.
- Arc: `Creative Practice`
  - Goal: `Publish one short reflection each week`
  - Goal: `Collect three examples of work that feels alive`
- Arc: `Steady Body`
  - Goal: `Run three times this week`
  - Goal: `Protect two early nights`
- Arc: `Deep Work`
  - Goal: `Finish the agent plugin submission packet`
- Recent To-dos:
  - `Drafted submission checklist`
  - `Reviewed current goals`
  - `Logged a run`
  - `Reflected on weekly focus`
  - `Updated chapter notes`
- Chapter summary:
  - `A week about turning scattered ambition into a small repeatable rhythm.`
- Show-up status:
  - A short streak or latest show-up summary with no private journal text.
- Write-test workspace:
  - Goal: `Agent plugin verification`
  - To-do: `Verify control-plane write capture`
  - To-do: `Revisit Phone Agent strategy after removal`
  - To-do step: `Confirm OpenAI submission packet matches live MCP tools`

## Reviewer Credential Handling

Store the actual demo credentials outside this public repository. For each submission form, provide credentials only through the platform's secure reviewer credential fields.

Do not commit:

- Passwords
- OAuth client secrets
- Access tokens
- Refresh tokens
- Supabase service role keys
- Personal user exports

## Reset Procedure

Before each submission or resubmission:

1. Confirm the account can sign in from a clean browser profile.
2. Revoke any stale OAuth grants from previous tests.
3. Reconnect through the target client.
4. Run all prompts in `docs/reviewer-test-plan.md`.
5. Archive or reset controlled write-test items if a test client creates duplicates.
6. Restore seeded data if any internal testing changed it.

## Success Criteria

The reviewer should be able to:

- Connect Kwilt through OAuth.
- Run every prompt in `docs/reviewer-test-plan.md`.
- See useful Kwilt summaries.
- Create or update a controlled Goal, To-do, or To-do step when write scope is granted.
- Revoke access.
- Reconnect without contacting Kwilt support.
