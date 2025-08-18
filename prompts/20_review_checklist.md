# PR Review Checklist

- Scope: one architectural concern; no infra mixing unless justified.
- Contracts: public interfaces unchanged or ADR updated.
- Side-effects: isolated; domain remains pure.
- Types & errors: explicit, consistent, documented.
- Tests: added/updated; failure cases covered; contracts stable.
- Docs: ARCHITECTURE diagram/text updated if boundaries moved.
- Performance: no N+1s or obvious regressions; basic perf budget respected.
- Security: secrets untouched; no new data exfil paths; input validation remains intact.
