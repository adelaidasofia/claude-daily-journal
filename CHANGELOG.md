# Changelog

## 1.5.0 — 2026-09-01

**The journal names your floor for you now.** Same journal-skill change as today's `ai-brain-starter` update, shipped in lockstep.

- **No more "you call it tonight — what floor?"** The skill used to hand the naming back to you about once a week, on the theory that it trains the muscle. In practice it asks you to do the one piece of work the assistant is best set up to do: by the time you see that question it has already pulled your whole day, read your entry history, and has the 34 floor definitions and the shadow-twin tests in front of it. You have a tired brain at midnight.
- **What it does instead:** names the floor, gives you the one thing that made it pick that floor over the one next door, then asks only whether that's right. Correcting it is the point — that's the check working, not you failing a quiz.
- **Shadow-twin question too:** it now tells you which twin it read and why, instead of testing you on the difference between Acceptance and Resignation.

## 1.4.0 — 2026-07-14

**Movement mechanics: the journal now tracks how you MOVE between floors, not just where you stand.** Same journal-skill changes as today's `ai-brain-starter` update, shipped in lockstep.

- **The door (new Step 6.5)** — every session closes with ONE small, dated, physical action matched to your floor, and tomorrow's session opens by asking whether it happened (new Step 1 door check; `door` / `door_prev` frontmatter). Includes the Maté guard: floors that deserve time get a container ("ten minutes to feel this fully"), not an exit.
- **Body-first check (Step 4)** — sleep, food, movement, sunlight checked before accepting the day's story, recorded as `body_check` frontmatter. Two or more "no" answers and the skill says so: some of this floor might be body, not story.
- **Shadow-twin probe (Step 4)** — one distinguishing question before tagging Acceptance, Neutrality, Peace, or Pride, because Resignation feels like Acceptance from the inside and the mislabel is how people stay stuck.
- **Movement capture (Step 4)** — `floor_yesterday` plus `moved_because` (body / witness / rupture / rope / role / story), and `rope` when something pulled you up from a low floor. Over months this builds your personal rope inventory: what reliably works for YOU.
- **Crisis protocol (new top-level section)** — a safety override that stops all mechanics, witnesses first, asks the nearest-rope question ("who or what would you get up for right now?"), surfaces a support line once, and still saves their words verbatim.
- **Hand the naming back** — once ~30 entries exist, roughly weekly the user names the floor before Claude does. The skill trains the muscle instead of becoming it.
- Entry-template frontmatter now carries a machine-readable `floor:` field (array form for elevator emotions) so the movement fields have something to read on the next session's lookup.
- `plugin.json` and the skill frontmatter both bumped to 1.4.0.

**No action required** for existing installs — new fields appear in entries as they're written; old entries don't need backfilling.

---

## 2026-05-08 — README quick-try min-version bumped to 2.1.133+

Tracking the `ai-brain-starter` floor bump for the same reason: 2.1.133 (released 2026-05-08) fixes a silent bug where subagents weren't discovering project/user/plugin skills via the Skill tool. The `/journal` flow cascades into the advisory-panel rule and can spawn humanizer + deconstruct calls. When that cascade runs inside a subagent, the pre-2.1.133 bug applies. Plus the parallel-session 401 race fix benefits anyone running multiple worktrees.

README quick-try line bumped 2.1.129+ → 2.1.133+. No manifest version bump (single-line documentation change). The full `claude plugin add` install path is unaffected.

---

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
