# Execution Constraints

Use this file before editing code.

## Execution contract

Before editing, produce a short plan:

- Selected issue:
- Priority:
- Evidence:
- Confidence:
- Execution risk:
- Files likely to change:
- Validation command:

Then make the smallest safe change that solves the selected issue.

## Allowed safe changes

Usually safe:

- Add loading/error/empty/retry UI to an existing screen.
- Prevent duplicate submit with disabled/submitting state.
- Add debounce/throttle to search or rapid-input API calls.
- Add request cancellation or stale response guard.
- Extract repeated API logic into an existing service/hook pattern.
- Add cache invalidation/refetch using existing project tooling.
- Add component-level fallback or framework-supported error boundary.
- Add missing tests following an existing test pattern.

## Requires approval

Ask/report before doing:

- New dependency installation.
- Large folder restructure.
- State-management migration.
- API contract change.
- Backend change.
- Database/schema migration.
- Auth/payment/billing/permissions behavior change.
- Major design-system migration.
- Replacing the router or data-fetching architecture.
- Broad rewrite across many unrelated files.

## Do not do

- Do not rewrite the whole app.
- Do not fix unrelated P2/P3 issues while fixing P0/P1.
- Do not rename public exports/components without checking usage.
- Do not remove existing validation, auth, or error handling unless replacing it with an equal or safer pattern.
- Do not hide failing validation by loosening types, disabling lint rules, or deleting tests.
- Do not change environment variables or deployment config unless asked.

## After editing

Always:

- Summarize changed files.
- Explain why the fix solves the issue.
- Run validation when commands are available.
- Report validation failures honestly.
- Identify remaining risks.
