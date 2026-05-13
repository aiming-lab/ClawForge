# Release Snapshot

Back to [README](../README.md) · See also [task-generation.md](task-generation.md), [hard-benchmark.md](hard-benchmark.md), and [results.md](results.md)

## What this page covers

This page explains what is treated as part of the checked-in ClawForge release snapshot and what can be regenerated locally.

## Checked-in release artifacts

The repository currently checks in benchmark-facing data under `openclaw_env/data/`, including:

- task specs under `openclaw_env/data/tasks/`
- split and coverage artifacts under `openclaw_env/data/datasets/`
- profile-specific task and dataset views under `openclaw_env/data/profiles/`
- base configuration fixtures under `openclaw_env/data/base_configs/`

The repository also checks in documentation-facing figure assets under `docs/assets/`.

## Locally regenerable artifacts

The standard regeneration command is:

```bash
python scripts/generate_tasks.py
```

That command can rebuild task specs, split files, and coverage metadata. It can also be pointed at a separate output root with `--output-data-dir` if you do not want to overwrite the checked-in tree.

## Scope note for this public hardening pass

This documentation pass does not refresh or regenerate the current dirty `openclaw_env/data/...` worktree contents. The docs describe the current checked-in snapshot, but they do not claim that every dirty data file was rebuilt or revalidated as part of this pass.

## Results artifacts

Repository-facing result figures in `docs/assets/` are treated as documented release artifacts. They are useful for documentation and paper alignment, but they are not a live leaderboard or a continuously refreshed scoreboard.
