# Security and Auth Playbook

## Inspect

- Tokens, API keys, secrets, and env usage.
- localStorage/sessionStorage/AsyncStorage/SecureStore usage.
- Frontend-only auth/permission checks.
- Route protection.
- Sensitive data in logs, analytics, error messages, or URLs.
- API boundary assumptions.

## Failure patterns

- Secret hardcoded in frontend.
- Sensitive token stored in unsafe storage.
- UI hides action but backend is not protected.
- PII logged to console/analytics.
- Auth errors treated as generic UI failure.
- Payment/billing state trusted only from frontend cache.

## Priority rules

- P0: exposed secret/token/PII, broken auth/payment permission boundary.
- P1: inconsistent route protection or sensitive data logged in important flows.
- P2: security handling is scattered but not immediately exposed.
- P3: minor cleanup.

## Safe fixes

- Remove unsafe console logs without exposing values.
- Add frontend guard only as UX support, not security source of truth.
- Improve auth error handling.
- Move sensitive values away from unsafe client storage when existing safer pattern exists.

## Requires approval

- Backend permission change.
- Auth provider/session architecture change.
- Payment/billing behavior change.

## Rule

Frontend security is not the source of truth. Never claim that hiding a button or client-side route guard secures backend access.
