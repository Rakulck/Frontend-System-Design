# Principal Frontend Engineer

A Claude Code open skill and marketplace plugin for analyzing, improving, and validating frontend codebases like a principal frontend engineer.

It is **framework-agnostic in analysis** and **framework-aware in execution**. It first detects the existing stack, architecture, routing, API/data layer, state management, styling system, and validation commands, then produces a priority-ranked report or applies selected fixes safely.

## Installation

This repository serves as a direct, open Claude Code skill. No terminal installation commands are required.

### 1. Claude Code CLI Install

To install it for local command-line use with Claude Code:

1. Download or clone this repository.
2. Choose your installation scope and copy the `frontend-system-design/` folder:

**Project install (recommended):**
Copy `frontend-system-design/` into `.claude/skills/` at your project root.

**Global install:**
Copy `frontend-system-design/` into `~/.claude/skills/` in your user home directory.

```text
your-project/
  .claude/
    skills/
      frontend-system-design/
        SKILL.md
        references/
```
*(Note: Other Agent Skills-compatible tools may use different paths, such as `.agents/skills/`).*

### 2. Claude.ai Web Install

To use this skill inside the Claude.ai web interface:

1. Zip the `frontend-system-design/` folder so the zip file contains the skill folder as its root.
2. Upload the zip file in Claude.ai under **Customize → Skills**.

## Usage

Analyze only:

```text
/frontend-system-design analyze this codebase. Do not modify code.
```

Fix selected issues:

```text
/frontend-system-design fix P0 and P1 issues only. Keep changes small and validate after edits.
```

Validate:

```text
/frontend-system-design validate the recent frontend changes.
```

*(Note: If installed via the marketplace plugin, the namespace is `/principal-frontend-engineer:frontend-system-design` instead).*

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

The skill operates in three focused modes:

1. **Analyze**
   Read-only analysis. Produces the grounded priority report.
2. **Execute**
   Implements selected fixes safely. Preserves existing stack and patterns.
3. **Validate**
   Runs checks and verifies that changes did not break build, tests, or key flows.

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
  frontend-system-design/      <-- Open Skill Path (Primary)
    SKILL.md
    references/
  .claude-plugin/              <-- Marketplace Plugin Path
    marketplace.json
  plugins/
    principal-frontend-engineer/
      .claude-plugin/
        plugin.json
      skills/
        frontend-system-design/
      agents/
        frontend-auditor.md
        frontend-executor.md
        frontend-validator.md
  README.md
  LICENSE
  CHANGELOG.md
```

## Advanced: Claude Code Plugin Marketplace

If you prefer to install this globally via the Claude Code marketplace (which bundles the skill and its specialized execution agents into a single managed plugin), you can use these terminal commands:

```bash
claude plugin marketplace add Rakulck/Frontend-System-Design
claude plugin install principal-frontend-engineer@principal-frontend-engineer
```

Then inside Claude Code:

```text
/reload-plugins
```

### Local testing before publishing (Marketplace only)

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

## Development notes

This skill intentionally avoids sample private repo outputs in the MVP. Test it on real repositories locally, then improve the skill based on failure cases.

Best iteration loop:

```text
Run audit → inspect weak findings → improve SKILL.md/references/agents → run again on a fresh repo → repeat.
```
