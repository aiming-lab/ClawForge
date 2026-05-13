# Task Generation

Back to [README](../README.md) · See also [hard-benchmark.md](hard-benchmark.md), [project-structure.md](project-structure.md), and [release-snapshot.md](release-snapshot.md)

## Output location

By default, generated outputs are written under:

- `openclaw_env/data/tasks`
- `openclaw_env/data/datasets`

Use `--output-data-dir` if you want to write to a separate root instead of the checked-in data tree.

## Regenerate the benchmark

```bash
python scripts/generate_tasks.py
```

## Hard benchmark generation knobs

The released `362`-task hard snapshot is one official profile, not a hard-coded ceiling.

Two layers matter:

- the shared base count, controlled by `--hard-decision-variants-per-scenario`
- explicit per-scenario overrides, controlled by `--hard-decision-scenario-counts`

If no explicit overrides are passed, unspecified hard scenarios fall back to the shared base count.

Useful flags:

| Flag | Purpose |
| --- | --- |
| `--hard-decision-variants-per-scenario <int>` | base hard count before applying the built-in scenario profile |
| `--hard-decision-scenario-counts a=INT,b=INT` | override specific hard-scenario counts |
| `--output-data-dir <path>` | write generated tasks to a custom root |
| `--complex-task-pack {off,standard}` | include or disable the auxiliary complex-workflow pack |
| `--complex-scenario-profile {legacy,life_work}` | choose the composed-workflow scenario set |
| `--include-branch-sensitive` | enable the experimental branch-sensitive family |

## Coverage reports

Generation writes coverage metadata to:

- [`../openclaw_env/data/datasets/generator_coverage_report.json`](../openclaw_env/data/datasets/generator_coverage_report.json)
- [`../openclaw_env/data/datasets/hard_split_coverage_report.json`](../openclaw_env/data/datasets/hard_split_coverage_report.json)

## Notes

- Hard-task metadata is stored in `TaskData.public`, including scenario name, ability tags, prompt style, and step count.
- Changing per-scenario counts changes the release profile, not the underlying task semantics.
- This public hardening pass does not claim to have refreshed the currently dirty `openclaw_env/data/...` worktree files.
