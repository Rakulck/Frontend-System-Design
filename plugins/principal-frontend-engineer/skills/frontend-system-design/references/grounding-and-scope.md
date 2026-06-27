# Grounding and Scope Rules

Use this reference before analysis or execution. Its purpose is to prevent broad, hallucinated, or unsafe frontend changes.

## Evidence rules

Every finding must be grounded in at least one of these:

- A specific file path and code pattern.
- A manifest/config signal such as `package.json`, `pubspec.yaml`, `*.csproj`, lockfile, config file, or CI file.
- A repeated pattern across multiple files.
- A missing project-level construct that can be reasonably verified, such as no validation command, no error boundary, no shared API helper, or no loading/error state in inspected core screens.

Do not claim issues without evidence. If evidence is incomplete, write: **Not enough evidence found**.

## Confidence levels

- **High:** directly confirmed from code or project files.
- **Medium:** strongly inferred from multiple files or project patterns.
- **Low:** possible issue, but evidence is incomplete.

Do not execute Low-confidence fixes without user approval.

## Scope rules

Do not expand the task beyond the user's request.

Examples:

- If the user asks to fix caching, do not redesign folder structure.
- If the user asks to fix P0 issues, do not fix P2 cleanup.
- If the user asks for analyze-only, do not edit files.
- If a broader issue is discovered, report it under recommendations instead of fixing it.

## Stop conditions

Stop and report instead of editing when:

- Framework or project boundary cannot be confidently detected.
- Required dependency is missing and adding it was not approved.
- Fix requires backend/API contract changes.
- Fix requires database/schema changes.
- Fix affects auth, billing, payment, permissions, or production deployment behavior.
- Fix requires a broad migration or folder restructure.
- Validation fails due to unrelated existing errors.
- The user requested audit/report/analyze-only mode.

## Dependency rules

- Do not add new libraries by default.
- Prefer existing project tools and conventions.
- If a new dependency would materially improve the fix, present it as an option with tradeoffs.
- Never assume React Query, SWR, Redux, Zustand, Riverpod, Bloc, Tailwind, Axios, or any framework-specific package exists.

## Privacy and sensitive data rules

- Do not print secrets, tokens, private keys, auth headers, customer data, or environment variable values.
- Do not recommend storing secrets in frontend code.
- Do not log sensitive data as part of debugging.
- If sensitive data is discovered, report the risk without exposing the value.

## Change-size rules

Prefer fixes that are:

- Small
- Local
- Reversible
- Reviewable
- Consistent with existing project patterns

If the best fix is large, write a plan and ask for explicit execution approval.
