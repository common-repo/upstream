# upstream

A [common-repo](https://github.com/common-repo/common-repo) upstream template providing shared development tooling for upstream repository authors.

## What's Included

| File | Purpose |
|------|---------|
| `.pre-commit-config.yaml` | Trailing whitespace, end-of-file, YAML lint, merge conflict, large file checks |
| `.github/workflows/ci.yaml` | Pre-commit checks and common-repo config validation |
| `.github/workflows/commitlint.yml` | Conventional commit enforcement on PRs |
| `.github/workflows/release.yaml` | Semantic release with GitHub App token auth (supports manual trigger via `workflow_dispatch`) |
| `.releaserc.yaml` | Semantic release configuration (conventionalcommits preset) |
| `commitlint.config.js` | Commitlint conventional config |

## Usage

Requires **common-repo >= 0.28.0**.

Add to your upstream repo's `.common-repo.yaml`:

```yaml
- repo:
    url: https://github.com/common-repo/upstream
    ref: v1.0.0
```

### Template Variables

The release workflow is templatized for GitHub App credentials. Override the defaults if your org uses different secret names:

```yaml
- repo:
    url: https://github.com/common-repo/upstream
    ref: v1.0.0

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
