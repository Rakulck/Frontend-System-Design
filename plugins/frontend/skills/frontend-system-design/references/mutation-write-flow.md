# Mutation and Write Flow Playbook

## Inspect

- Forms and submit handlers.
- File/image upload flows.
- Payment, booking, checkout, generation, profile, auth, and settings writes.
- Duplicate submit prevention.
- Client validation.
- Server confirmation and error handling.
- Optimistic update and rollback behavior.
- Cache invalidation/refetch after success.

## Failure patterns

- Button can be clicked multiple times.
- User input lost after failure.
- Success UI shown before server confirmation for critical writes.
- Optimistic update without rollback.
- Upload has no progress/retry/cancel.
- Mutation errors swallowed.
- Cache not updated after mutation.

## Priority rules

- P0: duplicate payment/booking/checkout/generation credit/account change; data loss; broken auth write.
- P1: important form has no error/retry/submitting state; cache not invalidated after important write.
- P2: inconsistent form patterns; duplicated mutation logic.
- P3: minor button/message polish.

## Safe fixes

- Add `isSubmitting`/disabled state.
- Preserve form input on failure.
- Add success/error handling.
- Refetch or invalidate affected data.
- Use optimistic UI only when safe and reversible.
- Add upload progress/retry/cancel if project patterns support it.

## Requires approval

- Backend idempotency contract.
- Payment/billing/auth behavior changes.
- Database schema or API changes.
