# Architecture decision log

Date: 2026-10-06. Accepted means an explicit user constraint; Proposed means a reviewable implementation recommendation. Neither means implemented. Use Superseded when an accepted decision is replaced, link the replacement, and retain history.

Entry points: [MVP specification](../specs/insurance-rag-mvp.md), [test plan](../testing/mvp-test-plan.md), [machine-readable traceability](../specs/traceability.json).

Concrete implementation: [Technical architecture and technology stack](../technical-design.md), mapped through ADR-0013.

| ADR | Design plan | Status | Decision |
| --- | --- | --- | --- |
| [ADR-0001](0001-specification-and-test-first-delivery.md) | DP-01 | Accepted | Specification and test-first delivery |
| [ADR-0002](0002-python-local-modular-boundaries.md) | DP-02 | Accepted | Python-first local modular boundaries |
| [ADR-0003](0003-source-provenance-and-synthetic-data.md) | DP-03 | Accepted | Public source provenance and synthetic customer data |
| [ADR-0004](0004-server-enforced-access-and-policy-identity.md) | DP-04 | Accepted | Server-enforced access and exact policy identity |
| [ADR-0005](0005-clause-chunks-and-linked-conditions.md) | DP-05 | Proposed | Clause chunks, parent context and linked conditions |
| [ADR-0006](0006-embedding-adapters-and-isolated-indexes.md) | DP-06 | Proposed | Swappable embeddings and isolated index configurations |
| [ADR-0007](0007-scoped-evidence-retrieval.md) | DP-07 | Proposed | Policy-scoped evidence retrieval and expansion |
| [ADR-0008](0008-generation-provider-adapters.md) | DP-08 | Accepted | Replaceable generation-provider adapters |
| [ADR-0009](0009-grounding-comparison-and-abstention.md) | DP-09 | Proposed | Grounded answers, comparisons and explicit uncertainty |
| [ADR-0010](0010-local-support-queue.md) | DP-10 | Proposed | Persistent asynchronous local support queue |
| [ADR-0011](0011-controlled-retrieval-and-answer-evaluation.md) | DP-11 | Proposed | Controlled retrieval and answer evaluation |
| [ADR-0012](0012-local-record-storage-and-extension-path.md) | DP-12 | Proposed | Local structured records and production extension path |
| [ADR-0013](0013-concrete-mvp-technology-stack.md) | DP-13 | Proposed | Concrete technology stack and technical boundaries |

## Adding a feature or revising a decision

Record context, decision, alternatives, rationale, consequences, requirement/test IDs, status and evidence. Update the specification, mapping and acceptance examples before implementation. Do not automatically accept a proposed decision because a later developer uses it. Link superseded records and preserve the original rationale.
