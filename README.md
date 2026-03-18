# Codex SafeFlow

A minimal setup for running Codex with a safer, more structured workflow.

Instead of relying on one-off prompts, this repo gives Codex a small operating system:

- an `AGENTS.md` contract for how the agent should work
- a persistent `.ai/` memory folder for decisions, tasks, and mistakes
- a lightweight `.codex/config.toml` for agent limits

The result is simple: better continuity, cleaner task execution, and fewer repeated mistakes across sessions.

## Why This Exists

When coding agents work without guardrails, they tend to:

- lose context between sessions
- repeat the same mistakes
- make changes without leaving durable reasoning behind
- drift away from the actual project structure

Codex SafeFlow fixes that with a very small set of conventions.

## What’s Included

```text
.
├── .ai/
│   ├── DECISION-LOG.md
│   ├── MINOR-ISSUES.md
│   ├── MISTAKES.md
│   └── TASKS.md
├── .codex/
│   └── config.toml
└── AGENTS.example.md
```

### `AGENTS.example.md`

The base instruction file for your repo.

It tells Codex to:

- read the `.ai/` memory files at the start of each session
- plan work in `TASKS.md`
- keep durable lessons in the memory files
- respect project structure and validation commands
- use a reviewer pass for non-trivial changes

You should copy this to `AGENTS.md` and then tailor it to your codebase.

### `.ai/`

This is the persistent memory layer:

- `DECISION-LOG.md` tracks important decisions worth remembering
- `MINOR-ISSUES.md` stores known small issues that are not fixed yet
- `MISTAKES.md` captures lessons that should prevent repeated errors
- `TASKS.md` is the working scratchpad for breaking work into steps

These files are intentionally simple. They work well because they are easy to maintain.

### `.codex/config.toml`

Small Codex configuration for agent behavior.

Current defaults:

- max threads: `2`
- max depth: `1`

That keeps this setup controlled and lightweight.

## Quick Start

1. Copy `AGENTS.example.md` to `AGENTS.md`.
2. Open `AGENTS.md` and replace the placeholder project sections with your real repo details.
3. Keep the `.ai/` folder in the root of your project.
4. Start using Codex normally.
5. Let the agent update `.ai/` as work progresses.

Example:

```bash
cp AGENTS.example.md AGENTS.md
```

## Recommended Workflow

For each session, Codex should:

1. Read `AGENTS.md`.
2. Load the `.ai/` memory files.
3. Write or refine the current plan in `TASKS.md`.
4. Implement the requested change.
5. Record durable decisions, issues, or mistakes back into `.ai/`.

This keeps sessions consistent without adding much process overhead.

## Best Use Cases

This setup is a good fit for:

- solo development with Codex
- small teams using shared agent conventions
- repos where continuity between sessions matters
- projects where you want agent output to stay structured and reviewable

## Customizing It

You can extend the template by adding:

- project architecture notes
- validation commands
- folder-specific rules
- reviewer requirements
- deployment or migration constraints

The important part is to keep the rules durable. If something will matter in future sessions, it belongs in `AGENTS.md`.