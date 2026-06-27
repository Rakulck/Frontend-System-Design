# Priority Classification Rules

Use this file to classify findings consistently.

## P0 — Critical

Use P0 when the issue can cause:

- Production downtime or app crash in a core route/screen.
- Blank UI for a core user flow when an API fails.
- Data loss or lost user input.
- Duplicate critical writes: payment, booking, checkout, account change, upload, generation credit use.
- Broken auth, billing, permissions, or payment flow.
- Unsafe sensitive-data exposure.
- Core onboarding, checkout, dashboard, generation result, upload, or navigation failure.

P0 fixes should be small and targeted. If they require backend or product decisions, stop and report.

## P1 — High

Use P1 when the issue significantly hurts:

- Reliability under API failure or slow network.
- Performance under normal traffic.
- API traffic due to repeated requests, no debounce, unbounded polling, or waterfall calls.
- UX for important screens because loading/error/empty/retry states are missing.
- Scalability of data fetching, caching, or mutation behavior.
- Mobile reliability: offline, backgrounding, upload retry, network transitions.

P1 fixes are reasonable in execute mode when requested.

## P2 — Medium

Use P2 for:

- Maintainability problems.
- Duplicated API or UI logic that is not immediately risky.
- Inconsistent folder structure.
- Mixed visual and business logic in large components.
- Design-system inconsistency.
- Missing tests for non-critical flows.
- State boundaries that will slow future development but do not currently break user flows.

P2 fixes usually need user approval unless the user asks for refactoring.

## P3 — Low

Use P3 for:

- Naming cleanup.
- Minor consistency improvements.
- Small polish.
- Non-critical component extraction.
- Nice-to-have optimization.

Do not spend execution time on P3 unless asked.

## Severity escalators

Raise severity when the issue affects:

- Auth/session
- Billing/payment
- Checkout/booking
- Onboarding
- Search/discovery
- Uploads
- Generated results
- User profile/preferences
- Notifications or realtime progress
- Core dashboard or home screen

## Severity reducers

Lower severity when:

- The affected screen is non-core.
- There is already a fallback.
- Issue is isolated to internal/admin-only UI.
- The problem is cosmetic or naming-only.
- Evidence is weak.
