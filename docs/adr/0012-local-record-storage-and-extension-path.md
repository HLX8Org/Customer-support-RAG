# ADR-0012: Local structured records and production extension path

Status: Proposed | Date: 2026-10-06 | Design plan: DP-12

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

Account ownership, sessions and support state need exact lookup and persistent updates independent of vector similarity.

## Decision

Propose SQLite for local structured account/session/ticket records, separate from the local vector index. Encapsulate persistence and support integrations behind interfaces. Bind services locally and make network-dependent checks opt-in.

## Rationale

An embedded transactional store supports a small local prototype while preserving a later migration path.

## Alternatives considered

JSON files are simple but complicate concurrent updates and deduplication. PostgreSQL is a possible production-oriented alternative but adds a server. Vector storage alone is not an account/transaction source of truth.

## Consequences and limitations

SQLite is not a production concurrency guarantee. Backups, migrations, transaction boundaries and authorization remain application concerns. Later deployments need measured capacity and operational requirements.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-06, FR-14, FR-15
- Planned tests: T-13, T-34, T-35, T-36, T-41, T-42, T-43
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

- https://www.sqlite.org/whentouse.html

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
