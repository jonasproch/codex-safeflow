# AGENTS.md

Read the `.ai` memory folder at the start of every session before doing any work:

- `.ai/DECISION-LOG.md`: important decisions you think are worth remembering for the future
- `.ai/MINOR-ISSUES.md`: any minor issues the reviewer finds that are not fixed right away, but might want to be fixed in the future
- `.ai/MISTAKES.md`: any mistakes you think are worth remembering for the future, don't put every small thing here, just the important things that could save time in the future
- `.ai/TASKS.md`: before doing the work, plan and split the task into smaller subtasks (if it makes sense) here and go one by one when implementing them

Treat these files as mandatory context. Keep them concise and durable. Only the main agent writes `.ai/*`.

Read the root domain rule files before changing the corresponding layer:

- `frontend-rules.md`: required context for any work in `Mediclinic.DMS.Client/`.
- `backend-rules.md`: required context for any work in `Mediclinic.DMS.API/`, `Mediclinic.DMS.Database/`, `Mediclinic.DMS.Models/`, or `DB/`.

Use the `reviewer` subagent at the end of implementation work to critique the result before considering the task done.

Skip `reviewer` only for very small changes, such as a 1-2 file edit with only a few changed lines and no meaningful behavioral risk.

## Project Overview

Describe this repository in 2-5 lines.

Example:
- This is a SaaS app with a React frontend and ASP.NET Core backend.
- The frontend lives in `apps/web/`.
- The API lives in `apps/api/`.
- Shared contracts live in `packages/contracts/`.

## Architecture Map

List the important areas of the codebase so agents do not need to guess.

- `apps/web/`: React frontend
- `apps/api/`: ASP.NET Core API
- `packages/contracts/`: shared DTOs and types
- `packages/ui/`: reusable UI components
- `infra/`: deployment and infrastructure config

If relevant, add boundary rules.

Example:
- Do not import API internals into the frontend.
- Shared contracts must stay backward compatible unless explicitly requested.
- Database schema changes must include migration files.

## Core Commands

List the commands agents should prefer for validation.

- Install: `pnpm install`
- Dev: `pnpm dev`
- Frontend tests: `pnpm test`
- Frontend typecheck: `pnpm typecheck`
- Lint: `pnpm lint`
- Backend tests: `dotnet test`
- Build: `pnpm build`

If there are project-specific commands, include them.

Example:
- Run only web tests: `pnpm --filter web test`
- Run API locally: `dotnet run --project apps/api`
- Apply migrations: `dotnet ef database update`

## Working Rules

Capture durable repo-specific expectations