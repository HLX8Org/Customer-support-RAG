# ADR-0010: Persistent asynchronous local support queue

Status: Proposed | Date: 2026-10-06 | Design plan: DP-10

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

The user accepted discussing a local queue but asked about MVP versus production escalation. Samsung public contact routes do not establish internal AI handoff technology.

## Decision

Offer an explicit customer-triggered support submission, persist one idempotent ticket with transcript/evidence references, expose a support-only review/reply screen and show customer-owned status. Keep submission behind a replaceable support interface.

## Rationale

Delivers a complete learning handoff without live staffing or external writes.

## Alternatives considered

Phone/email links alone do not preserve an in-app case. Real-time chat requires staffing and presence handling. An external ticket service introduces credentials and workflow commitments before the local flow is proven.

## Consequences and limitations

This is our proposed workflow, not Samsung claim submission. Tickets need restart durability, owned access and transition rules. A real integration requires authorization, delivery retries and duplicate prevention.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-14
- Planned tests: T-33, T-34, T-35, T-36, T-37
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

- https://uk.careplus.co/
- https://www.samsung.com/uk/support/repair/

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
