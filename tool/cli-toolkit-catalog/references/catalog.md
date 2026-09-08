# CLI Tool Category Catalog

## Package Runners

The `npx`, `bunx`, and `uvx` commands below are not system-installed binaries
but package runners that download and execute npm or PyPI packages on-the-fly.

**npx**: executes npm packages without a global install.

**bunx**: executes npm packages via the Bun runtime (faster than npx).
In most cases `bunx` can replace `npx`; if the user's primary runtime is Bun,
the agent may substitute `bunx` for `npx` freely.
This catalog only uses `npx` in examples for consistency.

**uvx**: executes PyPI packages without a virtual-env setup.

| Tool | Command | When to use |
|------|---------|---------|
| npx | `npx` | One-off npm package execution without a global install |
| bunx | `bunx` | npm package execution through the Bun runtime |
| uvx | `uvx` | PyPI application execution without a virtual environment |

## Text & Data

| Tool | Command | When to use |
|------|---------|---------|
| jq | `jq` | Querying or transforming JSON |
| yq | `yq` | Querying or transforming YAML, TOML, XML, or CSV |
| ripgrep | `rg` | Recursive file-name or text searches; prefer it over grep for most searches |

## File Archiving

| Tool | Command | When to use |
|------|---------|---------|
| gzip | `gzip` | Compressing or decompressing gzip data |
| tar | `tar` | Creating or extracting tar archives |
| zip / unzip | `zip` / `unzip` | Creating or extracting ZIP archives |
| zstd | `zstd` | Compressing or decompressing Zstandard data |

## Network

| Tool | Command | When to use |
|------|---------|---------|
| curl | `curl` | General-purpose HTTP requests from the command line |
| dra | `dra` | Downloading GitHub release assets, with automatic selection for the current OS and architecture or optional executable installation |

## Media Processing

| Tool | Command | When to use |
|------|---------|---------|
| ffmpeg | `ffmpeg` | Converting or processing audio and video |

## Shell Utilities

| Tool | Command | When to use |
|------|---------|---------|
| busybox | `busybox` | Unix utilities unavailable natively, especially on Windows |
| tlrc | `tldr` | Quick command examples instead of a full manual |
| [bkt] | `bkt` | Reusing cached results of expensive commands within a chosen TTL, such as repeated `curl` GET requests where briefly stale responses are acceptable |

### Unix Shell Utilities

These tools are natively available on Linux/macOS.
On Windows, it should prefix with `busybox` (e.g. `busybox dos2unix`).

| Tool | Command | When to use |
|------|---------|---------|
| dos2unix | `dos2unix` | Converting line endings from CRLF to LF |
| unix2dos | `unix2dos` | Converting line endings from LF to CRLF |

## Encoding & Conversion

| Tool | Command | When to use |
|------|---------|---------|
| base64 | `base64` | Encoding or decoding Base64 data |

## Linting

| Tool | Command | When to use |
|------|---------|---------|
| [editorconfig-checker] | `editorconfig-checker` | Validating repository files against `.editorconfig` rules |

## Scaffolding

| Tool | Command | When to use |
|------|---------|---------|
| tiged | `npx tiged` | Repository snapshots without Git metadata; prefer it over `git clone --depth 1` for inspection, templates, or project bootstrapping |

## Skill Management

| Tool | Command | When to use |
|------|---------|---------|
| skills | `npx skills` | Installing or managing agent skills |

## Further reference

This catalog intentionally omits all flags and detailed usage.
Run `<command> --help` for full documentation unless an explicit exception is documented here.
Do not search the web for tool docs when `--help` is available locally.

[editorconfig-checker]: https://github.com/editorconfig-checker/editorconfig-checker
[bkt]: https://github.com/dimo414/bkt
