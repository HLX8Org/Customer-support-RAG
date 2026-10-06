# ADR-0002: Python-first local modular boundaries

Status: Accepted | Date: 2026-10-06 | Design plan: DP-02

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

The user chose Python-first learning and a locally hosted vector database while allowing replaceable model providers.

## Decision

Keep Python application logic, locally hosted vector storage, and independent embedding/generation boundaries. Keep interface and infrastructure choices configurable. UI framework and vector database product remain open.

## Rationale

Makes call/data flow teachable and prevents provider-specific behavior from spreading through business logic.

## Alternatives considered

A vendor-managed RAG platform reduces local setup but hides requested experimentation. A tightly coupled single script is quicker but makes changes and access invariants harder to isolate.

## Consequences and limitations

Adapters add a small amount of plumbing. Local operation is a prototype constraint, not a production deployment claim. No production authentication or service-level target is implied.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-11, FR-15
- Planned tests: T-24, T-25, T-41, T-42, T-43
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

Session requirements and the linked MVP specification; no external product capability is asserted by this decision.

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
