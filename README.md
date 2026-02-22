# Schema Library

AI directives, role cards, and cross-platform configurations.

## Layout

```bash
.
├── agents/               # Agent role cards and unified config guides
│   ├── README.md
│   ├── data_engineer_AGENTS.md
│   ├── minimal_AGENTS.md
│   └── unified_agents.md
├── memory/               # Memory management strategies and guides
│   ├── README.md
│   └── MEMORY_MANAGEMENT.md
├── skills/               # Reusable agent skills and market info
│   └── README.md
├── teams/                # Collections/groups of agents
│   └── README.md
├── LICENSE
└── README.md
```

## Core Components

- **Agents**: Standalone role cards (`*_AGENTS.md`) and guides for unified cross-tool configuration.
- **Memory**: Strategies for maintaining context across different AI platforms (Gemini, Claude, OpenCode).
- **Skills**: Documentation and templates for extending agent capabilities using the Agent Skills standard.
- **Teams**: Orchestration patterns for multi-agent workflows.

## Notes

- On case-insensitive filesystems (common on macOS), `agents/` and `AGENTS/` refer to the same directory. This repository uses lowercase `agents/` as the canonical name.
