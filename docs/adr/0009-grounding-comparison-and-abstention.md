# ADR-0009: Grounded answers, comparisons and explicit uncertainty

Status: Proposed | Date: 2026-10-06 | Design plan: DP-09

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

The user requires unknown answers when retrieval lacks evidence and escalation for uncertainty. Product comparisons do not establish upgrade eligibility.

## Decision

Use explicit answer states with validated source references. Ask for missing facts, abstain on insufficient evidence, flag conflicts for review and do not obey instructions embedded in documents. Compare cited product attributes; avoid invented prices, eligibility and claim approval.

## Rationale

Makes incomplete evidence visible instead of converting a search failure into a denial or unsupported assurance.

## Alternatives considered

A single similarity cutoff is not calibrated coverage confidence. Mandatory yes/no answers hide uncertainty. Unconstrained general model knowledge cannot substantiate company-specific policy facts.

## Consequences and limitations

Mechanical citation validation only establishes reference validity, not full claim support. Human-labelled evaluation and adversarial fixtures remain necessary. False coverage statements need separate reporting.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-12, FR-13
- Planned tests: T-26, T-27, T-28, T-29, T-30, T-31, T-32
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

Session requirements and the linked MVP specification; no external product capability is asserted by this decision.

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
