# Validation Gates

Use this file after execution or when validating only.

## Detect commands

Inspect:

- `package.json` scripts
- `pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`, `bun.lockb`
- README instructions
- CI config
- `pubspec.yaml`
- `*.csproj`, solution files

## Prefer least risky checks

Run available commands in this order when relevant:

1. Lint
2. Typecheck/analyze
3. Unit tests
4. Build
5. Framework-specific tests

Examples:

- npm: `npm run lint`, `npm run typecheck`, `npm test`, `npm run build`
- pnpm: `pnpm lint`, `pnpm typecheck`, `pnpm test`, `pnpm build`
- yarn: `yarn lint`, `yarn typecheck`, `yarn test`, `yarn build`
- bun: `bun run lint`, `bun test`, `bun run build`
- Flutter: `flutter analyze`, `flutter test`
- .NET: `dotnet build`, `dotnet test`

## Do not run

- Deploy commands
- Database migrations
- Destructive scripts
- Production data scripts
- Package installation unless approved
- E2E suites that require external services unless clearly configured and safe

## Reporting

Return:

- Commands run
- Passed checks
- Failed checks
- Whether failure appears related to your changes
- Fix verification
- Remaining risk
- Next recommended step

If validation fails due to unrelated existing errors, say so and do not hide or weaken checks.
