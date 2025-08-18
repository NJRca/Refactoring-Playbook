# Architecture (Starter)

## Modules & Boundaries
- Domain: `src/domain/*` (pure; business rules; ports)
- Application: `src/app/*` (use-cases; orchestrations)
- Infrastructure: `src/infrastructure/*` (adapters: DB, HTTP, queues)
- Interface: `src/interface/*` (REST/GraphQL/UI handlers)

## Key Invariants
- Domain has no imports from infrastructure/interface.
- All side-effects live in adapters; injected via ports.

## Diagrams
<!-- Optionally use Mermaid -->
```mermaid
flowchart LR
UI[Interface] --> APP[Application]
APP --> DOM[Domain]
APP --> ADP[Infra Adapters]
ADP --> EXT[(DB/HTTP/FS)]

## 4) `/docs/DECISIONS.md`  *(empty log to start)*
```md
# Architectural Decision Records
<!-- Append ADRs using the template in /prompts/10_refactor_playbook.md -->
