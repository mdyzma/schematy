## What This Folder Is

This folder contains *agent role cards*: small, standalone instruction files you can feed to an AI assistant to define:
- who it is (role)
- what it should do (responsibilities)
- what it must not do (constraints / forbidden actions)
- how it should work (workflow / style)

Files are named `*_AGENTS.md` so they are easy to discover and select.

## How To Use

1. Pick the agent file that matches the task.
2. Provide its contents to your AI tool as high-priority instructions (system/project prompt, or the tool’s “agent”/“profile” feature).
3. If the task changes, switch to a different agent file rather than editing the instructions inline.

## Agents Included

- `minimal_AGENTS.md`: “Repo Assistant” baseline for general codebase questions and small changes.
- `data_engineer_AGENTS.md`: “Data Platform Engineer” for analytics/schema work (dbt/Flyway/Redshift style workflows).

## Conventions For New Agents

When adding a new `*_AGENTS.md`:
- Keep it short and operational (what to do, what not to do).
- Prefer explicit allow/deny lists (paths, commands, environments).
- Include an approval checkpoint for any risky action (deploys, migrations, destructive commands).
- Avoid assuming repo contents that don’t exist; keep “Context” accurate.
- If you need multiple variants (e.g., “safe read-only” vs “write”), create separate agent files.

Suggested sections (optional, but consistent with the existing agents):
- `## Role`
- `## Context`
- `## Responsibilities`
- `## Allowed Actions`
- `## Forbidden Actions`
- `## Workflow`
- `## Style`

## Note On `agents/` vs `AGENTS/`

This repository currently has two directories with duplicate agent files: `AGENTS/` and `agents/`.
Pick one as the canonical source of truth and keep the other in sync (or remove it) to avoid drift.
