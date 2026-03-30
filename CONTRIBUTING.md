# Contributing

Thanks for contributing to the GameForge S&Box egg project.

## Scope

This repository focuses on:
- Pterodactyl egg behavior (`sandbox-pterodactyl.json`)
- Container image build/runtime (`Yolk/DockerFile`, `Yolk/entrypoint.sh`)

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
- Document any new env vars or startup behavior.
- Update relevant docs when changing build or panel behavior.

## Testing Checklist

Before opening a PR:

1. Validate shell syntax:

```bash
bash -n Yolk/entrypoint.sh
```

2. Build image from repo root:

```bash
docker build --platform linux/amd64 -f Yolk/DockerFile -t local/gameforge-sbox-egg:test .
```

3. If your change touches egg variables, verify `sandbox-pterodactyl.json` values and defaults.

4. Include startup log snippets in PR when changing update/start behavior.

## Pull Request Template (Recommended)

Include:
- What changed
- Why it changed
- Risk or compatibility impact
- How it was tested
- Any follow-up work

## Code Style

- Shell: keep scripts POSIX/Bash-safe and defensive.
- Dockerfile: keep layers purposeful and avoid unnecessary runtime bloat.
- JSON: preserve formatting and valid schema structure for Pterodactyl export.

## Reporting Issues

When filing an issue, include:
- Relevant logs
- `SBOX_*` env values (redact secrets)
- Current image tag
- Repro steps
