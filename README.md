# Principal Frontend Engineer

A Claude Code marketplace plugin for analyzing, improving, and validating frontend codebases like a principal frontend engineer.

It is **framework-agnostic in analysis** and **framework-aware in execution**. It first detects the existing stack, architecture, routing, API/data layer, state management, styling system, and validation commands, then produces a priority-ranked report or applies selected fixes safely.

## Installation

### Claude Code Marketplace Install

```bash
claude plugin marketplace add Rakulck/Frontend-System-Design
claude plugin install principal-frontend-engineer@principal-frontend-engineer
```

Then inside Claude Code:

```text
/reload-plugins
```

### Direct Claude Skill Usage

This repo also includes a root-level open skill folder:

```text
frontend-system-design/
  SKILL.md
  references/
```

This is useful for SkillsMP discovery and manual Claude.ai skill upload.

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

Fix selected issues:

```text
/principal-frontend-engineer:frontend-system-design fix P0 and P1 issues only. Keep changes small and validate after edits.
```

Validate:

```text
/principal-frontend-engineer:frontend-system-design validate the recent frontend changes.
```

## Permissions

This skill is safe by default. It only pre-approves read-only tools:

* Read
* Grep
* Glob

Execution actions such as editing files, running build commands, installing packages, changing architecture, or modifying project behavior should require explicit user intent and Claude Code permission.

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

## Safety and Anti-Hallucination Rules

* Every finding must include codebase evidence.
* Low-confidence issues should not be executed without user approval.
* The skill should not assume frameworks, libraries, APIs, or files.
* The skill should not recommend new dependencies unless necessary and approved.
* The skill should not modify backend contracts, database schema, auth, billing, payment, or deployment logic unless explicitly requested.
* The skill should not broaden the task beyond the user’s requested scope.

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

## Supported Frameworks

Strongest support:

* React
* Next.js
* React Native
* Expo
* Flutter

General support:

* Vue
* Nuxt
* Angular
* Svelte
* Blazor
* Razor / ASP.NET frontend views

The skill is framework-aware, not framework-forcing. It detects the existing stack first.

## Repository structure

```text
principal-frontend-engineer/
  .claude-plugin/
    marketplace.json
  frontend-system-design/
    SKILL.md
    references/
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
