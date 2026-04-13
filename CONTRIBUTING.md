# Contributing

Thanks for contributing to the GameForge S&Box egg project.

## Scope

This repository focuses on:
- Pterodactyl and Pelican egg definitions (`sandbox-pterodactyl.json`, `sandbox-pelican.json`)
- Container image build and runtime (`Yolk/Dockerfile`, `Yolk/entrypoint.sh`)

## Getting Started

1. Fork and clone the repository.
2. Create a branch for your change.
3. Make focused commits for one concern at a time.
4. Open a pull request with testing notes.

## Branch Naming

Suggested patterns:
- `fix/<short-description>`
- `feat/<short-description>`
- `docs/<short-description>`

## Contribution Guidelines

- Keep changes small and targeted.
- Preserve existing behavior unless the PR intentionally changes it.
- Prefer safe defaults in runtime startup logic.
- Document any new env vars or startup behavior in `README.md`.
- Update both egg JSON files (`sandbox-pterodactyl.json` and `sandbox-pelican.json`) when adding or changing variables.
- Update relevant docs when changing build or panel behavior.

## Testing Checklist

Before opening a PR:

1. Validate shell syntax:

```bash
bash -n Yolk/entrypoint.sh
```

2. Validate egg JSON files:

```bash
node -e "JSON.parse(require('fs').readFileSync('sandbox-pterodactyl.json','utf8')); console.log('ok')"
node -e "JSON.parse(require('fs').readFileSync('sandbox-pelican.json','utf8')); console.log('ok')"
```

3. Build image from repo root:

```bash
docker build --platform linux/amd64 -f Yolk/Dockerfile -t local/gameforge-sbox-egg:test .
```

4. Smoke test the image:

```bash
docker run --rm -it -v sbox-test:/home/container local/gameforge-sbox-egg:test start-sbox
```

5. Include startup log snippets in the PR when changing update or launch behavior.

## Pull Request Template (Recommended)

Include:
- What changed
- Why it changed
- Risk or compatibility impact
- How it was tested
- Any follow-up work

## Code Style

- **Shell**: keep scripts `bash`-safe, use `set -euo pipefail`, and prefer defensive defaults.
- **Dockerfile**: keep layers purposeful; avoid unnecessary runtime bloat. Runtime base is `steamcmd/steamcmd:alpine`.
- **JSON**: preserve formatting and valid schema structure for the respective panel's egg export format.

## Reporting Issues

When filing an issue, include:
- Relevant log output from `/home/container/logs/`
- `SBOX_*` env values (redact tokens and secrets)
- Current image tag
- Repro steps
