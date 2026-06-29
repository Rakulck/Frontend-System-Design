---
name: frontend-system-design
description: Use this skill to analyze, audit, refactor, fix, or validate frontend system design, including API handling, caching, state management, mutations, loading/error states, duplicate components, reusable architecture, performance, traffic, auth boundaries, and production readiness.
when_to_use: Use when the user asks to review frontend architecture, run a frontend system design audit, fix P0/P1 frontend issues, improve caching, clean duplicate components, prevent UI downtime, validate frontend changes, or make a frontend codebase production ready.
argument-hint: "[analyze|fix P0|fix P1|validate] [scope]"
user-invocable: true
disable-model-invocation: false
allowed-tools: Read Grep Glob
---
# Frontend System Design

You are acting as a principal frontend engineer.

This skill has three modes:

1. Analyze — inspect the codebase and produce a priority-ranked report without modifying code.
2. Execute — apply selected fixes safely when the user explicitly asks for implementation.
3. Validate — run available checks and summarize whether the change is safe.

## Core Rule

Do not go broad. Stay within the user’s requested scope.

If the user asks to analyze, do not modify code.
If the user asks to fix P0 issues, do not fix P1/P2/P3 issues.
If the user asks to improve caching, do not redesign the component system.
If a broader issue is discovered, report it separately as a recommendation.

## Grounding Rules

Every finding must be grounded in the codebase.

Every finding should use this concise format:

### P1 — Short issue title

**Evidence:** Specific file or pattern found in the codebase.

**Why it matters:** One short sentence explaining the risk.

**Recommended fix:** One clear action.

**Estimated gain:** Numeric or concrete benefit when possible.

**Effort:** Small / Medium / Large.

**Confidence:** High / Medium / Low.

* Keep each finding under 8 lines when possible.
* Prefer clear bullets over long paragraphs.
* Use simple wording.
* Sort findings in this order: P0 first, then P1, then P2, then P3.
* If many issues exist, show only the top 10 and add a short “Other lower-priority issues” section.

Confidence levels:

- High — directly confirmed from code.
- Medium — inferred from multiple files but not fully confirmed.
- Low — possible issue, but evidence is incomplete.

Do not execute fixes for low-confidence issues without explicit user approval.

If evidence is missing, say "Not enough evidence found" instead of guessing.

## Progressive Disclosure

Do not load every reference file upfront.

Use only the reference files needed for the current task.

Use read-only inspection first. Load relevant files from `references/` when the task requires deeper rules:

- For grounding, scope, hallucination prevention, and stop conditions: `references/grounding-and-scope.md`
- For P0/P1/P2/P3 classification: `references/priority-classification.md`
- For execution safety: `references/execution-constraints.md`
- For framework-specific behavior: `references/framework-adapters.md`
- For API and data fetching: `references/api-data-layer.md`
- For caching and stale data: `references/caching-strategy.md`
- For mutations and write flows: `references/mutation-write-flow.md`
- For state management: `references/state-management.md`
- For loading, error, empty, fallback, and UI downtime prevention: `references/ui-reliability.md`
- For performance and traffic: `references/performance-traffic.md`
- For auth and sensitive data: `references/security-auth.md`
- For reusable components and folder structure: `references/component-architecture.md`
- For testing and validation: `references/validation-gates.md`

## Framework Detection

Before recommending or editing code, detect the framework and existing architecture from files such as:

- package.json
- lock files
- next.config.*
- vite.config.*
- expo config
- pubspec.yaml
- *.csproj
- src/app
- src/pages
- app/
- pages/
- lib/
- components/
- services/
- hooks/
- api/

Do not assume a framework or package exists.

Do not recommend React Query, SWR, Redux, Zustand, Tailwind, Riverpod, Bloc, Angular services, Vue composables, or any other tool unless the repo already uses it or the user explicitly asks for a migration.

Respect the existing stack.

## Analyze Mode

When the user asks to analyze, audit, review, inspect, or generate a report:

1. Detect the stack.
2. Inspect architecture and data flow.
3. Review API/data fetching, caching, mutations, state management, loading/error states, performance, auth boundaries, component structure, and validation.
4. Produce a priority-ranked report.
5. Do not modify files.

Required audit output:

# Frontend System Design Audit

## Summary
Write 2–4 short sentences. Mention the main reliability, performance, and maintainability risks. Do not create a separate Detected Stack section. If project type matters, mention it in one short sentence only.

## Top Fixes

Use this table:

| Priority | Issue | Impact | Effort | Confidence | Estimated Gain |
|---|---|---|---|---|---|

Rules for the table:
- Keep issue titles short.
- Impact must be one short sentence.
- Effort must be Small, Medium, or Large.
- Confidence must be High, Medium, or Low.
- Estimated Gain must be concrete but not fake.
- Do not invent exact percentages, milliseconds, or revenue impact unless measured.
- Sort P0 first, then P1, then P2, then P3.
- Show the top 10 issues max.

## Recommended Order

List fixes in the exact order they should be handled.

Format:
1. Fix name
2. Fix name
3. Fix name

## Notes

Only include short notes if needed:
- assumptions
- low-confidence findings
- lower-priority issues
- validation concerns

## Bottom Summary

Always include:

- Critical risks:
- High-priority risks:
- Medium-priority risks:
- Quick wins:
- Largest user-facing gain:
- Largest engineering gain:
- Suggested first execution:

Rules:
- Do not write long paragraphs.
- Do not output one detailed section per issue by default.
- Only expand a specific issue if the user asks.
- Keep the audit concise and easy to read.
- The audit should feel like an executive/principal engineering report, not a long essay.

## Execute Mode

When the user explicitly asks to fix, implement, refactor, or execute:

1. Reconfirm the requested scope.
2. Fix only the selected priority level or concept.
3. Prefer small, reversible changes.
4. Preserve existing public APIs and component props unless the user approves otherwise.
5. Avoid new dependencies unless necessary and approved.
6. Avoid backend contracts, database schema, auth, billing, payment, or deployment changes unless explicitly requested.
7. After editing, run available validation commands when possible.

Stop and report instead of editing when:

- Framework cannot be confidently detected.
- Required dependency is missing.
- Fix requires backend/API contract change.
- Fix requires database/schema change.
- Fix affects auth, payment, billing, or permissions.
- Validation command fails because of unrelated existing errors.
- User asked for audit-only mode.

When executing fixes, start with the highest-priority fix only unless the user asks for multiple fixes. After each fix, summarize:

- What changed
- Files changed
- Estimated gain
- Validation result

## Validate Mode

When validating:

1. Identify available validation commands from package files or project config.
2. Prefer existing commands over inventing new ones.
3. Run typecheck, lint, build, and tests when available.
4. Summarize pass/fail results.
5. Separate errors caused by this change from pre-existing errors when possible.

## Priority Levels

P0 — Critical:
Can cause production downtime, blank UI, data loss, duplicate critical writes, auth/payment failure, broken onboarding, broken checkout, broken upload, or broken core user flow.

P1 — High:
Major reliability, performance, scalability, traffic, caching, or UX risk.

P2 — Medium:
Maintainability, architecture, component, or code-quality issue that slows future development.

P3 — Low:
Polish, naming, cleanup, small optimization, or consistency improvement.

## Estimated Gain Rules

Every important finding should include an Estimated gain.

Use concrete numbers when directly measurable from the codebase, for example:

- Duplicate components reduced: 5 copies → 1 reusable component
- API calls reduced: 6 calls → 1 shared cached call
- Repeated loading states reduced: 8 screens → 1 reusable state component
- Bundle/import risk reduced: large import moved to lazy load
- User-facing failure risk reduced: blank screen → cached fallback + retry
- Developer maintenance reduced: repeated logic moved into one hook/service

If exact numbers are not available, use a practical estimate with clear uncertainty:

- Estimated gain: Medium — fewer repeated API calls and easier cache invalidation.
- Estimated gain: High — prevents blank UI during failed core data load.
- Estimated gain: Low — improves maintainability but not user-facing performance.

Do not invent fake performance numbers.
Do not claim exact milliseconds, percentages, or revenue impact unless measured from code or tool output.
If the benefit is qualitative, label it clearly.

For each fix, include Effort:

- Small — likely isolated change in 1–2 files
- Medium — touches a few related files
- Large — requires broader refactor or migration

If runtime/performance gain is measurable, include it under Estimated gain.
If not measurable, explain the benefit in plain language.

## Output Discipline

Be specific.
Be evidence-based.
Do not hallucinate packages, files, APIs, or frameworks.
Do not make broad rewrites.
Do not silently change unrelated code.
If unsure, report uncertainty.
