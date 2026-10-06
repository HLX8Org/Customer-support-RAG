# Insurance RAG Prototype

A design-stage insurance retrieval-augmented generation project. Start with
[the documentation index](docs/README.md) and follow [Repository Guidelines](AGENTS.md).
Application code and acceptance tests have not been implemented.

## Local development environment

The development environment uses **Python 3.13.14**, recorded in `.python-version`.
Python 3.12 remains a proposed application baseline in the technical design;
application/model dependencies have not yet been checked on 3.13.

Run these **zsh/bash** commands from this directory. A local Python 3.13 installation
is required; installing development packages requires access to PyPI.

```sh
python3.13 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements-dev.txt
python -m pip check
python -m pytest --version
```

- `-m venv .venv` creates the project environment with isolated installed packages.
- `source` activates it in the current shell, so `python` uses `.venv`.
- `-m pip install -r` installs the pinned development packages from the file.
- `pip check` checks installed dependency compatibility; `pytest --version` checks the test runner.

Use `deactivate` to leave the environment. Activation does not persist across shells.
Alternatively, invoke `.venv/bin/python` explicitly to avoid relying on activation.

## Tests and Git

Once behavior tests are added, run `.venv/bin/python -m pytest tests/`.
There are currently no application tests: running pytest without tests returns exit code 5.
Environment smoke checks do not establish application correctness or model quality.

Git is initialized locally on `main`. `.gitignore` excludes `.venv`, credentials,
Python caches, and generated `var/` state. Keep original PDFs and provenance under
`data/reference/`; their redistribution license has not been verified.
