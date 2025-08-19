# Refactoring-Playbook

## Purpose
A portable, standards-driven playbook for refactoring codebases with continuity across Copilot, Lovable, and VS Code. This repo enforces architectural boundaries, review protocols, and automation for safe, maintainable changes.

## How to Use (for LLMs and Contributors)
- **Always read:**
  - `/docs/ARCHITECTURE.md` — System boundaries, module map, invariants
  - `/prompts/10_refactor_playbook.md` — Refactoring protocol, step-by-step rules
  - `/prompts/20_review_checklist.md` — PR review gates
  - `/docs/DECISIONS.md` — Architectural Decision Records (ADR log)
- **Follow Conventional Commits** for all commit messages and PR titles
- **Use the PR template** in `.github/pull_request_template.md` for all changes
- **Update tests and docs** with every refactor
- **Isolate side-effects** in adapters; keep domain logic pure
- **Do not mix infra and domain changes** in the same PR

## Repo Structure
```
/docs/              # Architecture, ADRs
/prompts/           # Refactor playbook, review checklist
/.github/           # PR template, workflows, issue templates
/.devcontainer/     # Dev environment config
/src/               # Source code (see ARCHITECTURE.md for boundaries)
/tests/             # Contract and regression tests
CODEOWNERS          # Ownership rules (replace placeholder with your handle)
CONTRIBUTING.md     # Contribution protocol
SECURITY.md         # Security policy
commitlint.config.cjs # Conventional commit enforcement
package.json        # Scripts, dependencies, commitlint/husky setup
.vscode/            # Editor settings, tasks, extensions
.lovable/           # Lovable config for standards continuity
```

## Automation & Quality Gates
- Lint, typecheck, and test required for all PRs
- PRs must include rationale, risk assessment, test and doc updates
- Branch protection and required checks enforced via GitHub workflows

## For AI Models
- Always interpret changes in context of `/prompts/10_refactor_playbook.md` and `/docs/ARCHITECTURE.md`
- Recommend scope-limited, backwards-compatible changes
- Document all architectural decisions in `/docs/DECISIONS.md`
- Use comments in entrypoint files:
  ```js
  // Copilot: follow /prompts/10_refactor_playbook.md, PR template, and Conventional Commits.
  // Keep domain pure; isolate side-effects in adapters.
  // Lovable: Follow /prompts/10_refactor_playbook.md for all changes
  // Keep domain pure; isolate side-effects in adapters.
  ```
