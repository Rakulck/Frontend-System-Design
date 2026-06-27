# API and Data Layer Playbook

## Inspect

- Where API calls live.
- Whether visual components directly own transport logic.
- Whether request helpers are duplicated.
- Whether responses are typed/validated.
- Whether errors are normalized.
- Whether auth headers/session are handled safely.
- Whether requests can timeout, cancel, retry, or ignore stale responses when needed.
- Whether repeated screens call the same endpoint independently.

## Failure patterns

- Fetching inside render/effect without dependency control.
- Same API call duplicated across components.
- UI assumes successful response shape.
- Silent catch blocks.
- Errors shown as blank screen.
- Auth errors handled inconsistently.
- Race condition: older response overwrites newer response.

## Priority rules

- P0: core screen blanks/crashes on API failure; auth/payment/core data silently fails; stale response corrupts critical UI.
- P1: duplicated important API calls, missing error handling on important screens, repeated traffic, no cancellation for search.
- P2: API logic mixed with UI but currently stable; inconsistent helpers.
- P3: naming or minor organization cleanup.

## Safe fixes

- Reuse or create a small API helper consistent with the project.
- Normalize errors.
- Add typed response handling when the stack supports it.
- Add stale response guards or cancellation.
- Add loading/error/retry UI.
- Add debounce for rapid inputs.

## Requires approval

- Backend contract changes.
- New data-fetching library.
- API route restructuring.
- Auth/session handling change.
