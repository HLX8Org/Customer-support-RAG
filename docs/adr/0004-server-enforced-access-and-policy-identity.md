# ADR-0004: Server-enforced access and exact policy identity

Status: Accepted | Date: 2026-10-06 | Design plan: DP-04

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

Prospects, customers and support have different entitlements. The user permits all-customer support access initially and plans assigned-session scope later.

## Decision

Resolve synthetic identities and entitlements server-side. Customers access only owned private records; support accesses all synthetic customers initially; other employees have no support/private access. Resolve exact policy/version through account records and enforce permission checks on every data path.

## Rationale

A vector similarity match or request-supplied ID cannot establish identity, ownership or authority.

## Alternatives considered

UI-only restrictions are bypassable. Filtering only the initial vector results misses parent expansion, caches, citations and tickets. Case-assigned-only support is a later feature requested by the user.

## Consequences and limitations

Negative tests span search, lookup, history, evidence expansion and support. Synthetic fixture authentication is labelled as simulation and cannot be presented as production security.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-06, FR-07
- Planned tests: T-11, T-12, T-13, T-14, T-15
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

Session requirements and the linked MVP specification; no external product capability is asserted by this decision.

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
