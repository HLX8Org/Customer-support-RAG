# ADR-0008: Replaceable generation-provider adapters

Status: Accepted | Date: 2026-10-06 | Design plan: DP-08

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

The user wants the generation vendor and model type to be easily replaceable.

## Decision

Define a common generation request/response interface and explicit capability declarations. Keep provider prompts, limits and error translation in adapters. Business authorization and ticket submission remain outside the model.

## Rationale

Enables provider comparisons without changing customer access or evidence-selection behavior.

## Alternatives considered

Direct provider calls throughout the application couple product logic to one vendor. A framework-only interface still requires checking provider capabilities and error semantics.

## Consequences and limitations

Adapters cannot make every model equivalent. Unsupported context or output capabilities must fail clearly or use an explicitly tested fallback. No provider or SDK is selected yet.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-11
- Planned tests: T-24, T-25
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

Session requirements and the linked MVP specification; no external product capability is asserted by this decision.

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
