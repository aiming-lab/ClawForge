# Running Evaluations

Back to [README](../README.md) · See also [quickstart.md](quickstart.md), [execution-modes.md](execution-modes.md), and [hard-benchmark.md](hard-benchmark.md)

## Primary entrypoint

The main evaluation command is:

```bash
python examples/train_and_eval.py
```

The flagship hard benchmark is typically run with:

```bash
python examples/train_and_eval.py \
  --agent llm \
  --task-prefix hard_decision_workflow_ \
  --split test \
  --mode multi \
  --max-steps 20
```

The CLI default step budget is `15`, but documented benchmark-facing runs in this repository generally set `--max-steps` explicitly.

## Common commands

Hosted OpenAI-compatible endpoint:

```bash
python examples/train_and_eval.py \
  --agent llm \
  --llm-provider openai \
  --llm-base-url https://api.example.com/v1 \
  --model Kimi-K2.5 \
  --task-prefix hard_decision_workflow_ \
  --split test \
  --mode multi \
  --max-steps 20 \
  --llm-max-tokens 192 \
  -v
```

Expert upper bound:

```bash
python examples/train_and_eval.py --agent expert --split dev
```

Small sanity check:

```bash
python examples/train_and_eval.py --agent llm --split dev --domain calendar --difficulty 1 --limit 10
```

## Useful output flags

- `--verbose-log PATH`: save the full command trace
- `--save-report PATH`: save structured JSON output
- `--llm-request-retries N`: retry provider failures
- `--llm-retry-backoff-s S`: backoff base for retries
- `--inter-task-sleep S`: throttle between tasks

Structured reports include provider-aware fields such as:

- `provider_failures`
- `provider_impacted_tasks`
- `provider_adjusted_accuracy`

## History modes

The rollout client supports three history policies:

- `full`: send the full interaction history
- `summary`: force the compressed-history path
- `auto`: use the benchmark's trimming logic

The current default rollout policy is `full`.

## Metrics

The evaluator reports:

- full-pass accuracy
- partial-credit average score (`avg_score`)
- scenario-level summaries
- primary-ability and overlapping-tag summaries
- provider-aware accounting such as `provider_failures` and `provider_impacted_tasks`

`avg_score` is the dataset mean of the per-task weighted aggregate score computed by the same evaluator used for full-pass accuracy. A run can therefore receive substantial partial credit even when it does not satisfy every required check.

## Baseline agents

| Agent | Class | Description |
| --- | --- | --- |
| `expert` | `ExpertAgent` | replays ground-truth commands |
| `random` | `RandomAgent` | samples commands randomly |
| `rule` | `RuleAgent` | keyword-matching heuristic |
| `llm` | `LLMAgent` | multi-turn LLM-driven command agent |
