# upstream

Shared maintenance templates for upstream repository authors.

- `src/` is the distributed payload: `src/.github/workflows/ci.yaml`, `release.yaml`, and `src/cog.toml` are renamed into consumer roots by `.common-repo.yaml`; do not place agent indexes under `src/`.
- Root `.github/workflows/` runs this repository's `prek`, config-validation, template tests, Cocogitto commit, and release jobs. Root `.pre-commit-config.yaml` and `cog.toml` configure those jobs; `.releaserc.yaml` is legacy release configuration.
- `.common-repo.yaml` is both the local self-application and the consumer-facing source API; its YAML merge appends unique pre-commit arrays. TOML auto-merge recursively merges tables, replaces scalar conflicts, and uses the configured array mode (default replace).
- Validate with `common-repo validate && common-repo apply --dry-run`; run `script/test` for template-variable, payload, and workflow checks (requires Python 3 with **PyYAML**). Run `prek install` on new checkouts/worktrees, then `prek run --all-files`.

## Maintaining this index

- Update the affected `AGENTS.md` files in the same change when paths, responsibilities, commands, dependencies, or conventions change.
- Keep indexes brief: record semantic entry points and non-obvious constraints; link to existing documentation instead of duplicating it.
- Add a directory index only when it provides useful navigation beyond its parent; omit generated, vendored, and fixture trees.
- Every `AGENTS.md` must have a sibling `CLAUDE.md` containing only `@AGENTS.md`.
