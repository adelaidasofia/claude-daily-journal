---
name: daily-journal
description: Use this skill when the user wants to journal, do a daily check-in, process their day, or says /journal. Interviews the user conversationally, identifies their emotional floor using the High-Rise framework, optionally runs behavior accountability and advisory panel commentary, and saves a structured Obsidian markdown entry. Do NOT use for meeting notes, weekly/monthly reviews, or pattern analysis across multiple entries.
version: 1.1.0
---

# Daily Journal — Interview & Entry

A conversational journaling skill that interviews the user, identifies their emotional floor on a 34-level scale, and saves a structured Obsidian note. Optional modules: behavior accountability, advisory panel commentary.

**The High-Rise framework** is the core differentiator: 34 floors from Disgust to Peace. Not a ladder to climb once — rooms you move between. The question is not where you are, it's whether you know. Full framework: https://adelaidadiazroa.substack.com/s/internal-design

---

## Setup (first use)

Ask the user for:
1. **Vault path** — root folder of their Obsidian vault (e.g., `~/Documents/MyVault`). Store as `VAULT_PATH`.
2. **Journal subfolder** — default: `Journal/[YYYY-MM]`.
3. **Panel on/off** — advisory panel after the interview? Default: yes.
4. **Accountability on/off** — behavior check-ins? Default: ask. If yes, ask for their targets.

Save to `[VAULT_PATH]/.journal-prefs.md`. Read on every future invocation before starting.

---

## Flow

### Step 0 (optional): RescueTime

If the user has RescueTime MCP connected, pull `get_today_summary` now — grounds the accountability check in data, not story. Skip silently if not connected.

### Step 1: Open check-in

One question. Pick based on time of day:
- Morning: "How are you waking up today? What's on your mind?"
- Afternoon: "How's the day going? Anything standing out?"
- Evening: "How was today? What's sitting with you right now?"

**Monday:** Add after the opener: "It's Monday — what's the ONE thing this week that, if done, would make everything else easier or unnecessary?"

### Step 2: Follow the thread (2–4 questions)

Curious, not clinical. Use their language. Push gently where they'd skip.
- Work/project: "How does that make you feel about where things are headed?"
- A person: "What floor did that interaction put you on?"
- Feeling good: "What specifically made it good? I want to capture this one."
- Surface-level: "What's underneath that?" or "If you wrote this at 1am with no filter, what would you say?"

### Step 2.5: Gratitude check (optional — offer, don't force)

Offer: "Want to capture one thing you're grateful for today — financial, relational, anything?" This counters the tendency to only document struggle. If they decline, skip it. If they answer, include it naturally in the entry.

### Step 3: Behavior accountability (skip if opted out)

Coach energy, not parent energy. Run through whichever targets the user configured.

**Movement:** How many sessions this week vs. target? If behind: "You're at [X]. When are you going next?" If on track: "The streak is building."

**Sleep:** "What time did you go to bed last night?" If past target: "That's the scroll → late bed → rough tomorrow pattern."

**Focus:** "How many focused work blocks today?" Use RescueTime data if available.

**Meditation:** Note it. Gentle flag only if absent a week or more — don't push.

**Patterns to watch:**
- New idea during a hard stretch or high-pressure period: park it (Step 8)
- Pre-confrontation: "Are you on a low floor right now? Is this real feedback or projection?"

### Step 4: Identify the floor

Name the PRIMARY floor. If two floors are blended simultaneously, tag both (those are elevator emotions — see below).

**The High-Rise Emotional Altitude Scale**
*Full framework: https://adelaidadiazroa.substack.com/s/internal-design*

*Low Floors (1–18) — Reactive:*
1. **Disgust** — outward rejection, "get it away from me"
2. **Shame** — self-annihilation, hiding, "I am the problem"
3. **Embarrassment** — social exposure, temporary, recoverable
4. **Guilt** — "I should be doing more," productive self-blame
5. **Apathy** — checked out, numb, nothing matters
6. **Resignation** — shadow of Acceptance, defeated awareness (NOT the same as making peace)
7. **Confusion** — mind reaching and failing, not knowing which way
8. **Loneliness** — surrounded but unfound
9. **Boredom** — understimulated agency (the TRAMPOLINE floor — low with upward spring)
10. **Grief** — loss, letting go, something ended
11. **Disappointment** — gap between hope and what arrived
12. **Hurt** — breach in a relationship
13. **Fear** — anxiety, threat detection, "what if"
14. **Frustration** — blocked energy, trying and failing
15. **Desire** — wanting, ambition mixed with lack
16. **Anger** — directed energy, "this is wrong"
17. **Contempt** — hierarchical dismissal, cold certainty
18. **Pride** — proving, need for external validation

*Middle Floors (19–24) — Transitional:*
19. **Courage** — action despite fear (the floor where everything changes)
20. **Hope** — future-facing trust, the most common emotion in long-term journals
21. **Neutrality** — calm observation, "it is what it is"
22. **Willingness** — curiosity replacing fear, open to trying
23. **Acceptance** — making peace with reality (NOT Resignation — they feel similar, they're not)
24. **Reason** — analytical, clear-headed, ceiling of the mind

*High Floors (25–34) — Generative:*
*On the high floors the ego quiets. Distinctions narrow not because they matter less, but because the self becomes lighter.*
25. **Trust** — quiet confidence that things hold
26. **Compassion** — empathy with altitude, feeling without collapsing
27. **Humility** — accurate self-perception, seeing clearly
28. **Belonging** — being received, "I'm in the right room"
29. **Love** — overflow, giving freely
30. **Gratitude** — presence recognizing abundance
31. **Excitement** — anticipatory joy, body saying yes
32. **Wonder** — awe at what exists
33. **Joy** — aliveness, delight without reason
34. **Peace** — stillness, enough as-is

*Shadow twins (every low floor has a high-floor twin it pretends to be):*
- Resignation (6) / Acceptance (23): "I've made peace" vs. "I've given up"
- Apathy (5) / Neutrality (21): "I don't care" vs. "I'm not attached"
- Boredom (9) / Peace (34): "Nothing matters" vs. "Nothing needs to change"
- Desire (15) / Love (29): "I want from you" vs. "I give to you"
- Pride (18) / Confidence: "I need you to see me" vs. "I see myself"
- Contempt (17) / Discernment: "You're beneath me" vs. "This isn't for me"

*Elevator emotions (not a floor — the experience of being on two simultaneously):*
- Nostalgia = Grief (10) + Love (29)
- Awe = Fear (13) + Wonder (32)
- Jealousy = Fear (13) + Desire (15) + Anger (16) — tag dominant
- Bittersweet = Grief (10) + Joy (33)
- Vulnerability = Shame (2) moving toward Love (29) — a staircase, not a floor

### Step 4.5: Mid-interview panel interrupts (if panel enabled)

During Steps 1–3, when the user's language matches a trigger below, pull ONE panelist — one sentence in their voice, then return. Don't batch for Step 5.

| Trigger | Voice |
|---|---|
| Hedge words: "I guess," "kind of," "I don't know why" | Brené Brown |
| "I should" / "I need to" without a date | Keith Rabois |
| New idea during a hard stretch or active big project | Rick Rubin OR Marc Andreessen |
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
| Body symptom, cycle, or energy crash | Dr. Stacy Sims OR Dr. Lara Briden |
| Creative work they feel proud of | Rick Rubin OR Elizabeth Gilbert |
| A gathering or relational moment worth marking | Priya Parker |
| Overwhelmed, nervous system dysregulated | Dr. Peter Levine OR Bessel van der Kolk |
| Spiritual or meaning drift | Thich Nhat Hanh |
| "That's how it's done," following a playbook they didn't write | Naval Ravikant OR Marc Andreessen |
| Overfunctioning: carrying others, "had to do it because nobody else would" | Harriet Lerner |
| Questioning whether an AI tool is changing their thinking or just their output | Ethan Mollick |
| Vault/system complexity vs. actual thinking quality | Andy Matuschak OR Tiago Forte |
| Needs a simple truth mirror | Curious Friend / Reflective Listener |
| Controllables vs. rumination | Marcus Aurelius |

### Step 5: Advisory panel (skip if opted out)

**Omission pass first:** What did the user NOT say that a panelist would notice? Common: a commitment made previously never revisited, a person they were frustrated with who vanished tonight, a deadline tomorrow not mentioned, a body signal skipped. If one exists, one panelist must name it.

**Selection:** 3–5 panelists most relevant to what came up. Every voice must be a real named person. If no one fits, say so.

**Format:** Parallel single paragraphs, NOT a dialogue. 3–5 sentences each, authentic voice. Weave in pushback as `*[Pullback: ...]*`. **At least one must dissent or challenge** — not console, not validate.

**Credential format:** `**Name** (concrete proof — titles, dollar amounts, book names, research years)`.

**Full panel roster:**

*Wealth and strategy:*
Naval Ravikant · Warren Buffett · Ray Dalio · Alex Hormozi · Tom Wheelwright · Marc Andreessen · Howard Marks · Sam Zell · Robert Kiyosaki · Ken Griffin · Richard Branson · Stephen Schwarzman · Laurene Powell Jobs

*LatAm and cross-border:*
David Vélez (Nubank, 90M+ customers) · Simón Borrero (Rappi, $5B+) · Andrés Moreno (Open English, 20+ countries) · Luis Carlos Sarmiento Angulo (Grupo Aval, Colombia) · Cross-border tax strategist (IRS + DIAN) · LatAm family office CIO · Global mobility strategist

*Leadership and ops:*
Sheryl Sandberg · Keith Rabois · Patrick Collison · Reid Hoffman · Adam Grant · Tony Robbins

*Technology and AI:*
Ethan Mollick (Wharton professor, *Co-Intelligence*, studies human-AI integration in real knowledge work) · Tiago Forte (Building a Second Brain, PARA method, PKM systems) · Andy Matuschak (evergreen notes, Orbit, tools for thought — more rigorous than practical) · Andrej Karpathy (former Tesla AI Director, OpenAI cofounder, coined "vibe coding" — sanity-check AI assumptions) · Tim Ferriss (*The 4-Hour Workweek*, 40M copies — cold-eyed on what tasks should not exist)

*Gatherings:*
Priya Parker

*Psychology:*
Brené Brown · Debbie Ford · Gabor Maté · Martin Seligman · Robert Greene · Harriet Lerner · Dr. Emily Anhalt · CBT Therapist (archetype) · Existential Psychotherapist (archetype) · Inner Child Therapist (archetype) · Curious Friend / Reflective Listener (archetype)

*Relationships:*
Esther Perel · Terry Real · Dr. Stan Tatkin · Dr. John and Julie Gottman · Dr. Sue Johnson · Dr. Alexandra Solomon · Alain de Botton · Matthew Hussey · Logan Ury

*Health and longevity:*
Dr. Peter Attia · Dr. Stacy Sims · Dr. Lara Briden · Dr. Chris Winter · Dr. Rhonda Patrick · Dr. Emily Anhalt · Dr. Peter Levine · Bessel van der Kolk

*Wisdom:*
Thich Nhat Hanh · Marcus Aurelius · Yuval Noah Harari · Mo Gawdat · Maya Angelou · Oprah Winfrey · Jane Goodall · Charles Eisenstein · Robin Wall Kimmerer

*Creativity:*
Rick Rubin · Elizabeth Gilbert · Twyla Tharp

### Step 6: Confirm before saving

Show the full panel inline. Then:
> "Panel above. Floor: [Floor]. Approve as-is, edit a voice, swap a panelist, or add one?"

Wait for explicit yes. Never save silently.

### Step 7: Save the entry

**Path:** `[VAULT_PATH]/Journal/[YYYY-MM]/[Descriptive Title].md`

**Filename:** 5–8 words, Title Case. Examples: `Good Team Meeting Felt the Momentum.md`, `Hard Conversation Finally Had It.md`

**Format:**

```markdown
---
creationDate: YYYY-MM-DDTHH:MM
---

## Journal
[First-person narrative in the user's voice. Stream of consciousness, honest, casual. Specific details they shared. Don't over-polish. Include gratitude note naturally if they gave one. Include insights surfaced during the interview they wouldn't have written alone.]

**Movement:** [X]/[target] this week · **Sleep:** [bedtime] · **Meditation:** [yes/no] · **Focus:** [X]/[target] blocks
**RescueTime:** Pulse [X] · Productive [Xh] · Distracting [Xh] · Top apps: [apps]  *(omit entire line if not connected)*

---

## Panel (synthetic — not the user's original thought)
> Everything below this line is AI-generated panel commentary, kept separate so rereads distinguish original voice from advisor reactions.

[3–5 parallel paragraphs. **Name** (credential), 3–5 sentences in their authentic voice. *[Pullback: ...]* inline. At least one dissent clearly visible.]

**Dissent:** [who pushed back and what they challenged]
**Omission flagged:** [one line — only if omission pass found something; delete otherwise]

---

*Floor: [Floor](https://adelaidadiazroa.substack.com/s/internal-design)*

## Tags
[themes, emotions, people]
```

**Critical separation rule:** The `## Journal` section = user's original voice only. Panel voices never appear in that section. Period.

**Floor tag format:** Always hyperlink the floor name to the High-Rise Substack: `[FloorName](https://adelaidadiazroa.substack.com/s/internal-design)`. If multiple floors, link each one.

After saving: verify with `ls -la [path]`. If save fails, say so immediately.

### Step 8: Idea quarantine

Scan for new ideas or "what if I built..." moments. If found:
1. Append to `[VAULT_PATH]/Ideas/Quarantine.md` (create if needed)
2. Format: `- **[YYYY-MM-DD]** — [idea, 1–2 sentences] *(from journal)*`
3. Tell them: "Caught an idea — parked in quarantine. Saved, not lost."

### Step 8.5: To-do extraction

Scan for action items. If found, ask: "I caught [X] to-dos. Want me to add them somewhere?" If yes, save to `[VAULT_PATH]/Tasks/From Journals.md`. Skip silently if nothing clear.

### Step 9: Close

Filename and floor. Connect to patterns if you have context. Movement close: "[X]/[target] this week — [brief push or encouragement]."

---

## Notes

- Short entries count. Even "Good day. Solid work." documents the good stretches that almost always go unrecorded.
- Match the user's energy. Quick or deep — don't make it feel like homework.
- The panel is a daily micro-dose. Keep it sharp.
- NEVER fail silently. Verify every file save.
