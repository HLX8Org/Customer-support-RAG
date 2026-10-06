# ADR-0003: Public source provenance and synthetic customer data

Status: Accepted | Date: 2026-10-06 | Design plan: DP-03

Accepted records capture explicit user constraints. Proposed records document recommendations that remain reviewable, not implementation approval or completed behavior.

## Context

The user accepted UK/English public mobile-protection PDFs and synthetic customers. Local PDFs and Google Drive are initial sources.

## Decision

Preserve original PDFs/checksums and explicit product/version provenance. Keep fictional customer/certificate values labelled and separate from insurer wording. Include Drive-origin ingestion in the MVP scope; manual export is the proposed first path and authenticated synchronization remains gated.

## Rationale

Separates authoritative public wording from fictional account examples and provides reproducible evaluation inputs.

## Alternatives considered

Entirely fictional product policies simplify licensing but lose authentic document structure. Real customer data is outside the learning scope. Live Drive sync first requires unresolved identity and sharing decisions.

## Consequences and limitations

Publicly downloadable does not mean openly licensed. Manual imports cannot establish current Drive ACLs or propagate revocations. Permission mapping must be explicit before private files are indexed.

## Traceability and verification

- Specification: [Insurance RAG MVP](../specs/insurance-rag-mvp.md)
- Requirements: FR-01, FR-02
- Planned tests: T-01, T-02, T-03, T-04
- Test definitions: [MVP test plan](../testing/mvp-test-plan.md)
- Implementation status: Not implemented; tests not written or run.

## Evidence

- ../../data/reference/mobile_protection_uk/source-manifest.json
- ../../data/reference/mobile_protection_uk/README.md

## Change history

- 2026-10-06: Initial record. No prior decision is superseded.
