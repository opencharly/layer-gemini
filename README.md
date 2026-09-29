# gemini

The Google Gemini CLI — `gemini` on `PATH` for AI coding assistance and search.

`gemini` installs the Gemini CLI globally via npm. It depends on `nodejs` and
ships a `package.json` pinning `@google/gemini-cli`, which the build installs
globally under `NPM_CONFIG_PREFIX` (`~/.npm-global`). The result is verifiable:
the `gemini` binary lands at `~/.npm-global/bin/gemini`, the scoped package is
unpacked under `~/.npm-global/lib/node_modules/@google/gemini-cli`, and
`gemini --version` exits cleanly and prints a semantic version. A CUE-validated
tmux profile exposes it through the same generic local/SSH/nested Charly agent
channel as the other terminal agents.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `gemini` |
| Requires | `@github.com/opencharly/layer-nodejs` |
| Binary | `~/.npm-global/bin/gemini` |
| Agent channel | `tmux` profile `gemini` (terminal, persistence required) |
| Service / port | none |

## How to use it

Compose the layer into an image: the image node names this repo in its inner
`candy:` list (the outer `candy:` key holds the image spec — `base:` plus the
list of candies):

```yaml
version: 2026.261.1747
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-gemini:v2026.243.0409'
```

Then, inside the built image:

```bash
gemini --version         # semantic version
gemini                   # interactive session
```

## Layout

- `charly.yml` — the `gemini:` candy entity: the `require:` dep, the `agent_provide:`
  / `terminal_profile:` blocks, and the `check:` steps.
- `package.json` — pins `@google/gemini-cli`.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Family skill: `/charly-coder:gemini`
- `/charly-coder:nodejs` — the required runtime dependency
- `/charly-coder:claude-code`, `/charly-coder:codex` — sibling AI CLIs
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
