# Renovate config

Shared dependency policy for my repositories.

## Usage

Add this to `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>timmo001/renovate-config"]
}
```

This follows the preset's default branch. Changes apply on the next Renovate run.
Keep repository-specific pins, custom managers and groups in the consumer config.

## Policy

- One-day release delay by default.
- Two hours for Effect packages, including compiler tooling, plus OpenCode, Pi,
  Herdr and Plannotator.
- No release delay for first-party dependencies or Git submodules.
- Coordinated Effect, OpenCode 1, OpenCode 2, OpenTUI, Lit and Oxlint groups.
  Effect compiler tooling stays outside the runtime group. Browser Control has
  its own release cycle and stays outside the OpenCode groups.
- The first-party Oxlint rules package updates independently, without a release delay.
- Recommended presets, a dependency dashboard, the `dependencies` label, and
  grouped GitHub Actions pinned to commit digests.

Package-family patterns cover new members without adding each package here.
Renovate's maintained monorepo groups cover other families, including Astro,
Babel, Tailwind CSS and Vitest.

Renovate owns release-age policy. pnpm consumers should set
`minimumReleaseAge: 0` in `pnpm-workspace.yaml`.

## Validation

Run `mise run check` to validate the preset with the pinned Renovate version.
