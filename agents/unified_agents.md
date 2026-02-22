# Unified Agent Configuration Guide

This guide describes how to set up a unified configuration for AI agents (OpenCode, Gemini CLI, Codex, and Claude Code) using an XDG-compliant structure.

## Directory Structure

We recommend using `~/.config/ai` as the central repository for your agent configurations. This allows you to maintain a single source of truth for skills and rules.

```bash
mkdir -p ~/.config/ai/skills
mkdir -p ~/.config/ai/agents
```

## 1. Unified Rules (`AGENTS.md`)

The `AGENTS.md` file acts as the central instruction set for your agents. It defines the persona, behavioral rules, and project-specific guidelines.

### Creation
Create your global rules file:

```bash
touch ~/.config/ai/AGENTS.md
```

Add your core instructions to this file. For example:

```markdown
# Global Agent Rules

- **Role**: Senior Software Engineer.
- **Tone**: Professional, concise, and direct.
- **Privacy**: Never output secrets or API keys.
- **Testing**: Always run tests before submitting changes.
```

### Compatibility Setup
Link the tool-specific configuration files to your unified `AGENTS.md` to ensure all agents share the same instructions.

```bash
# OpenCode (Native support for ~/.config/opencode/AGENTS.md)
mkdir -p ~/.config/opencode
ln -s ~/.config/ai/AGENTS.md ~/.config/opencode/AGENTS.md

# OpenAI Codex
mkdir -p ~/.codex
ln -s ~/.config/ai/AGENTS.md ~/.codex/AGENTS.md

# Claude Code (Uses CLAUDE.md)
mkdir -p ~/.claude
ln -s ~/.config/ai/AGENTS.md ~/.claude/CLAUDE.md

# Gemini CLI
# Gemini uses system defaults or project-specific context. 
# You can enforce this globally by setting the GEMINI_SYSTEM_MD environment variable.
# Add this to your shell profile (.bashrc/.zshrc):
export GEMINI_SYSTEM_MD="~/.config/ai/AGENTS.md"
```

## 2. Unified Skills (`skills/`)

Skills are reusable capabilities (like "git-release" or "security-audit") stored in standardized directories. Most tools adhere to the "Agent Skills" open standard.

### Creation
Store all your custom skills in `~/.config/ai/skills`.

```bash
# Example: Create a 'hello-world' skill
mkdir -p ~/.config/ai/skills/hello-world
echo '---
name: hello-world
description: A simple greeting skill
---
Say hello to the user!' > ~/.config/ai/skills/hello-world/SKILL.md
```

### Compatibility Setup
Link the tool-specific skill directories to your unified skills folder.

```bash
# OpenCode & Gemini CLI & OpenAI Codex
# These tools natively support the ~/.agents/skills standard alias.
mkdir -p ~/.agents
ln -s ~/.config/ai/skills ~/.agents/skills

# Claude Code
# Claude primarily checks ~/.claude/skills.
mkdir -p ~/.claude
ln -s ~/.config/ai/skills ~/.claude/skills

# Gemini CLI (Specific Override)
# While Gemini reads ~/.agents/skills, you can also link its specific directory for safety.
mkdir -p ~/.gemini
ln -s ~/.config/ai/skills ~/.gemini/skills
```

## 3. Project-Specific Setup

For individual projects, you can maintain the same unified approach by placing an `AGENTS.md` file in the project root.

*   **OpenCode & Codex**: Will automatically detect `AGENTS.md`.
*   **Claude Code**: Will look for `CLAUDE.md`. You can symlink `AGENTS.md` to `CLAUDE.md` in the project root if needed, or rely on OpenCode's compatibility layer if using OpenCode as your driver.
*   **Gemini CLI**: Can be configured to look for `AGENTS.md` by adding it to the `context.fileName` setting in your project's `.gemini/settings.json` (or global settings).

```json
// .gemini/settings.json
{
  "context": {
    "fileName": ["AGENTS.md", "GEMINI.md", "CLAUDE.md"]
  }
}
```

## 4. Specialized Unified Roles

To extend your system, define specialized roles as sub-agents in `~/.config/ai/agents/`. These can be symlinked to tool-specific agent directories (e.g., `~/.config/opencode/agents/` or `~/.gemini/agents/`).

### Git/GitHub Specialist
**File**: `~/.config/ai/agents/git-expert.md`

```markdown
---
name: git-expert
description: Expert in Git and GitHub operations. Use for pulls, commits, pushes, and PR management.
tools:
  - bash
  - skill
---
# Git/GitHub Specialist Persona

You are an expert in source control. Your goal is to maintain repository integrity and follow best practices.

## Guidelines:
- **Clean Commits**: Ensure commit messages follow the Conventional Commits standard (e.g., `feat:`, `fix:`, `chore:`).
- **Safety First**: Always verify the current branch and status before performing destructive operations or pushes.
- **Pull/Sync**: Always pull with rebase when appropriate to keep history clean.
- **GitHub Interaction**: Use `gh` CLI for interacting with issues, PRs, and repository metadata.
```

### Generalized Architect
**File**: `~/.config/ai/agents/architect.md`

```markdown
---
name: architect
description: High-level architect for requirement analysis and task planning. Use to break down complex tasks.
tools:
  - read_file
  - glob
  - grep_search
---
# Generalized Architect Persona

You are a Senior Software Architect. Your task is to bridge the gap between requirements and implementation.

## Guidelines:
- **Requirement Analysis**: Deeply analyze task descriptions to identify edge cases, dependencies, and potential technical debt.
- **Modular Planning**: Break down complex requests into small, actionable, and testable sub-tasks for a developer.
- **Technology Alignment**: Ensure proposed solutions align with the project's existing architecture and conventions.
- **Outcome**: Your final output should be a structured "Implementation Plan" (e.g., a TODO list or a technical design spec).
```

## Summary of Paths

| Tool | Global Rules Path | Global Skills Path | Action |
| :--- | :--- | :--- | :--- |
| **OpenCode** | `~/.config/opencode/AGENTS.md` | `~/.agents/skills` | Symlink Rules & Skills |
| **Codex** | `~/.codex/AGENTS.md` | `~/.agents/skills` | Symlink Rules & Skills |
| **Claude** | `~/.claude/CLAUDE.md` | `~/.claude/skills` | Symlink Rules & Skills |
| **Gemini** | `GEMINI_SYSTEM_MD` (Env Var) | `~/.gemini/skills` | Set Env Var & Symlink Skills |

By following this setup, any skill you add to `~/.config/ai/skills` or any rule you add to `~/.config/ai/AGENTS.md` will be instantly available to all your AI agents.
