# Performance and Traffic Playbook

## Inspect

- Repeated API calls.
- Fetch-on-every-render loops.
- Search/API call on every keystroke.
- Missing debounce/throttle.
- Missing pagination/virtualization.
- Large payloads.
- Waterfall requests.
- Unbounded polling.
- Heavy bundle imports.
- Unnecessary client components.
- Expensive renders.
- Oversent analytics/events.

## Failure patterns

- Effects missing dependencies or with unstable dependencies.
- Multiple components independently fetch same data.
- Full dataset loaded into table/list.
- Polling continues when screen hidden/unmounted.
- Search sends request for every character.
- Client bundle imports large libraries into core routes.

## Priority rules

- P0: traffic/performance issue breaks core flow or can take production down.
- P1: major repeated calls, unbounded polling, no pagination on large data, or visible slow UX.
- P2: moderate render or bundle inefficiency.
- P3: micro-optimization.

## Safe fixes

- Debounce/throttle rapid input.
- Add pagination/infinite loading when endpoint supports it.
- Deduplicate requests using existing tools.
- Parallelize independent requests when safe.
- Stop polling when not needed.
- Lazy load heavy non-critical components.

## Requires approval

- Backend pagination/API contract changes.
- New virtualization/data library.
- Major rendering architecture migration.
