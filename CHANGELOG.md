# Changelog

## 2.0.0 — 2026-07-14

**True sync with ai-brain-starter.** The plugin's journal skill had quietly diverged from the `daily-journal` skill in ai-brain-starter for months. This release re-establishes ai-brain-starter as the source of truth and rewrites this skill as its standalone rendering. New `docs/SYNC.md` documents the policy, the adaptation rules, and the intentional deltas so divergence can't recur silently.

**Behavioral upgrades ported from ai-brain-starter:**

- **Capture-first contract** — the entry is SAVED from the user's first substantive message; everything after is in-place enrichment. Graceful exit at every step: the entry is never held hostage to the interview or the panel. A captured-and-abandoned entry is a valid, complete entry.
- **Resume-or-create (Step 0.0)** — a second `/journal` the same day resumes today's file instead of duplicating it. One calendar day = one growing entry.
- **3:45 AM day boundary** — a 2 AM entry files under the previous day, matching how people actually journal.
- **Narrating ≠ relitigating filter** — panel triggers no longer fire on retrospective mentions of closed decisions; only present-tense reweighing pulls a panelist.
- **Panel confirm scoped to enrichment** — the panel is shown in full before it's written next to the user's words; the save itself never waits on it.
- **Elevator emotions** — added Schadenfreude (Pride + corrupted Joy) and Overwhelm (any floor, flooding).
- **`gratitudes:` + `entry_status:` frontmatter** — queryable by the insights skill; capture-stage vs. enriched entries are distinguishable.

Carries forward everything from 1.4.0 (door, body-first check, shadow-twin probe, crisis protocol, movement capture). plugin.json bumped 1.4.0 → 2.0.0.

---

## 1.4.0 — 2026-07-14

**Movement mechanics: the journal now tracks how you move between floors, not just where you are.** Codified from a long research session on High-Rise movement dynamics (floor drivers, exits, loops, resilience direction).

- **Crisis protocol** — formal override section: crisis language stops all mechanics (no panel, no accountability, no door), witness-first response, nearest-rope question, support line surfaced once, entry saved verbatim. Mirrors the `/rise` Tier 2 safety override.
- **Body-first check (Step 4)** — low floors usually arrive body-first, story-second. Before accepting the user's causal story for a low floor, check sleep/food/movement/sunlight and record `body_check` frontmatter. Two or more "no" → name the possible body driver before analyzing the story.
- **Shadow-twin probe (Step 4)** — mandatory distinguishing question before tagging Acceptance, Neutrality, Peace, or Pride (vs Resignation, Apathy, Boredom, Confidence). Mislabeling is the #1 way people stay stuck; the mislabel itself is logged as signal.
- **Movement capture (Step 4)** — new frontmatter: `floor_yesterday`, `moved_because` (body | witness | rupture | rope | role | story), and `rope` (what pulled them up from a low floor). Builds each user's personal rope inventory and feeds transition/loop/resilience-direction analysis in the insights skill.
- **The door (new Step 6.5)** — every session ends with ONE small, dated, physical action matched to floor tier (map + door, never map alone). Includes the Maté guard: fresh, proportionate floors get a container ("feel it fully," "tell one person"), not an exit — fast isn't always healthy. `door:` saved to frontmatter; next session opens by checking it (`door_prev`).
- **Hand the naming back (Step 4)** — after ~30 entries, roughly weekly, the user names the floor before Claude does. The skill trains the muscle rather than becoming it.
- `skills/daily-journal/SKILL.md` version bumped 1.2.0 → 1.4.0; plugin.json 1.3.0 → 1.4.0.

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
