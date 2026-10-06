# ADR-0001: Specification and test-first delivery

Status: Accepted | Date: 2026-10-06 | Design plan: DP-01

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

The user explicitly requested specification-driven and test-driven development with ADR mapping. Model-quality evaluation and software behavior verification require different evidence.

## Decision

Maintain stable requirement, design-plan and test IDs. Write acceptance examples and meaningful failing behavior tests before implementation. Record architectural choices and their status; do not claim model quality from mocked tests.

## Rationale

A traceable process supports incremental features and makes unimplemented behavior visible.

## Alternatives considered

Implementation-first followed by tests is simpler initially but does not satisfy the requested workflow. A large immutable specification slows discovery; keep a versioned living specification instead.

## Consequences and limitations

Adds documentation upkeep. TDD applies to deterministic behavior; labelled evaluations separately assess probabilistic outputs. Proposed ADRs require review and must not become Accepted automatically.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-01, FR-02, FR-03, FR-04, FR-05, FR-06, FR-07, FR-08, FR-09, FR-10, FR-11, FR-12, FR-13, FR-14, FR-15, FR-16
- Planned tests: T-01, T-02, T-03, T-04, T-05, T-06, T-07, T-08, T-09, T-10, T-11, T-12, T-13, T-14, T-15, T-16, T-17, T-18, T-19, T-20, T-21, T-22, T-23, T-24, T-25, T-26, T-27, T-28, T-29, T-30, T-31, T-32, T-33, T-34, T-35, T-36, T-37, T-38, T-39, T-40, T-41, T-42, T-43
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

- https://agilealliance.org/glossary/tdd/
- https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/introduction.html

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
