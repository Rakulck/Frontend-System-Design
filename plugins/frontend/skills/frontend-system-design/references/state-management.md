# State Management Playbook

## Inspect

Classify state into:

- Server state: API data, lists, user profile, generated results.
- UI state: modals, tabs, drawers, filters, selected item.
- Form state: input before submission.
- Auth/session state.
- Persistent local state.
- Realtime/progress state.

Check whether state is stored in the right place.

## Failure patterns

- Server state copied into global UI store and becomes stale.
- Local UI state put into global store unnecessarily.
- Form state lost during API failure.
- Auth state scattered across files.
- Persistent state stores sensitive data unsafely.
- Realtime/progress state not reconciled with backend source of truth.

## Priority rules

- P0: state bug can corrupt core user flow, auth, payment, or generated result.
- P1: stale server state or scattered auth/session state creates reliability risk.
- P2: state boundaries are messy and slow development.
- P3: minor naming/organization cleanup.

## Safe fixes

- Keep local UI state local.
- Use existing server-state/cache tool for API data.
- Avoid copying server state unless necessary.
- Add clear source-of-truth comments or helpers when ambiguity causes bugs.
- Keep form state stable during submit/failure.

## Requires approval

- State library migration.
- Broad store restructure.
- Auth/session architecture changes.
