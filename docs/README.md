# Insurance RAG design documents

Start with the [MVP specification](specs/insurance-rag-mvp.md). It captures confirmed requirements, proposed defaults, access rules, contracts, acceptance gates and incremental delivery.

- [Technical architecture and technology stack](technical-design.md): concrete tool recommendations, local deployment topology, module layout, API contracts, storage/transaction boundaries and provider configuration.

- [Architecture decision log](adr/README.md): 13 decisions with context, rationale, alternatives, consequences and status.
- [Acceptance and TDD plan](testing/mvp-test-plan.md): 43 planned behavior checks, fixtures and test-first workflow.
- [Traceability manifest](specs/traceability.json): requirement -> design plan -> ADR -> planned test mappings, plus implementation increments.
- [Candidate source corpus](../data/reference/mobile_protection_uk/README.md): original public PDFs and provenance.

All software behavior is specified, not implemented. Accepted ADRs capture explicit user requirements; Proposed ADRs remain recommendations. Application tests and model evaluations have not been run. Update specification and traceability before adding features; keep superseded decision history.
