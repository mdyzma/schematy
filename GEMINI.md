# GEMINI Context: Schema Library

## Project Overview
This repository, `schematy`, serves as a centralized hub for AI agent configurations, role cards, and operational schemas. It is designed to provide a unified "mental model" for AI agents across different platforms, including **Gemini CLI**, **OpenCode**, **OpenAI Codex**, and **Claude Code**.

### Key Areas:
- **Agents**: Role-based instruction sets (role cards) that define persona and responsibilities.
- **Memory Management**: Strategies for maintaining consistent context and "long-term" memory across diverse tools.
- **Skills**: Portable capabilities based on the Agent Skills standard.
- **Teams**: Orchestration guidelines for multi-agent collaboration.

## Key Files & Directories
- **`agents/`**: Contains role cards (`*_AGENTS.md`) and the `unified_agents.md` guide for cross-platform setup.
- **`memory/MEMORY_MANAGEMENT.md`**: The master guide for cross-tool context synchronization and symlink strategies.
- **`skills/README.md`**: Overview of the Agent Skills ecosystem and directory structures.
- **`teams/README.md`**: Defines conventions for grouping agents into functional teams.

## Usage for Gemini CLI
This repository provides the blueprints for configuring Gemini CLI and other agents. Use the role cards in `agents/` to set up specific personas, and follow the guides in `memory/` and `agents/unified_agents.md` to establish a persistent, tool-agnostic development environment.

## Maintenance
- Ensure new agent files follow the `*_AGENTS.md` naming convention.
- Keep cross-platform compatibility in mind when updating memory or skill documentation.
- Update the root `README.md` layout section when new top-level directories or key files are added.
