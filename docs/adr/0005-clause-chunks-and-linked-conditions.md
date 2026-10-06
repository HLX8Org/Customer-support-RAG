# ADR-0005: Clause chunks, parent context and linked conditions

Status: Proposed | Date: 2026-10-06 | Design plan: DP-05

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

The PDFs are structured policy wording and two-column summaries. Care+ battery benefit and warranty timing occur on different pages.

## Decision

Use reviewed structural extraction and clause/table-row child chunks, complete subsection parents and explicit related-condition/exclusion links. Begin around 250-450 tokens, split oversized clauses around 600 tokens, and use overlap only within split clauses. Adapt limits to the active tokenizer.

## Rationale

Retains contractual units and makes distant qualification retrieval explicit rather than hoping overlap supplies it.

## Alternatives considered

Fixed windows are a useful baseline but can cut clauses. Whole-page chunks mix topics. Embedding-based semantic splitting and LLM-written summaries add unneeded MVP complexity.

## Consequences and limitations

Manual boundary/link review is feasible for four PDFs but needs later automation. Links require provenance and product/version checks. Suggested sizes remain unmeasured defaults.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-03, FR-04, FR-05
- Planned tests: T-05, T-06, T-07, T-08, T-09, T-10
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

- https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/rag/rag-chunking-phase
- ../../data/reference/mobile_protection_uk/SCPlus_Terms_Conditions_UK_1.pdf

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
