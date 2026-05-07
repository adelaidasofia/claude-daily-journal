---
name: release-process
description: Maintainer-facing release procedure for claude-daily-journal — how to cut a tag, what the workflow does, what artifacts ship.
---

# Release Process

Maintainer-facing reference. User-facing release notes are in [`../CHANGELOG.md`](../CHANGELOG.md).

## Two install paths in parallel

1. **`claude plugin add`** (canonical path) — installs the plugin permanently into the user's Claude Code, surviving across sessions. Recommended for users who want the skill always available.
2. **`--plugin-url` quick-try** (Claude Code 2.1.129+) — loads the plugin for the current session only, against an existing vault. Frame as evaluation, not substitute.

The `--plugin-url` path requires a published GitHub release with a `.zip` artifact at the stable URL.

## Cut a release

```bash
# 1. Bump version in the manifest
#    .claude-plugin/plugin.json — "version": "X.Y.Z"
# 2. Add a CHANGELOG.md entry at the top
# 3. Commit on main
git add .claude-plugin/plugin.json CHANGELOG.md
git commit -m "chore: bump to vX.Y.Z"
git push origin main

# 4. Tag and push
git tag -a vX.Y.Z -m "vX.Y.Z — short summary"
git push origin vX.Y.Z
```

The tag push triggers `.github/workflows/release.yml`. Ships in seconds. GitHub release publishes with auto-generated notes from PRs merged since the previous tag.

Semver: `vX.Y.0` for new features, `vX.Y.Z` for fixes, `vN.0.0` for breaking changes.

## What `release.yml` does

1. **Checkout the tag's tree** — `actions/checkout@v6`.
2. **Validate plugin manifest** — confirms `.claude-plugin/plugin.json` exists and parses as JSON.
3. **Build staged tree** — `rsync` to `/tmp/claude-daily-journal`, excluding `.git`, `.github`, `node_modules`, `__pycache__`, `.venv`, `*.bak`, `.DS_Store`, secrets (`.env`, `.env.*`, `*.key`, `*.pem`, `*.pfx`, `*.p12`, `secrets.json`, `.zsh_secrets`). `.env.example` explicitly included.
4. **Archive** — `zip -rq` produces `claude-daily-journal.zip`; `tar czf` produces `claude-daily-journal.tar.gz`. Both have `claude-daily-journal/` at the archive root, which is what `--plugin-url` expects.
5. **Sign** — `sha256sum` produces `.sha256` files alongside both archives.
6. **Publish** — `gh release create $TAG --generate-notes` creates the release.

Single-trigger only (push:tags). No `workflow_dispatch`, so no untrusted-input handling required.

## Artifacts

| Asset | Purpose |
|---|---|
| `claude-daily-journal.zip` | Plugin archive consumable by `claude --plugin-url` |
| `claude-daily-journal.zip.sha256` | SHA256 of the zip |
| `claude-daily-journal.tar.gz` | Cross-platform alternative archive |
| `claude-daily-journal.tar.gz.sha256` | SHA256 of the tarball |

Stable URL pattern (latest, regardless of version):

```
https://github.com/adelaidasofia/claude-daily-journal/releases/latest/download/claude-daily-journal.zip
https://github.com/adelaidasofia/claude-daily-journal/releases/latest/download/claude-daily-journal.zip.sha256
```

## Privacy gating (PR-scoped)

`.github/workflows/lint.yml` includes a `privacy` job that fires on every pull request. Scans files **changed in the PR** for tokens that match the maintainer's local hookify guard at `hookify.no-personal-in-daily-journal.local.md`. Pre-existing committed content is never re-scanned. Pushes to main bypass — local hookify catches direct pushes.

If the maintainer's hookify rule changes, update the CI scan in `lint.yml` to match.

## Re-run a release

This workflow uses single-trigger (push:tags) and doesn't expose `workflow_dispatch` for re-runs. To rebuild a release, delete the tag and re-tag from the same commit:

```bash
git tag -d vX.Y.Z
git push origin --delete vX.Y.Z
gh release delete vX.Y.Z --yes
git tag -a vX.Y.Z -m "vX.Y.Z — re-run"
git push origin vX.Y.Z
```

If `workflow_dispatch` re-run capability is needed in the future, mirror the env-var pattern from `ai-brain-starter`'s `release.yml` (bind `${{ github.event.inputs.tag }}` to an env var, never inline into the run shell).

## See also

- `.github/workflows/release.yml` — the workflow itself
- `.github/workflows/lint.yml` — `privacy` job and JSON-validity gate
- `../CHANGELOG.md` — version history
