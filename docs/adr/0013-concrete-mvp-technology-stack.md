# ADR-0013: Concrete MVP technology stack and technical boundaries

Status: Proposed | Date: 2026-10-06 | Design plan: DP-13

## Context

The first spec described interfaces but left tools, deployment and implementation boundaries unresolved. The user asked where the technical/stack design was. Python-first learning, local vector storage and replaceable generation/embedding models are confirmed constraints.

## Decision

Recommend Python 3.12, Streamlit UI, FastAPI/Uvicorn backend with Pydantic contracts, Qdrant in a localhost-bound container, SQLite through sqlite3 repositories, pdfplumber/pypdf extraction, custom structural chunking, Sentence Transformers embedding adapters, provider-specific generation adapters and pytest-based tests. Propose fake/Ollama/Anthropic generation adapters; actual real-model IDs and opt-in calls remain unset.

The [technical design](../technical-design.md) defines topology, source layout, routes, transactions, configuration and tests. API/domain services enforce identity/ownership; UI/provider/vector-library calls do not own business authorization.

## Rationale

Keeps product logic in Python, gives authorization a testable backend boundary, isolates local vector representations for experimentation and keeps exact account/support state separate from search. Direct interfaces make data flow teachable without mandatory agent orchestration.

## Alternatives considered

- Streamlit-only: fewer processes but closer coupling between UI reruns and business workflows.
- React/Next.js: stronger frontend control with an additional language/build ecosystem.
- Embedded Qdrant or Chroma: fewer infrastructure steps; different persistence/ownership tradeoffs.
- PostgreSQL/pgvector: can consolidate storage but adds a relational server and is not required by the current corpus.
- SQLAlchemy/Alembic: richer persistence/migrations with more dependencies; defer until justified.
- LangChain/LangGraph or a universal generation gateway: possible integration helpers but unnecessary for the initial fixed RAG sequence; model/backend contracts still need explicit tests.

## Consequences and limitations

Two Python web processes plus a vector container require local setup. sqlite3 repositories require disciplined transactions and schema migrations. Real embedding inference and provider switching are not yet benchmarked or compatibility-tested. Exact package/container locks are a scaffolding deliverable, not invented here. Proposed stack does not change the original access matrix or imply production authentication/readiness.

## Traceability and verification

- Specification: [MVP spec](../specs/insurance-rag-mvp.md)
- Technical plan: DP-13; realizes DP-02-DP-12.
- Requirements: FR-01, FR-03, FR-06, FR-08, FR-09, FR-11, FR-14, FR-15, FR-16.
- Planned tests: T-01, T-02, T-03, T-05, T-06, T-11, T-12, T-13, T-16, T-17, T-18, T-19, T-20, T-24, T-25, T-33, T-34, T-35, T-36, T-37, T-38, T-39, T-40, T-41, T-42, T-43.
- Implementation status: Not implemented; executable application tests not written or run.

## Evidence

Primary-source references and verification limits are listed in [technical design section 1](../technical-design.md#1-recommended-stack-and-alternatives). Current documentation establishes capabilities, not runtime compatibility on this machine.

## Change history

- 2026-10-06: Added a concrete proposed stack to fill the technical-design gap. No accepted user constraint is superseded.
