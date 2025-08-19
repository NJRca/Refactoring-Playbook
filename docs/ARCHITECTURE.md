# Architecture (Starter)

## Modules
- Domain: src/domain/*
- Application: src/app/*
- Infrastructure: src/infrastructure/*
- Interface: src/interface/*

## Invariants
- Domain imports no infrastructure/interface.
- Side-effects isolated in adapters and injected via ports.
