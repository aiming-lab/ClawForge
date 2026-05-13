# Quick Start

Back to [README](../README.md) · See also [evaluation.md](evaluation.md), [execution-modes.md](execution-modes.md), and [release-snapshot.md](release-snapshot.md)

## Install

```bash
pip install -e .
pip install -e ".[dev]"
```

Optional Google-backed provider dependencies for online Calendar, Gmail, or Tasks paths:

```bash
pip install -e ".[google]"
```

## Generate the benchmark snapshot

```bash
python scripts/generate_tasks.py
```

By default this writes under `openclaw_env/data/{tasks,datasets}`.

## Run a first hard-benchmark evaluation

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
  --llm-timeout-s 45 \
  --llm-request-retries 4 \
  --llm-retry-backoff-s 4 \
  --inter-task-sleep 3 \
  -v \
  --verbose-log ./tmp/hard_test_verbose.log \
  --save-report ./tmp/hard_test_report.json
```

This uses the documented benchmark-facing protocol rather than the raw CLI defaults. The CLI default step budget is `15`, while standard hard-benchmark runs in this repository typically use `20`.

## Run Claude through a local LiteLLM proxy

Export the proxy settings:

```bash
export LITELLM_PROXY_KEY="your-litellm-proxy-key"
export LITELLM_PROXY_BASE_URL="http://127.0.0.1:4000/v1"
```

Then run:

```bash
python examples/train_and_eval.py \
  --agent llm \
  --llm-provider openai \
  --model claude-sonnet-4.6 \
  --task-prefix hard_decision_workflow_ \
  --split test \
  --mode multi \
  --max-steps 20 \
  --llm-max-tokens 1024 \
  -v
```

When `--llm-provider openai` is used with a `claude-*` model name, the client defaults to the local LiteLLM proxy URL and reads `LITELLM_PROXY_KEY` unless `--llm-base-url` or `--llm-api-key-env` is overridden.

## Common next steps

- [evaluation.md](evaluation.md): output interpretation and comparison commands
- [execution-modes.md](execution-modes.md): exact mode behavior
- [openclaw-setup.md](openclaw-setup.md): `real` and `hybrid` prerequisites
- [task-generation.md](task-generation.md): generator flags and release-profile overrides
