# Contributing

ClawForge is a benchmark-first repository. Keep changes narrow, reproducible, and tied to real runtime behavior.

## Local setup

```bash
pip install -e .
pip install -e ".[dev]"
```

Optional Google-backed provider dependencies:

```bash
pip install -e ".[google]"
```

## Core commands

CLI help:

```bash
python examples/train_and_eval.py --help
python scripts/generate_tasks.py --help
```

Targeted regression checks:

```bash
pytest -q tests/test_train_and_eval_cli.py
pytest -q tests/test_hard_decision_workflow_generator.py
pytest -q tests/test_hard_split_and_configs.py tests/test_generation_options.py
```

Broader suite:

```bash
python -m pytest tests -v
```

## Development expectations

- Do not commit local secrets, OAuth tokens, or client-secret JSON files.
- Do not commit local trajectory dumps, temporary reports, or ad hoc benchmark outputs.
- Treat `openclaw_env/data/` as release content. If you regenerate tasks or datasets, describe exactly what changed and why.
- Keep public-facing docs aligned with the actual checked-in repo surface.
