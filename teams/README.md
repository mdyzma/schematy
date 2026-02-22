# Teams

Part of the **Schema Library**, this folder is for *agent teams*: small bundles of agent role cards that are meant to be used together for a workflow (for example: planner + implementer + reviewer), or for a domain (for example: data platform team).

## Intent

A team document should answer:
- which agents belong to the team (by referencing files in `agents/`)
- when to use the team (scope)
- the handoff sequence between agents (order of operations)
- any shared constraints (safety rails that apply across all agents)

## Suggested Structure

Create one file per team, for example `data_platform_TEAM.md`:
- `## Purpose`
- `## Agents`
- `## Workflow`
- `## Shared Constraints`

## Status

No team definitions are committed yet; this README defines the convention.
