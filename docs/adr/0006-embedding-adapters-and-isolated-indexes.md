# ADR-0006: Swappable embeddings and isolated index configurations

Status: Proposed | Date: 2026-10-06 | Design plan: DP-06

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

The user explicitly expanded the MVP to include swappable embeddings for testing. This accepted requirement needs a compatible-index design.

## Decision

Provide document/query embedding adapters and separate built indexes per complete corpus/chunk/embedding configuration. Verify manifest compatibility before search. Initially compare Qwen3-Embedding-0.6B and BGE-small-en-v1.5; candidate selection remains proposed.

## Rationale

Independent indexes simplify experiment isolation, rollback and incompatible vector dimensions/spaces.

## Alternatives considered

One shared unnamed vector field risks mixing representations. Named vectors can reduce duplicate payloads in supporting databases but add MVP coupling. A fixed embedding model would not satisfy the revised requirement.

## Consequences and limitations

More storage/build time, acceptable for the small corpus. Do not assume equal dimensions mean compatible spaces. Record prompts, revisions and normalization; selecting an unbuilt configuration requires a build.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-08, FR-09
- Planned tests: T-16, T-17, T-18, T-19, T-20
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

- https://qdrant.tech/documentation/tutorials-operations/embedding-model-migration/
- https://www.sbert.net/examples/sentence_transformer/applications/semantic-search/README.html
- https://huggingface.co/Qwen/Qwen3-Embedding-0.6B
- https://huggingface.co/BAAI/bge-small-en-v1.5

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
