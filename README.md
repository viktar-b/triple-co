# contech-context project

This repository was initialized with `contech-context` so Codex and Cursor can
work with private construction and engineering corpora through a mounted SMFS
filesystem.

## Install the CLI

```bash
curl -LsSf https://get.ocr.pro/contech-context/install.sh | sh
```

## Reproduce this setup

```bash
contech-context install --repo .
contech-context use <container-tag> --repo .
cat ./memory/mount/profile.md
cd ./memory/mount && smfs grep "Focused construction or engineering question"
```

`contech-context use` records the container tag in `contech-context.lock`, makes
it the default, and mounts it at the repo's configured SMFS path.

## Supermemory API key

Mounting requires Supermemory auth. Prefer a user-level
`SUPERMEMORY_API_KEY` so every terminal, Codex session, and installed repo can
mount without relying on stale cached credentials.

Use `export SUPERMEMORY_API_KEY="<your-supermemory-api-key>"` for the current
macOS/Linux shell, add the same line to your shell profile to persist it, or
set `SUPERMEMORY_API_KEY` as a user environment variable on Windows. Verify
with `contech-context init --repo .`; `api_key_present` should be `true`. If
`contech-context use` reports `key_source: stored_credentials` and SMFS returns
`401`, the environment key is not visible to that shell or the stored
credentials are stale.

## Files added by contech-context

- `AGENTS.md`: repo-local Codex guidance.
- `.cursor/rules/`: Cursor rules for SMFS-first retrieval and citations.
- `.cursor/skills/`: Cursor skills for using and troubleshooting the workflow.
- `contech-context.lock`: managed bundle metadata plus the user-owned SMFS
  container allowlist and mount defaults.
- `./memory/mount/`: the default SMFS mount path after a corpus is mounted.

Do not store API keys or private corpus dumps in this repository. Use
`SUPERMEMORY_API_KEY` or stored SMFS credentials for mounting.
