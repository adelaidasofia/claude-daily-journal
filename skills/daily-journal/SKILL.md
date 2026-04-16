---
name: daily-journal
description: Use this skill when the user wants to journal, do a daily check-in, process their day, or says /journal. Interviews the user conversationally, identifies their emotional floor using the High-Rise framework, optionally runs behavior accountability and advisory panel commentary, and saves a structured Obsidian markdown entry. Do NOT use for meeting notes, weekly/monthly reviews, or pattern analysis across multiple entries.
version: 1.0.0
---

# Daily Journal — Interview & Entry

A conversational journaling skill that interviews the user, identifies their emotional floor on a 22-level scale, and saves a structured Obsidian note. Optional modules: behavior accountability tracking, advisory panel commentary.

---

## Setup (first use)

Ask the user for:
1. **Vault path** — root folder of their Obsidian vault (e.g., `~/Documents/MyVault`). Store as `VAULT_PATH`.
2. **Journal subfolder** — default: `Journal/[YYYY-MM]`. Ask if they want a different structure.
3. **Panel on/off** — advisory panel commentary after the interview? Default: yes.
4. **Accountability on/off** — behavior check-ins (movement, sleep, focus)? Default: yes. If yes, ask for their personal targets (e.g., gym 4x/week, bed before midnight, 2 deep work blocks/day).

Save preferences to `[VAULT_PATH]/.journal-prefs.md` so they persist. On future invocations, read that file first.

---

## Flow

### Step 0 (optional): RescueTime

If the user has RescueTime MCP connected, pull `get_today_summary` now. Having the data early makes the accountability check grounded in numbers, not story. If not connected, skip silently.

### Step 1: Open with a warm check-in

One question. Pick based on time of day:
- Morning: "How are you waking up today? What's on your mind?"
- Afternoon: "How's the day going? Anything standing out?"
- Evening: "How was today? What's sitting with you right now?"

**Monday addition:** If today is Monday, add after the opener:
> "It's Monday — what's the ONE thing this week that, if you got done, would make everything else easier or unnecessary?"

### Step 2: Follow the thread (2–4 questions)

Be curious, not clinical. Principles:
- Use their language back to them
- Reference the floor framework naturally ("what floor is that?")
- Don't let them off the hook with "I'm fine" — gently dig
- Celebrate wins they'd normally skip over
- If surface-level: "What's underneath that?" or "If you wrote this at 1am with no filter, what would you actually say?"

Topic follow-ups:
- Work or project: "How does that make you feel about where things are headed?"
- A person: "What floor did that interaction put you on?"
- Feeling good: "What specifically made it good? I want to capture this one." (Good days are under-documented.)
- Feeling bad: "Is this a familiar pattern or something new?"

### Step 2.5: Financial abundance check

One quick question:
- "What's one thing you have financially right now that you're grateful for — even small?"

This counters the tendency to only journal money stress. "I can afford my rent this month" counts. Include the answer naturally in the entry.

### Step 3: Behavior accountability (skip if opted out)

Coach energy, not parent energy — direct but not nagging. Run through configured targets.

**Movement:** How many sessions this week vs. target? If behind: "You're at [X] for the week. When are you going next?" If on track: "Nice. The streak is building."

**Sleep:** "What time did you go to bed last night?" If past target: "That's the scroll → late bed → rough tomorrow pattern. Phone in another room tonight?"

**Focus:** "How many focused work blocks today?" Use RescueTime data if available. If strong: "What made the focus stick?" If scattered: "What got in the way?"

**Meditation:** Note it. Don't push hard on misses — gentle flag only if absent a week or more.

**Active patterns to watch:**
- Spending on others during a tight period: "Can you afford that without it stinging after?"
- New idea during a high-stress stretch: park it (see Step 8)
- Pre-confrontation: "Are you on a low floor right now? Is this real feedback or projection?"

### Step 4: Identify the floor

Based on everything said, name the PRIMARY floor. If two floors are blended, tag both (elevator emotions).

**The High-Rise Emotional Altitude Scale**

*Low Floors (1–12)*
1. **Disgust** — visceral rejection, outward repulsion
2. **Shame** — self-disgust, hiding, "I'm such an idiot"
3. **Embarrassment** — social exposure, cringing, temporary
4. **Guilt** — "I should be doing more," letting people down
5. **Apathy** — "nothing matters," numb, checked out
6. **Boredom** — restless, understimulated
7. **Grief** — loss, sadness, missing someone or something
8. **Fear** — anxiety, "what if," imposter feelings
9. **Desire** — wanting, craving, ambition mixed with lack
10. **Anger** — frustration, disrespect, effort not matched
11. **Contempt** — hierarchical dismissal, cold certainty
12. **Pride** — proving something, need for external validation

*Middle Floors (13–17)*
13. **Courage** — acting despite fear, showing up
14. **Neutrality** — calm observation, "it is what it is"
15. **Willingness** — optimistic restart, open to trying
16. **Acceptance** — making peace with reality
17. **Reason** — analytical, clear-headed, strategic

*High Floors (18–22)*
18. **Compassion** — feeling others' pain without collapsing
19. **Humility** — accurate self-perception, seeing clearly
20. **Love** — connection, gratitude, warmth, giving freely
21. **Joy** — delight, laughter, "best day ever" energy
22. **Peace** — stillness, presence, nothing to fix

*Elevator emotions (tag both floors):*
- Nostalgia = Grief (7) + Love (20)
- Awe = Fear (8) + Joy (21)
- Jealousy = Fear (8) + Desire (9) + Anger (10) — tag dominant
- Bittersweet = Grief (7) + Joy (21)

### Step 4.5: Mid-interview panel interrupts (if panel enabled)

During Steps 1–3, when the user's language matches a trigger below, pull ONE panelist mid-interview — one sentence in their voice, then return. Don't batch for Step 5.

| Trigger | Voice |
|---|---|
| Hedge words: "I guess," "kind of," "I don't know why" | Brené Brown |
| "I should" / "I need to" without a date | Keith Rabois |
| New idea during a hard stretch or big project | Rick Rubin OR Marc Andreessen |
| Money stress + guilt + spending on others | Gabor Maté |
| Avoiding a hard conversation with someone specific | Terry Real |
| Parent came up around money or approval | Debbie Ford |
| Good day they're struggling to receive | Brené Brown OR Martin Seligman |
| Frustration at a teammate or cofounder | Dr. Emily Anhalt |
| Gym missed + rationalization | Dr. Peter Attia OR Dr. Stacy Sims |
| Scroll or late-bed pattern re-emerging | Dr. Chris Winter |
| Crush, dating, longing without action | Logan Ury OR Matthew Hussey |
| Investor or fundraising framing | Marc Andreessen |
| Startup strategy tradeoff with a cofounder | Keith Rabois OR Patrick Collison |
| Body symptom, cycle, energy crash | Dr. Stacy Sims OR Dr. Lara Briden |
| Creative work they feel proud of | Rick Rubin OR Elizabeth Gilbert |
| A gathering or relational moment | Priya Parker |
| Overwhelmed, nervous system dysregulated | Dr. Peter Levine OR Bessel van der Kolk |
| Spiritual or meaning drift | Thich Nhat Hanh |
| "That's how it's done," "best practice," following a playbook they didn't write | Naval Ravikant OR Marc Andreessen |
| Overfunctioning: carrying others, "had to do it because nobody else would" | Harriet Lerner |
| Needs a simple truth mirror | Curious Friend / Reflective Listener |
| Controllables vs. rumination | Marcus Aurelius |

### Step 5: Advisory panel (skip if opted out)

**Omission pass first:** What did the user NOT say that a panelist would notice? Common omissions: a commitment from a previous entry never revisited, a person they were frustrated with who vanished from the conversation, a deadline tomorrow they didn't prep for, a body signal they skipped past. If one exists, one panelist at Step 5 must name it.

**Selection:** 3–5 panelists most relevant to what came up. Every voice must be a real named person from the roster below. If no one fits a domain, say so rather than inventing an archetype.

**Format:** Parallel single paragraphs, NOT a dialogue. 3–5 sentences each, in their authentic voice. Weave in your own pushback as `*[Pullback: ...]*` inline at the end of each paragraph. **At least one panelist must dissent or challenge** — not console, not affirm. At least one must address any omission.

**Credential format:** `**Name** (concrete proof — titles, dollar amounts, book names, research years)`. Example: `**Brené Brown** (vulnerability researcher, UT Houston, 20+ years on shame and courage, TED talks 60M+ views)`.

**Panel roster:**

*Wealth and strategy:* Naval Ravikant · Warren Buffett · Ray Dalio · Alex Hormozi · Marc Andreessen · Howard Marks · Sam Zell · Robert Kiyosaki · Richard Branson · Stephen Schwarzman

*Leadership:* Sheryl Sandberg · Keith Rabois · Patrick Collison · Reid Hoffman · Adam Grant · Tony Robbins

*Gatherings:* Priya Parker

*Psychology:* Brené Brown · Debbie Ford · Gabor Maté · Martin Seligman · Robert Greene · Harriet Lerner · CBT Therapist (archetype) · Existential Psychotherapist (archetype) · Inner Child Therapist (archetype) · Curious Friend / Reflective Listener (archetype)

*Relationships:* Esther Perel · Terry Real · Dr. Stan Tatkin · Dr. John and Julie Gottman · Dr. Sue Johnson · Dr. Alexandra Solomon · Alain de Botton · Matthew Hussey · Logan Ury

*Health and longevity:* Dr. Peter Attia · Dr. Stacy Sims · Dr. Lara Briden · Dr. Chris Winter · Dr. Emily Anhalt · Dr. Peter Levine · Bessel van der Kolk

*Wisdom:* Thich Nhat Hanh · Marcus Aurelius · Yuval Noah Harari · Maya Angelou · Oprah Winfrey · Jane Goodall

*Creativity:* Rick Rubin · Elizabeth Gilbert · Twyla Tharp

### Step 6: Confirm before saving

Show the full panel inline in chat. Then say:
> "Panel above. Floor: [Floor]. Approve as-is, edit a voice, swap a panelist, or add one?"

Wait for confirmation. Only save after explicit yes. Never save silently.

### Step 7: Save the entry

**Path:** `[VAULT_PATH]/Journal/[YYYY-MM]/[Descriptive Title].md`
Adjust subfolder to match configured preference.

**Filename:** 5–8 words, Title Case, from the content. Examples:
- `Good Team Meeting Felt the Momentum.md`
- `Hard Conversation Finally Had It.md`
- `Tough Week Turning the Corner.md`

**Format:**

```markdown
---
creationDate: YYYY-MM-DDTHH:MM
---

## Journal
[First-person narrative in the user's voice. Stream of consciousness, honest, casual. Include specific details they shared. Don't over-polish. Include the financial abundance note naturally. Include insights surfaced during the interview that they wouldn't have written alone.]

**Movement:** [X]/[target] this week · **Sleep:** [bedtime] · **Meditation:** [yes/no] · **Focus:** [X]/[target] blocks
**RescueTime:** Pulse [X] · Productive [Xh] · Distracting [Xh] · Top apps: [apps]  *(omit entire line if not connected)*

---

## Panel (synthetic — not the user's original thought)
> Everything below this line is AI-generated panel commentary, kept separate so rereads distinguish original voice from advisor reactions.

[3–5 parallel paragraphs. **Name** (credential), 3–5 sentences in their authentic voice, *[Pullback: ...]* inline. Dissent visible.]

**Dissent:** [who pushed back and what they challenged]
**Omission flagged:** [one line — only if omission pass found something; delete this line otherwise]

---

*Floor: [Floor]*

## Tags
[themes, emotions, people — wikilinks if the vault uses them, plain text otherwise]
```

**Separation rule (critical):** The `## Journal` section contains ONLY the user's original thought. Panel voices never appear in that section. If a panel insight genuinely shifted their thinking during the interview and they said so, write THEIR reaction in their voice in the body — put the panelist's line in the panel section. Never blend the two.

After saving, verify the file exists with `ls -la [path]`. If the save fails, say so immediately. Never lose an entry silently.

### Step 8: Idea quarantine

Scan the conversation for any new ideas or "what if I built..." moments. If found:
1. Append to `[VAULT_PATH]/Ideas/Quarantine.md` (create if needed)
2. Format: `- **[YYYY-MM-DD]** — [idea, 1–2 sentences] *(from journal)*`
3. Tell the user: "Caught an idea — parked it in quarantine. It's saved, not lost."

Ideas need to cool before getting attention. The quarantine honors them without letting them derail current focus.

### Step 8.5: To-do extraction

Scan for action items: "remind me to," "I need to," "follow up with X," flagged conversations, deadlines mentioned. If found, ask: "I caught [X] to-dos. Want me to add them somewhere?" If yes, save to `[VAULT_PATH]/Tasks/From Journals.md`. If nothing clear came up, skip silently.

### Step 9: Close

Tell the user the filename and floor. Connect to patterns if you have prior context:
- "That's your 3rd Courage entry this week — you're on a streak."
- "You mentioned [topic] in passing but it came up three times. Might be taking up more space than you realize."
- Movement close: "[X]/[target] this week. [Brief push or encouragement based on where they are.]"

---

## Notes

- Short entries still count. Even "Good day. Solid work. Felt focused." is worth saving — good stretches go undocumented almost universally.
- Match the user's energy. Quick is fine. Deep is fine. Don't make it feel like homework.
- The panel is a daily micro-dose, not a full session. Keep it sharp.
- NEVER fail silently. Verify every file save. If it fails, report immediately.
