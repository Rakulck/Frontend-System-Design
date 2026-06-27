# UI Reliability Playbook

## Inspect

For every major data screen, check:

- First-load state.
- Background loading state.
- Empty state.
- Error state.
- Retry action.
- Partial success state.
- Last-known-good-data fallback.
- Component-level failure isolation.
- Route-level error boundary where supported.

## Failure patterns

- API failure creates blank screen.
- Whole page blocked during background refetch.
- No retry path.
- Empty state looks like loading or failure.
- Error in one widget crashes entire screen.
- Cached data discarded during refetch.

## Priority rules

- P0: core screen can blank/crash with no recovery.
- P1: important screen has poor slow-network or error UX.
- P2: inconsistent loading/error state patterns.
- P3: copy/polish improvements.

## Safe fixes

- Add skeleton/loader for first load.
- Add error state with retry.
- Add empty state.
- Keep previous data visible during background refresh.
- Add component-level fallback or route-level error boundary where framework supports it.

## Requires approval

- Major route/layout restructure.
- Product/design decisions for complex empty/error states.
