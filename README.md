# claude-daily-journal

A Claude Code plugin for conversational daily journaling with emotional floor detection, optional behavior accountability, and an optional advisory panel. Saves structured Obsidian markdown entries.

Built around the **High-Rise Emotional Altitude Scale** — a 22-level emotional framework that gives language to where you are, not just what happened.

---

## What it does

1. Interviews you conversationally (evening check-in, afternoon pulse, morning intention)
2. Identifies your emotional floor — the primary altitude you're operating from
3. Optionally tracks behavior patterns you care about: movement, sleep, focus, meditation
4. Optionally runs a panel of named advisors relevant to what came up
5. Saves a first-person Obsidian note with your voice in the body and panel commentary separated below a divider

The floor framework is the differentiator. Over time, your journal becomes a navigable dataset: which emotions appear most, what triggers them, how you move between floors, which patterns repeat across months and years.

---

## Install

```bash
claude plugin add github.com/adelaidasofia/claude-daily-journal
```

Or clone manually and add:

```bash
git clone https://github.com/adelaidasofia/claude-daily-journal ~/.claude/plugins/claude-daily-journal
claude plugin add ~/.claude/plugins/claude-daily-journal
```

Then in any Claude Code session:

```
/journal
```

On first use, Claude will ask for your vault path and preferences. Takes 60 seconds to configure, never asked again.

---

## Requirements

- Claude Code
- An Obsidian vault (any folder structure works — the skill adapts to yours)
- Nothing else required

**Optional integrations:**
- RescueTime MCP — if connected, Claude pulls your productivity data and uses it in the accountability check so the conversation is grounded in numbers, not story
- The insights plugin (companion skill) — runs weekly and monthly pattern analysis across your journal entries

---

## The High-Rise framework

The 34-floor emotional scale was developed by [Adelaida Diaz-Roa](https://github.com/adelaidasofia) as part of *The High-Rise Series*. Each floor has a name, a description, and a direction — Low Floors (1–18, reactive), Middle Floors (19–24, transitional), High Floors (25–34, generative). The framework was expanded from 16 → 22 → 34 floors by mapping ~150 named human emotions onto the building, surfacing distinctions the smaller schemas collapsed (Anger vs Frustration, Joy vs Excitement, Love vs Compassion vs Gratitude).

The goal is not to stay on high floors. It's to know which floor you're on, understand how you got there, and recognize the moves that take you somewhere else.

For people who don't want the floor framework: you can tell Claude "skip the floor identification" and it will do a plain interview-and-save without the altitude analysis.

---

## Configuration

On first use, preferences are saved to `[VAULT_PATH]/.journal-prefs.md`:

```markdown
vault_path: ~/Documents/MyVault
journal_folder: Journal/[YYYY-MM]
panel: enabled
accountability: enabled
movement_target: 4x/week
sleep_target: before midnight
focus_target: 2 blocks/day
```

Edit this file anytime to change your setup.

---

## Entry format

Each entry saves as:

```
[VAULT_PATH]/Journal/[YYYY-MM]/[Descriptive Title].md
```

With YAML frontmatter, a first-person narrative body in your voice, a behavior summary line, and a clearly-labeled panel section separated by a horizontal rule so your words are always distinguishable from the AI commentary.

---

## The advisory panel

The panel is an optional feature that pulls 3–5 named thinkers into a brief commentary after the interview. The panel roster includes public figures across wealth and strategy, psychology, relationships, health, leadership, wisdom, and creativity.

Each panelist speaks in their authentic voice. At least one dissents or challenges rather than validates. The commentary lives in a clearly-labeled section below your journal body — never blended into your original writing.

You can customize your panel, skip it entirely, or build your own roster by editing the SKILL.md.

---

## Submitting to the Cowork marketplace

Once your repo is on GitHub, submit at: **[clau.de/plugin-directory-submission](https://clau.de/plugin-directory-submission)**

Anthropic reviews for quality and safety before listing. The community marketplace (`anthropics/claude-plugins-community`) is a faster path for community submissions — add via:

```bash
claude plugin marketplace add anthropics/claude-plugins-community
```

---

## License

MIT
