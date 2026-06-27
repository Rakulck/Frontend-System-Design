# Caching Strategy Playbook

## Inspect

- Whether data is cached anywhere.
- Which library or pattern is already used: React Query, SWR, Apollo, RTK Query, custom cache, Next fetch cache, local storage, AsyncStorage, Riverpod/Bloc cache, etc.
- Whether same request is duplicated.
- Whether mutations invalidate/refetch affected data.
- Whether critical data is incorrectly cached.
- Whether last-known-good data is available for repeat loads.

## Data classes

- Static/reference: can cache longer.
- User profile/preferences: cache but refresh on app/session start and after edits.
- Feed/list/search: cache briefly, paginate, background refresh.
- Critical fresh: auth, payment, permissions, inventory, availability; avoid stale decisions.
- Generated/persistent results: persist immediately, reload safely.

## Failure patterns

- No cache for expensive repeated data.
- Cache exists but never invalidates after mutation.
- Stale data shown as truth for critical flows.
- Cache key does not include filters/user/context.
- Refetch loops.
- Full screen blank while refetching despite usable cached data.

## Priority rules

- P0: stale cache can show wrong payment/auth/permission/critical result state.
- P1: repeated API calls or no invalidation causes significant UX/performance issue.
- P2: cache keys/invalidation are inconsistent but not core-flow breaking.
- P3: minor cache cleanup.

## Safe fixes

- Use existing caching tool.
- Add request deduping.
- Add invalidation/refetch after mutation.
- Keep last-known-good data while refreshing.
- Correct cache keys to include user/filter/context.

## Requires approval

- Introducing a new caching library.
- Changing freshness behavior for payment/auth/permissions.
- Adding persistent offline cache for sensitive data.
