# Project Structure

Back to [README](../README.md) · See also [task-generation.md](task-generation.md) and [release-snapshot.md](release-snapshot.md)

## Repository map

```text
ClawForge/
├── docs/
├── examples/
├── openclaw_env/
│   ├── backend/
│   ├── core/
│   ├── data/
│   ├── evaluation/
│   ├── skills/
│   ├── tasks/
│   └── utils/
├── scripts/
├── tests/
├── pyproject.toml
└── README.md
```

## Where things live

- `examples/`: runnable entrypoints such as `train_and_eval.py`
- `openclaw_env/backend/`: backend implementations and execution routing
- `openclaw_env/core/`: environment and task abstractions
- `openclaw_env/data/`: checked-in tasks, split files, coverage reports, and benchmark release artifacts
- `openclaw_env/evaluation/`: checkers, metrics, and evaluator logic
- `openclaw_env/skills/`: app-family skills, adapters, and fallback policies
- `openclaw_env/tasks/`: task generators, registry, and generation options
- `scripts/`: generation and maintainer utilities
- `tests/`: generator, runtime, and CLI regression tests

## Development checks

Targeted checks:

```bash
pytest -q tests/test_train_and_eval_cli.py
pytest -q tests/test_hard_decision_workflow_generator.py
pytest -q tests/test_hard_split_and_configs.py tests/test_generation_options.py
```

Broader suite:

```bash
python -m pytest tests -v
```

## Safety summary

The environment applies two protection layers:

- an allowlist for strict simulated backends
- a blocked-pattern filter for dangerous shell actions

`real` and `hybrid` disable the allowlist for real `openclaw` execution, but blocked patterns remain in force.
