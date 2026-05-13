# OpenClaw Setup

Back to [README](../README.md) · See also [quickstart.md](quickstart.md) and [execution-modes.md](execution-modes.md)

`real` and `hybrid` require a working OpenClaw installation. `mock` and `multi` do not.

## Check the CLI

```bash
openclaw status --json
openclaw agents list --json
openclaw channels list --json
```

## Install into the active conda environment

```bash
conda activate CLI-Agent
npm config set prefix "$CONDA_PREFIX"
export PATH="$CONDA_PREFIX/bin:$PATH"
npm install -g openclaw@latest
openclaw --version
```

## Start the gateway

```bash
openclaw onboard --install-daemon
openclaw gateway status
openclaw status --json
```

## Bootstrap Google-backed providers

For online Calendar, Gmail, or Tasks providers, place a Google OAuth desktop client at `~/.openclaw/client_secret.json` and bootstrap the required channels.

Keep OAuth files outside the repository and never commit local token or client-secret JSON files.

```bash
python scripts/login_required_channels.py \
  --split dev \
  --google-client-secret-file ~/.openclaw/client_secret.json \
  --google-email-client-secret-file ~/.openclaw/client_secret.json \
  --email-provider auto
```

## Useful provider environment variables

- `OPENCLAW_ENV_EMAIL_PROVIDER=auto|google_api|himalaya|mock`
- `OPENCLAW_ENV_TASKS_PROVIDER=auto|google_api|mock`
- `OPENCLAW_ENV_CALENDAR_PROVIDER=auto|google_api|gcalcli|khal|mock`
- `OPENCLAW_ENV_ENABLE_ONLINE_DATA=1`
- `OPENCLAW_ENV_STRICT_ONLINE_DATA=1`
- `OPENCLAW_ENV_GOOGLE_GMAIL_SCOPES`
- `OPENCLAW_ENV_GOOGLE_TASKS_SCOPES`
- `OPENCLAW_ENV_HIMALAYA_ACCOUNT`
