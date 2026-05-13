# Execution Modes

Back to [README](../README.md) · See also [evaluation.md](evaluation.md) and [openclaw-setup.md](openclaw-setup.md)

## Mode summary

| Mode | Behavior | Typical use |
| --- | --- | --- |
| `mock` | simulates `openclaw *` commands in process | unit tests and narrow backend checks |
| `multi` | routes each command family to its local backend or skill | default benchmark evaluation |
| `real` | runs `openclaw *` through the real CLI subprocess path while keeping routed local skills for the rest | integration testing |
| `hybrid` | runs a live OpenClaw gateway and the same routed skill stack, with optional online providers enabled | realistic end-to-end evaluation |

`multi` is the default benchmark mode because it preserves interactive state across command families without requiring a full online deployment.

## What changes by mode

The task schema and evaluator stay the same across modes. What changes is backend realization.

- In `mock`, the environment uses a narrow in-process mock path.
- In `multi`, commands are routed through the local backend and skill stack.
- In `real`, `openclaw *` is executed through the real CLI subprocess path.
- In `hybrid`, `openclaw` runs against a live gateway while the rest of the routed stack remains in place.

## Routing vs provider realization

Execution routing and provider realization are separate concerns.

In `real` and `hybrid`, command families such as `calendar`, `email`, `weather`, `tasks`, and `file` still execute through the normal routed path and therefore appear in traces, effects, and evaluator-visible state. The distinction is whether those skills stay local or trigger online provider behavior when configured.

## Practical guidance

- Use `mock` for unit tests and narrow runtime debugging.
- Use `multi` for benchmark development, reproducible evaluation, and most reported runs.
- Use `real` when you specifically need the real `openclaw` CLI subprocess path.
- Use `hybrid` when you want a live OpenClaw-backed run and accept the extra setup and provider variability.
