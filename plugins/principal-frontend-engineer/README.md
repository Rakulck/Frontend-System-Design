# Principal Frontend Engineer

A Claude Code marketplace plugin for analyzing, improving, and validating frontend codebases like a principal frontend engineer.

It is **framework-agnostic in analysis** and **framework-aware in execution**. It first detects the existing stack, architecture, routing, API/data layer, state management, styling system, and validation commands, then produces a priority-ranked report or applies selected fixes safely.

## Install

After pushing this repository to GitHub, users can install it with Claude Code's plugin marketplace commands.

Replace `YOUR_GITHUB_USERNAME` with your GitHub username or organization:

```bash
claude plugin marketplace add YOUR_GITHUB_USERNAME/principal-frontend-engineer
claude plugin install principal-frontend-engineer@principal-frontend-engineer
```

Optional project-shared install:

```bash
claude plugin marketplace add YOUR_GITHUB_USERNAME/principal-frontend-engineer --scope project
claude plugin install principal-frontend-engineer@principal-frontend-engineer --scope project
```

Inside Claude Code, reload plugins if already in a session:

```text
/reload-plugins
```

## Local testing before publishing

From the parent directory of this repo:

```bash
claude plugin validate ./principal-frontend-engineer
claude plugin validate ./principal-frontend-engineer/plugins/principal-frontend-engineer
claude plugin marketplace add ./principal-frontend-engineer
claude plugin install principal-frontend-engineer@principal-frontend-engineer
```

Or test the plugin directly without marketplace install:

```bash
claude --plugin-dir ./principal-frontend-engineer/plugins/principal-frontend-engineer
```

## Usage

Analyze only:

```text
/principal-frontend-engineer:frontend-system-design analyze this codebase. Do not modify code.
```

Fix critical/high-priority issues only:

```text
/principal-frontend-engineer:frontend-system-design fix P0 and P1 issues only. Keep changes small and validate after edits.
```

Validate latest changes:

```text
/principal-frontend-engineer:frontend-system-design validate the latest frontend changes.
```

## What it does

Principal Frontend Engineer reviews and improves frontend system design across:

- API handling and data fetching
- Caching, stale data, and cache invalidation
- Mutation/write-flow safety
- Loading, error, empty, retry, and fallback states
- State management boundaries
- Performance and traffic handling
- Auth, security, and sensitive data handling
- Reusable components and folder structure
- Testing, validation, and production readiness

## Modes

The plugin is built around one skill and three focused agents.

```text
Skill: frontend-system-design
  Orchestrates the workflow and decides whether to analyze, execute, or validate.

Agents:
  frontend-auditor
    Read-only analysis. Produces the grounded priority report.

  frontend-executor
    Implements selected fixes safely. Preserves existing stack and patterns.

  frontend-validator
    Runs checks and verifies that changes did not break build, tests, or key flows.
```

## Safety layer

The skill includes explicit constraints to prevent broad or hallucinated changes:

- Evidence required for every finding
- Confidence levels: High, Medium, Low
- Execution risk labeling
- Stop conditions before risky edits
- No broad rewrites by default
- No dependency additions without approval
- No backend/API/auth/payment/database/deployment changes unless explicitly requested
- Concept-specific playbooks for API, caching, mutations, state, reliability, performance, security, components, and validation

## Priority levels

```text
P0 — Critical
Can cause production downtime, blank UI, data loss, broken auth/payment, broken core flow, duplicate critical writes, or unsafe sensitive-data behavior.

P1 — High
Major reliability, performance, scalability, traffic, or UX risk.

P2 — Medium
Maintainability, architecture, design-system, or code-quality issue that will slow future development.

P3 — Low
Cleanup, naming, small consistency issue, polish, or nice-to-have optimization.
```

## Framework support

Strong target support:

- React
- Next.js
- React Native / Expo

General framework-aware support:

- Flutter
- Vue
- Angular
- Svelte
- Blazor
- ASP.NET MVC / Razor frontend views
- .NET backend + frontend/API boundary

The skill should not force React, Next.js, React Query, Tailwind, Zustand, Redux, Riverpod, Bloc, or any other tool unless the codebase already uses it or the user explicitly asks for a migration.

## Repository structure

```text
principal-frontend-engineer/
  .claude-plugin/
    marketplace.json
  plugins/
    principal-frontend-engineer/
      .claude-plugin/
        plugin.json
      skills/
        frontend-system-design/
          SKILL.md
          references/
            grounding-and-scope.md
            priority-classification.md
            execution-constraints.md
            framework-adapters.md
            api-data-layer.md
            caching-strategy.md
            mutation-write-flow.md
            state-management.md
            ui-reliability.md
            performance-traffic.md
            security-auth.md
            component-architecture.md
            validation-gates.md
      agents/
        frontend-auditor.md
        frontend-executor.md
        frontend-validator.md
  README.md
  LICENSE
  CHANGELOG.md
```

## Development notes

This marketplace intentionally avoids sample private repo outputs in the MVP. Test it on real repositories locally, then improve the skill based on failure cases.

Best iteration loop:

```text
Run audit → inspect weak findings → improve SKILL.md/references/agents → run again on a fresh repo → repeat.
```

## npm / npx installer note

An npm package is optional later. The recommended launch path is the native Claude Code plugin marketplace because it supports marketplace discovery, versioning, and plugin updates directly.
