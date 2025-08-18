# Refactor Playbook (Portable Across Tools)

**Objective:** Safely correct early design mistakes while preserving public contracts and keeping the environment portable across Lovable, Copilot, local dev, and CI.

**Inputs (authoritative):**
- `/docs/ARCHITECTURE.md` — current system boundaries, module map, ownership.
- `/docs/DECISIONS.md` — ADR log (why decisions were made).
- Lockfiles + runtime pins (`.devcontainer/`, `Dockerfile`, `package-lock.json`/`pnpm-lock.yaml`, `pyproject.toml`/`poetry.lock`, `.tool-versions`, `.nvmrc`).
- Test suite (golden/contract tests where applicable).

---

## 1) Forensics & Diagnosis
- Produce a quick **module dependency graph** for the touched area.
- Detect and mark risks:
  - **Anemic domain model**, **God objects**, **primitive obsession**, **temporal coupling**, **shared mutable state**, **hidden I/O & globals**, **leaky abstractions**, **mixed UI/domain/data**, **cyclic deps**.
- Identify **hotspots** (files with high churn + high complexity).
- List **external side-effects** (network, filesystem, DB, env vars).

**Output:**
- `REFactor-Notes.md` in the PR: graph (as text or mermaid), hotspots list, risk callouts.

---

## 2) Target Architecture & Cut Plan
- Re-state the relevant **bounded contexts** and desired module boundaries.
- Apply **ports & adapters** (dependency inversion):
  - Define **domain ports** in `src/domain/ports/` (or language equivalent).
  - Implement adapters in `src/infrastructure/adapters/`.
- **Isolate side-effects** to the outer layers. Domain stays pure.
- **Clarify state ownership** and **nullability contracts**.
- **Stabilize error model** (typed errors or discriminated unions).
- Define a **cut plan**:
  - Sequence of small PRs (≤ 400 lines diff ideally).
  - Compatibility notes (feature flags, toggles).

**Output:**
- ADR entry (see template below) if public interfaces change.
- Updated `/docs/ARCHITECTURE.md` diagram + text.

---

## 3) Implementation Rules
- Keep PRs **scope-limited**: one architectural concern at a time.
- Update/author **tests with each refactor**:
  - Contract tests for public APIs.
  - Snapshot tests for stable outputs.
  - Add regression tests when fixing bugs uncovered during refactor.
- Maintain **backwards compatibility** unless ADR explicitly approves a breaking change.
- Do **not** modify infra (Docker/CI/secrets) in the same PR as logic refactors unless required and documented.

---

## 4) Quality Gates (must pass)
- `make lint` (style/format)
- `make typecheck` (tsc/mypy/etc.)
- `make test` (unit/integration)
- PR **Review Checklist** (see `/prompts/20_review_checklist.md`)

---

## 5) Deliverables in Every Refactor PR
1. **Diff rationale** — what changed, why, alternative options considered.
2. **Risk assessment** — behavior/compat risks & mitigations.
3. **Tests** — list new/updated tests; include commands to run locally.
4. **Docs** — ARCHITECTURE & ADR updates if applicable.
5. **Follow-ups** — next cuts (bulleted, time-boxed).

---

## 6) Anti-Patterns (do not do)
- Broad, multi-concern PRs.
- Silent behavior changes.
- Introducing new global states or hidden I/O.
- Changing public interfaces without ADR & version notes.
- Mixing infra & domain refactors in one PR.

---

## 7) ADR (Decision Record) Template
Append to `/docs/DECISIONS.md`:
