# Codex SafeFlow

Minimal Codex setup for a safer, more consistent workflow.

It gives Codex three things:

- `AGENTS.md` for durable repo instructions
- `.ai/` for lightweight memory between sessions
- `.codex/` for small agent configuration

The default shape is intentionally simple: one main agent, one reviewer, and only occasional helper subagents when parallel work is actually worth the extra tokens.

## Files

```text
.
├── .ai/
│   ├── DECISION-LOG.md
│   ├── MINOR-ISSUES.md
│   ├── MISTAKES.md
│   └── TASKS.md
├── .codex/
│   ├── agents/
│   │   └── reviewer.toml
│   └── config.toml
└── AGENTS.example.md
```

- `AGENTS.example.md`: base instruction template for your repo
- `.ai/`: decision log, mistakes, minor issues, and working task plan
- `.codex/config.toml`: lightweight limits for subagents
- `.codex/agents/reviewer.toml`: read-only reviewer agent for non-trivial work

## Quick Start

1. Copy `AGENTS.example.md` to `AGENTS.md`.
2. Tailor `AGENTS.md` to your repo.
3. Keep `.ai/` in the project root.
4. Use Codex normally and let it maintain the memory files as needed.

```bash
cp AGENTS.example.md AGENTS.md
```

You can also ask Codex to create `AGENTS.md` from the template by scanning your repository and filling in the project-specific sections for you.

Example prompt:

```text
Read `AGENTS.example.md` and create `AGENTS.md` for this repository.
Scan the repo and replace the placeholder sections with repo-specific content.
Document the real architecture, important directories, boundary rules, and validation commands.
Keep the structure and intent of the template, but make the instructions concrete and concise for this codebase.
Do not invent details that are not supported by the repository.
```

## Notes

- Keep instructions concise and durable.
- Use the reviewer for non-trivial changes.
- Stay single-agent by default; only spawn helpers for clearly parallel, bounded work.
