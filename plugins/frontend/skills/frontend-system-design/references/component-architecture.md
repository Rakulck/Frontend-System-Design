# Component and Folder Architecture Playbook

## Inspect

- Component sizes and responsibilities.
- Repeated UI patterns.
- Business/data logic inside visual components.
- Shared primitives vs feature components.
- Folder/module boundaries.
- Styling consistency.
- Design-system tokens/components.

## Failure patterns

- Large component owns fetching, business logic, rendering, forms, and styling.
- Same loading/error/card/table patterns duplicated everywhere.
- Random one-off styling without shared primitives.
- Feature logic spread across unrelated folders.
- Public component API is unstable or unclear.

## Priority rules

- P0: component/folder issue directly causes core failure. Rare.
- P1: architecture causes repeated production bugs in important flows.
- P2: maintainability/scalability problem.
- P3: naming/polish.

## Safe fixes

- Extract small presentational component when duplication is clear.
- Move data logic into existing service/hook/composable pattern.
- Keep feature-level organization consistent.
- Preserve component props/public API unless local.

## Requires approval

- Full folder restructure.
- Design-system migration.
- Styling library migration.
- Breaking public component APIs.
