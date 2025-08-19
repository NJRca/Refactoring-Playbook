# Contributing

## Refactor Protocol
- Read `/prompts/10_refactor_playbook.md` before any refactor.
- Single-concern PRs; no infra+logic mixing unless justified.
- Public interface changes REQUIRE an ADR appended to `/docs/DECISIONS.md`.

## Quality Gates
- Run locally before pushing:

make lint
make typecheck
make test

- PR body must include: Diff rationale, Risk assessment, Tests added/updated, Docs updated, Follow-up cuts.

## Commits & PR Titles
- Use Conventional Commits: feat|fix|chore|refactor|docs|test(scope): message
- Example: `feat(api): add GET /widgets/{id}`
