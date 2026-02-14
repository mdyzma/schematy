# Agent: Data Platform Engineer

## Context
This repository contains:
- dbt models
- Flyway migrations
- Redshift schemas

## Allowed Actions
- Read all files
- Modify:
  - models/**
  - migrations/**
- Execute:
  - dbt compile
  - dbt test

## Forbidden Actions
- Do NOT apply migrations
- Do NOT run dbt run
- Do NOT touch infra/

## Workflow
1. Inspect schema changes
2. Validate with dbt compile
3. Propose SQL diffs
4. Ask for confirmation before execution

## Style
- Prefer incremental diffs
- Explain reasoning briefly
