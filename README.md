# Principal Frontend Engineer

A Claude Code skill for analyzing, improving, and validating frontend codebases like a principal frontend engineer.

It is **framework-agnostic in analysis** and **framework-aware in execution**. It first detects the existing stack, architecture, routing, API/data layer, state management, styling system, and validation commands, then produces a priority-ranked report or applies selected fixes safely.

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

### Modes

This is built around one primary skill and three focused agents.

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

### Priority levels

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

## One-line install with Claude Code

Open Claude Code from your project root and paste this:

```text
Install the Frontend System Design skill from https://github.com/Rakulck/Frontend-System-Design into this project’s .claude/skills folder, using the skill located at plugins/frontend/skills/frontend-system-design, then verify that .claude/skills/frontend-system-design/SKILL.md exists. After installation, show me this message: “Frontend System Design skill installed. Next step: run an audit with: /frontend-system-design analyze this codebase. Do not modify code.”
```

```text
/frontend-system-design analyze this codebase. Do not modify code.
```

## Open Skill Install

This is the primary and recommended way to use this skill. 

**Project Install (Recommended)**  
Copy the `frontend-system-design/` folder into your project's `.claude/skills/` directory.

**Global Install**  
Copy the `frontend-system-design/` folder into your global Claude skills directory: `~/.claude/skills/`

## Claude.ai Upload

Zip the `frontend-system-design/` folder so the zip contains the skill folder as its root, then upload it through Claude.ai Skills settings.

## Claude Code Plugin Install

*Important: these are Claude Code slash commands, not terminal commands.*

Use this exact one-line install command:

```text
/plugin marketplace add Rakulck/Frontend-System-Design && /plugin install frontend@system-design
```

Then run:

```text
/reload-plugins
```

Then usage:

```text
/frontend:frontend-system-design analyze this codebase. Do not modify code.
```

## Usage examples

Analyze only:

```text
/frontend:frontend-system-design analyze this codebase. Do not modify code.
```

Fix selected issues:

```text
/frontend:frontend-system-design fix P0 and P1 issues only. Keep changes small and validate after edits.
```

Validate:

```text
/frontend:frontend-system-design validate the recent frontend changes.
```

## Permissions

This skill is safe by default. It only pre-approves read-only tools:

* Read
* Grep
* Glob

Execution actions such as editing files, running build commands, installing packages, changing architecture, or modifying project behavior should require explicit user intent and Claude Code permission.

## Safety rules

* Every finding must include codebase evidence.
* Low-confidence issues should not be executed without user approval.
* The skill should not assume frameworks, libraries, APIs, or files.
* The skill should not recommend new dependencies unless necessary and approved.
* The skill should not modify backend contracts, database schema, auth, billing, payment, or deployment logic unless explicitly requested.
* The skill should not broaden the task beyond the user’s requested scope.

## Supported frameworks

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
  plugins/
    frontend/
      .claude-plugin/
        plugin.json
      skills/
        frontend-system-design/
          SKILL.md
          references/
      agents/
        frontend-auditor.md
        frontend-executor.md
        frontend-validator.md
  README.md
  LICENSE
  CHANGELOG.md
```

## Development notes

This repository intentionally avoids sample private repo outputs in the MVP. Test it on real repositories locally, then improve the skill based on failure cases.

Best iteration loop:

```text
Run audit → inspect weak findings → improve SKILL.md/references/agents → run again on a fresh repo → repeat.
```
