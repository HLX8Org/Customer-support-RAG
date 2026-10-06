# Repository Guidelines

## Project Structure & Module Organization

This design-stage insurance retrieval-augmented generation (RAG) prototype has no application code or tests. `requirements-dev.txt` pins development dependencies.

- `docs/specs/insurance-rag-mvp.md`: requirements and acceptance examples; start here.
- `docs/specs/traceability.json`: requirement, design, decision, and test mappings.
- `docs/technical-design.md`: proposed stack and module boundaries.
- `docs/adr/`: architecture decision records (ADRs); preserve their status and history.
- `docs/testing/mvp-test-plan.md`: 43 planned behavior checks.
- `data/reference/mobile_protection_uk/`: four original policy PDFs and their provenance manifest.

Planned `src/insurance_rag/` modules cover domain rules, contracts, services, interfaces, adapters, API, UI, and CLI. Tests belong under `tests/`; generated state under `var/`. These directories do not exist yet.

## Build, Test, and Development Commands

Run these shell commands from the repository root:

- `rg --files docs data`: inventory documentation and source assets; requires ripgrep.
- `shasum -a 256 data/reference/mobile_protection_uk/*.pdf`: calculate source checksums; compare with `source-manifest.json`.
- `source .venv/bin/activate`: activate the local Python 3.13.14 environment.
- `python -m pip install -r requirements-dev.txt`: install pinned development dependencies.
- `python -m pip check`: check installed dependency compatibility.
- `python -m pytest --version`: verify the installed test runner.

See `README.md` to recreate the environment. No build/start commands or application test suite exist yet.

## Coding Style & Naming Conventions

For new Python code, use four-space indentation, `snake_case` functions/modules, `PascalCase` classes, and typed public interfaces. No formatter or linter is configured. Keep provider libraries inside adapters and business rules independent of UI/storage frameworks. Use descriptive Markdown headings and numbered ADR filenames, such as `0013-concrete-mvp-technology-stack.md`.

## Testing Guidelines

Follow test-driven development: write a meaningful failing behavior test, implement, then refactor. pytest is installed; FastAPI TestClient and Streamlit AppTest remain proposed. Use `test_*.py` filenames and map tests to existing `T-xx` IDs. Run `.venv/bin/python -m pytest tests/` once tests exist. Use deterministic fakes and synthetic accounts by default. Keep real-model/network checks opt-in; report results and unrun checks separately. No coverage percentage is specified.

## Commit & Pull Request Guidelines

Git is initialized on `main`; no commit convention is established yet. Use concise imperative messages, optionally `docs:` or `feat:`. Pull requests should explain changes, link requirement/ADR/test IDs, and report validation; include screenshots for UI changes. Update specification and traceability before implementation. Do not automatically promote Proposed ADRs to Accepted.

## Security & Configuration

Preserve original PDFs and provenance. Use synthetic customer data; keep credentials and generated state outside commits. Enforce ownership and exact policy identity server-side. Vector similarity must never determine access rights.
