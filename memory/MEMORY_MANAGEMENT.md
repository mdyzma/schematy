# Memory Management: Unified Cross-Platform Guide

This document defines a precise, cross-platform architecture for AI agent memory. By centralizing context and instructions, you ensure a consistent "mental model" for your agents across **Gemini CLI**, **OpenCode**, **OpenAI Codex**, and **Claude Code**.

---

## 1. Context Tiers: Precision Definitions

### Tier 1: Static Persona & Global Rules
*   **Storage**: `~/.config/ai/AGENTS.md`
*   **Purpose**: Immutable principles. Defines *who* the agent is and *how* it should talk.
*   **Key Sections**: 
    - `# Role`: (e.g., Senior Full-Stack Engineer)
    - `# Tone`: (e.g., Direct, technical, no preamble)
    - `# Prohibitions`: (e.g., NEVER use Tailwind, NEVER print secrets)

### Tier 2: Project-Specific Context
*   **Storage**: `./PROJECT_CONTEXT.md` (Symlinked to `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`)
*   **Purpose**: Domain knowledge. Defines *what* the project is.
*   **Key Sections**:
    - `# Architecture`: Overview of folders and services.
    - `# Stack`: Libraries, database versions, API specs.
    - `# Conventions`: File naming, testing patterns, error handling logic.

### Tier 3: Dynamic Session Memory
*   **Storage**: Tool-specific (e.g., `~/.gemini/memory.json` or Claude's Auto Memory).
*   **Purpose**: Learned facts. Remembers *what* happened in recent conversations.
*   **Usage**: Saved via tools like `save_memory` or learned automatically.

---

## 2. Implementation: The Unified Symlink Strategy

Run these once to set up your central hub:

```bash
mkdir -p ~/.config/ai/skills ~/.config/ai/agents
# Set Gemini global context override
export GEMINI_SYSTEM_MD="~/.config/ai/AGENTS.md"
```

In every new project root, run this "Unified Init" command:

```bash
touch PROJECT_CONTEXT.md
ln -s PROJECT_CONTEXT.md AGENTS.md
ln -s PROJECT_CONTEXT.md CLAUDE.md
ln -s PROJECT_CONTEXT.md GEMINI.md
```

---

## 3. Exemplary Use Case: "The Microservice Migration"

### Scenario
You are migrating a Python microservice from Flask to FastAPI. You want your agents to know the migration plan, follow specific Pydantic patterns, and remember your preferred Git flow.

### Step 1: Set Global Persona
In `~/.config/ai/AGENTS.md`:
```markdown
# Role: Python Expert
- Prefer FastAPI over Flask.
- Use Pydantic v2 for all schemas.
- Use Conventional Commits for all Git operations.
```

### Step 2: Define Project Context
In `./PROJECT_CONTEXT.md`:
```markdown
# Project: Order Service
## Architecture:
- `src/app/`: FastAPI endpoints.
- `src/models/`: Database schemas.
## Migration Status:
- Phase 1 (Endpoints) complete.
- Phase 2 (Validation) in progress.
```

### Step 3: Action & Persistence
1.  **Start with Gemini CLI**:
    - *User*: "Refactor the validation in `models/orders.py`."
    - *Gemini*: Reads `PROJECT_CONTEXT.md` (via `GEMINI.md` link), sees Phase 2 status, and applies Pydantic v2 patterns from your global rules.
    - *Gemini*: Uses `save_memory("Used OrderCreate schema for validation")`.

2.  **Switch to OpenCode**:
    - *User*: "Commit the changes."
    - *OpenCode*: Reads `PROJECT_CONTEXT.md` (via `AGENTS.md` link), sees the same project status.
    - *OpenCode*: Applies "Conventional Commits" rule from your global persona.
    - *Outcome*: Commits as `feat(orders): update schema to pydantic v2`.

3.  **Cross-Tool Result**: 
    Both tools acted as the same "Python Expert" persona, understood the specific "Order Service" architecture, and correctly identified the project's current phase without you repeating instructions.

---

## 4. Context Maintenance

| Action | Command / Method |
| :--- | :--- |
| **Refresh Memory** | `/memory refresh` (Gemini) or restart session (OpenCode/Claude). |
| **Summarize History** | `/compact` (Claude) or automatic via `Compaction` agents. |
| **Force Global Context** | Update `GEMINI_SYSTEM_MD` or the linked `AGENTS.md`. |

By following this unified approach, you transform multiple independent LLM tools into a single, synchronized AI workforce.
