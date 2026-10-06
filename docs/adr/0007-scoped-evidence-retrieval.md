# ADR-0007: Policy-scoped evidence retrieval and expansion

Status: Proposed | Date: 2026-10-06 | Design plan: DP-07

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

Coverage questions require benefits, restrictions and account-specific scope; comparison questions require evidence for each permitted product.

## Decision

Filter to permitted policy/version before selecting evidence; expand parent and required condition links under the same authorization. Deduplicate citations and query compared products independently. Keep retrieval limits/configuration recorded.

## Rationale

Prevents cross-policy contamination and preserves evidence completeness for generation.

## Alternatives considered

Global semantic search may return a different product. Parent-only expansion misses distant conditions. Hybrid keyword/vector retrieval is a later benchmark candidate; it is not yet selected.

## Consequences and limitations

Incomplete linkage can still omit decisive conditions, so evaluation and uncertainty behavior are required. Similarity alone cannot establish coverage or answerability.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-10
- Planned tests: T-21, T-22, T-23
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

Session requirements and the linked MVP specification; no external product capability is asserted by this decision.

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
