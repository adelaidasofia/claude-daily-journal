# Sync policy — this plugin and ai-brain-starter

**Source of truth:** the `daily-journal` skill in [ai-brain-starter](https://github.com/mycelium-hq/ai-brain-starter) (`skills/daily-journal/SKILL.md`). This plugin is the **standalone rendering** of that skill for people who install it without the full AI Brain vault.

**Rule: improve the source first, port here second.** Never let the two evolve independently — that is how they diverged for months before v2.0.0 re-synced them.

## How to sync

1. Diff this repo's `skills/daily-journal/SKILL.md` against ai-brain-starter's.
2. Port every behavioral change, applying the adaptation rules below.
3. Bump this plugin's version + CHANGELOG; note the ai-brain-starter commit you synced to.

## Adaptation rules (what changes in the port)

The standalone plugin assumes: an Obsidian vault, optionally RescueTime MCP, and nothing else. Anything that depends on ai-brain-starter's vault infrastructure is adapted or dropped:

| ai-brain-starter feature | Standalone adaptation |
|---|---|
| `journal-preflight.py` + message/calendar/email/Slack fetchers (Step 0) | Dropped — RescueTime-only Step 0, skip silently if not connected |
| `journal-config.md` data-source toggles | `.journal-prefs.md` setup wizard |
| `/rise` morning pairing (Steps 0h, 1, 3.5) | Dropped — no rise skill ships standalone |
| `journal-index.json` for resume lookup | Frontmatter scan of the monthly folder |
| Gratitude group staging via iMessage/WhatsApp MCPs | Capture-only gratitude (still asked, still frontmatter-logged) |
| Step 9.5 first-journal telemetry (email-token funnel) | Dropped — plugin uses its own `hooks/install-ping.py` |
| User-specific accountability targets (gym 4x, etc.) | Config-driven generic targets from setup |
| Extended personal panel roster (personas, LatAm advisors, health team) | Public curated roster |
| `## Today` auto-pulled section, Session Captures, Deep Work Chain, weekly-focus file | Dropped or made conditional ("if the vault has one") |
| Panel Feedback Log auto-append (Step 9) | Dropped |

Everything else — capture-first contract, resume-or-create, 3:45 AM day boundary, crisis protocol, verbatim rule, separation rule, narrating≠relitigating filter, the 34-floor scale, shadow-twin probe, body-first check, movement capture (`floor_yesterday` / `moved_because` / `rope`), the door (Step 6.5, with Maté guard), hand-the-naming-back, omission pass, dissent requirement — is **identical behavior** in both and must stay identical.

## Companion skill

The `insights` skill (weekly/monthly movement reports: transition map, loop detection, resilience direction, rope inventory, door completion rate) lives in ai-brain-starter and is not shipped standalone yet. The frontmatter this plugin writes is designed to be consumed by it.

## Last sync

- **v2.0.0** (2026-07-14) — full re-sync after long divergence; ported capture-first contract, resume-or-create, day boundary, narrating≠relitigating, elevator-emotion additions (Schadenfreude, Overwhelm), gratitudes frontmatter, entry_status field, plus the movement-mechanics release (door, body-first check, shadow-twin probe, crisis protocol, movement capture) which landed in both simultaneously.
