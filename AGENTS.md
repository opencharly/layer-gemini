# AGENTS.md — layer-gemini

Standalone candy repo for the `gemini` layer — the Google Gemini CLI installed
globally via npm under `~/.npm-global`, with a tmux agent profile. The candy
lives in `charly.yml` at the repo root and projects the `gemini` skill entity
(`family: coder`).

Canonical files:

- `charly.yml` — the `gemini:` candy entity and the `gemini-skill:` skill entity.
- `package.json` — pins `@google/gemini-cli`.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-coder:gemini` — the owning skill: the npm install story, the
  `~/.npm-global` layout, and the tmux agent profile. Load before editing or
  troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package
  sections). Load before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence: the pinned
  package-version check (`node -e` against `0.51.0`), the `~/.npm-global/bin/gemini`
  and `package.json` file checks, and the `gemini --version` stdout match.
- The `package.json` pin and the `check:` that asserts it are one unit: a
  version bump moves both.

## Modify this repo

- Edit the `gemini:` candy entity in `charly.yml` and the `package.json` pin
  together; keep the matching `gemini-skill:` entity in step.
- A version bump is the `package.json` version plus the `node -e` assertion in
  the first `check:` step.
- Keep the `terminal_profile:`/`agent_provide:` tmux block valid against the
  current schema.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
