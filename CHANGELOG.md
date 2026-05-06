# Changelog

## 1.3.0 — 2026-05-06

**Release infrastructure + `--plugin-url` quick-try path.** Plus rolling up the post-1.2.0 polish on the journal skill.

- **`.github/workflows/release.yml`** — tag-triggered builder. Validates `.claude-plugin/plugin.json` parses, builds clean `claude-daily-journal.zip` + `.tar.gz` (excludes `.git`, `.github`, secrets, build artifacts), generates SHA256 sums, publishes the GitHub release with auto-generated notes from PRs merged since the previous tag. Stable URL: `https://github.com/adelaidasofia/claude-daily-journal/releases/latest/download/claude-daily-journal.zip`.
- **`.github/workflows/lint.yml`** — JSON validity (plugin.json, mcp.json) and a PR-scoped `privacy` job that mirrors the maintainer's local hookify guard for external contributors.
- **README quick-try section** — documents the `claude --plugin-url` invocation for existing Claude Code 2.1.129+ users who want to try the skill against an existing vault without a full clone-and-add.
- **plugin.json bumped 1.0.0 → 1.3.0** — manifest had drifted behind the CHANGELOG (1.2.0 entry was on Apr 17 but plugin.json never bumped). This catches it up plus reflects the post-1.2.0 polish (verbatim rule strengthening + journal-vs-staging boundary, README 34-floor framework reference) that landed without a version bump.

**No action required** for existing installs. The `claude plugin add` install path continues to work unchanged.

---

## 1.2.0 — 2026-04-17

**Verbatim-capture rule added.** Every message the user types during a journal session now gets logged word-for-word in a dedicated `### My responses to the panel (verbatim, every message I typed back in this session)` subsection inside the entry. No paraphrase. No summary. No typo fixes.

**Why:** A journal that silently paraphrases is a journal you stop trusting. The narrative synthesis is the readable reflection; the verbatim subsection is the archive. Both coexist in every entry.

- `skills/daily-journal/SKILL.md`: entry template updated to include the verbatim subsection; new rule line added to Step 7 reinforcing the requirement alongside the separation rule. Version bumped 1.1.0 → 1.2.0.

---

## 1.1.0 — 2026-04-16

Initial public release as a standalone Claude Code plugin (split from `ai-brain-starter`).

- 34-floor emotional altitude framework (High-Rise)
- Optional behavior accountability (movement, sleep, meditation, focus)
- Optional advisory panel with required dissent and mid-interview trigger routing
- Bilingual EN/ES with floor aliases
- First-use setup wizard saved to `[VAULT_PATH]/.journal-prefs.md`
- Strict separation between user voice and synthetic panel voice
- Panel optional, framework optional — can run as a plain journal if desired
