# Renovate config

Shared Renovate preset for timmo001's repositories. Consumers extend
`github>timmo001/renovate-config`, which reads `default.json` from `main`.

## Stack

- No `package.json`. Tools are pinned in `mise.toml` and locked in `mise.lock`.
  Keep it that way: don't add a package manager.
- Renovate validates the preset with `renovate-config-validator`.
- Prettier formats. hk runs the shared Markdown, YAML, Actions and shell lints
  from `timmo001/workflows`, pinned in `hk.pkl`.
- `.agents/skills/` is synced from `timmo001/skills` by `skills-lock.json`.
  Change those skills upstream, not in this repository.

## Checks

- `mise run check`: validates `default.json`.
- `mise run format:check`: Prettier. `mise run format` writes the fixes.
- `hk check --all`: the same lints as the pre-push hook. Run `hk install` once
  per clone to add the hook.

Run `mise run check` and `mise run format:check` before committing. The
`Validate` workflow runs them in CI.

## Rollout

Consumers pick up a change on their next Renovate run, so a broken preset breaks
every repository that extends it. Keep changes small, and push to `main` only
once the checks pass.
