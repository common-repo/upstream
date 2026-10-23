# upstream

A [common-repo](https://github.com/common-repo/common-repo) upstream template providing shared development tooling for upstream repository authors.

## What's Included

Applied to the consumer's root in order: `src/` first, then
[`common-repo/semantic-release`](https://github.com/common-repo/semantic-release)
v0.6.4, which in turn inherits `conventional-commits` and `pre-commit`.

| File | Source | Purpose |
|------|--------|---------|
| `.github/workflows/ci.yaml` | `src/` | Reusable CI (`workflow_call`): `prek` hooks, `common-repo validate` and `common-repo apply --dry-run`, and `script/test` when the repo has one |
| `cog.toml` | `src/` | Cocogitto config (tag prefix `v`, ignore merge commits), merged into an existing consumer `cog.toml` rather than overwriting it |
| `.github/workflows/release.yaml` | `semantic-release` | Cocogitto release-on-merge (bump, tag, GitHub Release) with GitHub App token auth (supports manual trigger via `workflow_dispatch`); overwrites the legacy npm `semantic-release` workflow still in `src/` |
| `.github/workflows/conventional-commits.yaml` | `conventional-commits` | Conventional commit enforcement on PRs (`cog check`) |
| `.github/workflows/pre-commit.yaml` | `pre-commit` | `prek` hooks on PRs |
| `.pre-commit-config.yaml` | `pre-commit`, `conventional-commits` | Trailing whitespace, end-of-file, YAML/TOML/JSON/XML, merge conflict, large file and private key checks, plus a `conventional-pre-commit` commit-msg hook |

## Usage

Requires **common-repo >= 0.28.0**.

Add to your upstream repo's `.common-repo.yaml`:

```yaml
- repo:
    url: https://github.com/common-repo/upstream
    ref: v2.2.1
```

### Template Variables

The release workflow is templatized for GitHub App credentials. Override the defaults if your org uses different secret names:

```yaml
- repo:
    url: https://github.com/common-repo/upstream
    ref: v2.2.1

- template-vars:
    GH_APP_ID_SECRET: YOUR_APP_CLIENT_ID
    GH_APP_KEY_SECRET: YOUR_APP_PRIVATE_KEY
    GH_APP_OWNER: your-org
```

| Variable | Default | Description |
|----------|---------|-------------|
| `GH_APP_ID_SECRET` | `COMMON_REPO_BOT_CLIENT_ID` | GitHub Actions secret name for the app ID |
| `GH_APP_KEY_SECRET` | `COMMON_REPO_BOT_PRIVATE_KEY` | GitHub Actions secret name for the app private key |
| `GH_APP_OWNER` | `common-repo` | GitHub org that owns the app |

### Required Secrets

Consumers must configure these repository or organization secrets:

| Secret | Description |
|--------|-------------|
| App ID secret (see `GH_APP_ID_SECRET`) | GitHub App client ID for release automation |
| App key secret (see `GH_APP_KEY_SECRET`) | GitHub App private key for release automation |

## License

[MIT](LICENSE)

## Joke

Why did the chicken cross the road?
