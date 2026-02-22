# Skills

This folder serves as a reference for the Agent Skills ecosystem and a placeholder for portable skills that can be shared across agents.

## In This Repository

Currently, this folder contains documentation on:
- How to structure and manage skills.
- The difference between Workspace (Local) and Home (Global) scopes.
- Marketplaces for discovering pre-built skills.

You can add your own skills here by creating a sub-folder for each skill with a `SKILL.md` file inside.

---

Most modern CLI coding agents
 have adopted an open, portable "Agent Skill" format (originally popularized by Anthropic), meaning a skill written for one tool will often work seamlessly in another.

At their core, Agent Skills are just folders containing a SKILL.md file. This file uses YAML frontmatter for metadata (like the skill's name and a description that acts as the "trigger phrase") and Markdown for the actual instructions, rules, and examples.

Here is a breakdown of how to create and manage skills across Gemini, Codex, OpenClaw, Copilot, and OpenCode.

## Skills markets

| Marketplace | Skills Count | Key Categories | Monetization | Installation |
| :--- | :--- | :--- | :--- | :--- |
| **[SkillzWave](https://skillzwave.ai)** | 44,000+ | Dev, Legal, Finance | Creator pricing | CLI (`skilz`) |
| **[Skills Store](https://skills.sh)** | Thousands | All verified | Per-download | API |
| **[Smithery](https://smithery.ai)** | Thousands | Tools, Web, AI | Community | Protocol servers |
| **[Agent Skills Repo](https://github.com/anthropics/skills)** | 100K+ | Coding, Analytics | Free/share | Direct install |
| **[ClawMart / ClawHub](https://clawhub.com)** | Growing | Custom extensions | Usage pay | File-based |

## Skils scope

Understanding how AI CLI agents handle skill scopes and where to place those files is crucial for keeping your workflows organized. Almost all modern agents (like the ones we discussed) follow a standard hierarchy of Workspace (Local) Scope versus Home (Global) Scope.

Here is how the file placement and scoping rules generally work across most popular tools.

Understanding how AI CLI agents handle skill scopes and where to place those files is crucial for keeping your workflows organized. Almost all modern agents (like the ones we discussed) follow a standard hierarchy of **Workspace (Local) Scope** versus **Home (Global) Scope**.

Here is how the file placement and scoping rules generally work across these tools.

### 1. Workspace (Project) Scope

Workspace skills are tied to a specific project, repository, or directory. They are designed to hold the unique context, conventions, and operational scripts for that specific codebase.

* **Standard Placement:** In the root of your project directory.
* Tool-agnostic standard: `<workspace-root>/.agents/skills/<skill-name>/SKILL.md`
* Tool-specific standard (e.g., Copilot): `<workspace-root>/.github/skills/<skill-name>/SKILL.md`


* **When to use it:** * When you have specific PR formatting rules for a single repo.
* When the agent needs instructions on how to build, test, or deploy that specific project.
* When you are sharing skills with your team.


* **Version Control:** You **should** commit these folders to Git. Because they are plain text, they act as living documentation that travels with the repo, allowing any developer's AI agent to instantly understand the project's rules upon cloning.

### 2. Home (Global) Scope

Home skills belong to you as an individual user. They are available to your AI agent no matter what directory you are currently working in.

* **Standard Placement:** In your user's home directory.
* Tool-agnostic standard: `~/.agents/skills/<skill-name>/SKILL.md`
* Tool-specific standard (e.g., OpenCode): `~/.config/opencode/skills/<skill-name>/SKILL.md` or `~/.opencode/skills/...`


* **When to use it:**
* Personal productivity hacks and standardized git aliases.
* Universal code review checklists you apply to all your work.
* Terminal navigation or system administration tasks.


* **Version Control:** These are typically managed in your personal "dotfiles" repository rather than a specific project repo.

---

### Scope Resolution: The Override Rule

Because you can have skills in both places, AI agents use a strict resolution order, reading from the most specific context to the least specific:

1. **Workspace Scope (`./.agents`)** is checked first.
2. **Home Scope (`~/.agents`)** is checked second.

**Why this matters:** If you have a global skill named `git-commit` (located in `~/.agents/skills/git-commit/SKILL.md`) but you are working in a repository that has its own specific `git-commit` skill (`./.agents/skills/git-commit/SKILL.md`), **the workspace skill will silently override the global one.** The agent will only load the project-specific instructions, preventing your personal preferences from clashing with a team's established repo conventions.

### Summary of File Structure

Regardless of whether you are in your Home or Workspace directory, the internal folder structure for the skill itself remains identical:

```text
📁 .agents/                 (or .gemini/, .github/, etc.)
 └── 📁 skills/
      ├── 📁 react-tester/  (The folder name acts as the system ID)
      │    └── 📄 SKILL.md  (Contains YAML metadata and Markdown rules)
      │
      └── 📁 sql-debugger/
           ├── 📄 SKILL.md
           └── 📄 query.sh  (Optional: Helper scripts the SKILL.md can trigger)

```

Would you like me to write a quick bash script you can run to instantly scaffold this directory structure (including the `SKILL.md` template) in your current workspace?

## Structure

```markdown
---
name: pr-reviewer
description: Executes read-only SQL queries against the local database to debug states.
---
# Goal
[What the skill achieves]
# Instructions
[Step-by-step logic]
# Constraints
[Do NOT do X, Y, Z]
```
