# ADR-0011: Controlled retrieval and answer evaluation

Status: Proposed | Date: 2026-10-06 | Design plan: DP-11

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

Model and chunking comparisons need reproducible evidence; current recommendations have not been benchmarked on the corpus.

## Decision

Keep source snapshots and gold labels versioned. Vary embeddings with identical fitting chunks; vary chunking separately with a fixed embedding model. Hold generation/prompt fixed for answer comparisons. Record retrieval completeness, citations, false coverage assertions, latency, memory and failures; reserve held-out questions.

## Rationale

Separates retrieval and generation failures and avoids changing multiple variables while attributing gains to one model.

## Alternatives considered

Leaderboards are useful screening evidence but not corpus validation. Exact-string answer checks penalize valid paraphrases. LLM-only judges can inherit errors and should not be the sole gold authority.

## Consequences and limitations

Manual evidence labels cost effort. Approximately 40 questions are a seed, not statistical proof. No numerical quality gate is approved until measurements inform it. Live/provider checks remain explicitly labelled.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-16
- Planned tests: T-38, T-39, T-40
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

Session requirements and the linked MVP specification; no external product capability is asserted by this decision.

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
