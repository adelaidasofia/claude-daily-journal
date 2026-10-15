# claude-daily-journal


<!-- mycelium-badges:start -->

<p>
  <a href="https://github.com/adelaidasofia/claude-daily-journal/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/github/license/adelaidasofia/claude-daily-journal?color=blue"></a>
  <a href="https://github.com/adelaidasofia/claude-daily-journal/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/adelaidasofia/claude-daily-journal?color=eab308"></a>
  <a href="https://github.com/adelaidasofia/claude-daily-journal/commits/main"><img alt="Last commit" src="https://img.shields.io/github/last-commit/adelaidasofia/claude-daily-journal"></a>
  <a href="https://github.com/adelaidasofia/claude-daily-journal/issues"><img alt="Open issues" src="https://img.shields.io/github/issues/adelaidasofia/claude-daily-journal"></a>
  <a href="https://myceliumai.co"><img alt="Built by Mycelium AI" src="https://img.shields.io/badge/built_by-Mycelium_AI-15B89A"></a>
</p>

<!-- mycelium-badges:end -->

A Claude Code plugin for conversational daily journaling with emotional floor detection, optional behavior accountability, and an advisory panel on every entry (on by default, one setting turns it off). Saves structured Obsidian markdown entries from your first message.

Built around a **34-floor emotional altitude scale** — a framework that gives language to where you are, not just what happened.

---

## What it does

1. Interviews you conversationally (evening check-in, afternoon pulse, morning intention)
2. Identifies your emotional floor — the primary altitude you're operating from
3. Optionally tracks behavior patterns you care about: movement, sleep, focus, meditation
4. Runs a panel of named advisors relevant to what came up: a quick first take the moment your entry is saved, then the full panel once your floor is named (on by default, and you can turn it off)
5. Saves your entry from your first message, so a quick check-in is never lost, then keeps updating that same note as you go. Your voice stays in the body, with the panel commentary separated below a divider

The floor framework is the differentiator. Over time, your journal becomes a navigable dataset: which emotions appear most, what triggers them, how you move between floors, which patterns repeat across months and years.

---

## Install

Open Claude Code, paste:

    /plugin marketplace add adelaidasofia/claude-daily-journal
    /plugin install claude-daily-journal@claude-daily-journal

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

## The 34-floor framework

Each floor has a name, a description, and a direction — Low Floors (1–18, reactive), Middle Floors (19–24, transitional), High Floors (25–34, generative). The framework was expanded from 16 → 22 → 34 floors by mapping ~150 named human emotions onto the building, surfacing distinctions the smaller schemas collapsed (Anger vs Frustration, Joy vs Excitement, Love vs Compassion vs Gratitude).

The goal is not to stay on high floors. It's to know which floor you're on, understand how you got there, and recognize the moves that take you somewhere else.

For people who don't want the floor framework: you can tell Claude "skip the floor identification" and it will do a plain interview-and-save without the altitude analysis.

---

## Configuration

On first use, preferences are saved to `[VAULT_PATH]/.journal-prefs.md`:

```markdown
vault_path: ~/Documents/MyVault
journal_folder: Journal/[YYYY-MM]
panel: enabled
panel_log: Journal/Panel Feedback Log.md   # optional; this is the default
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

One day is one entry. The note is written the moment you share something real, and a second `/journal` the same day picks up that same note instead of starting a new one.

---

## The advisory panel

The panel pulls 3–5 named thinkers into a brief commentary on your entry. The roster includes public figures across wealth and strategy, psychology, relationships, health, leadership, wisdom, and creativity.

It runs in two passes. A first take of three voices lands in the same reply that saves your entry, so even a two-line check-in gets one. The full panel replaces it in the reply that names your floor. Every panel is shown to you in chat before it is written to your note, and nothing waits for your approval: cut, swap or add a voice whenever you like.

Each panelist speaks in their authentic voice. At least one dissents or challenges rather than validates, and every dissent is collected in a Panel Feedback Log (`Journal/Panel Feedback Log.md` by default), so a pushback that keeps coming back is easy to spot. The commentary lives in a clearly-labeled section below your journal body, never blended into your original writing. If you journal more than once in a day, each session adds its own panel block and never rewrites an earlier one.

Say "no panel" during a session and that session gets a one-line note instead. Set `panel: disabled` in your prefs to turn the panel off entirely. You can also customize your panel or build your own roster by editing the SKILL.md.

---

## Submitting to the Cowork marketplace

Once your repo is on GitHub, submit at: **[clau.de/plugin-directory-submission](https://clau.de/plugin-directory-submission)**

Anthropic reviews for quality and safety before listing. The community marketplace (`anthropics/claude-plugins-community`) is a faster path for community submissions — add via:

```bash
claude plugin marketplace add anthropics/claude-plugins-community
```

---


## Telemetry

This plugin sends a single anonymous install signal to `myceliumai.co` the first time it loads in a Claude Code session on a given machine.

**What is sent:**
- Plugin name (e.g. `slack-mcp`)
- Plugin version (e.g. `0.1.0`)

**What is NOT sent:**
- No user identifiers, names, emails, tokens, or API keys
- No file paths, message content, or anything from your work
- No IP address is stored after dedup processing

**Why:** Helps the maintainer know which plugins people actually install, so attention goes to the ones that get used.

**Opt out:** Set the environment variable `MYCELIUM_NO_PING=1` before launching Claude Code. The hook will skip the network call entirely. Already-pinged installs leave a sentinel at `~/.mycelium/onboarded-<plugin>` — delete it if you want to reset state.

## License

MIT

---

<details>
<summary>Legacy install</summary>

Earlier Claude Code versions used different install commands. If the new `/plugin marketplace add` syntax is unavailable, these still work:

```bash
claude plugin add github.com/adelaidasofia/claude-daily-journal
```

Or clone manually and add:

```bash
git clone https://github.com/adelaidasofia/claude-daily-journal ~/.claude/plugins/claude-daily-journal
claude plugin add ~/.claude/plugins/claude-daily-journal
```

### Quick-try (Claude Code 2.1.133+)

For a one-command session-scoped trial without a permanent install:

```bash
claude --plugin-url https://github.com/adelaidasofia/claude-daily-journal/releases/latest/download/claude-daily-journal.zip
```

This loads the plugin for the current session only.

</details>
