# Changelog

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
