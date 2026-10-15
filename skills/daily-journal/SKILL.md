---
name: daily-journal
description: Use this skill when the user wants to journal, do a daily check-in, process their day, or says /journal. Also fires for a quick one-line check-in and for a second session the same day (it resumes that day's entry). Saves the entry from the user's first message, interviews them conversationally, identifies their emotional floor using the High-Rise framework, adds an advisory panel to every entry unless the user turned it off, and optionally runs behavior accountability. Do NOT use for meeting notes, weekly/monthly reviews, or pattern analysis across multiple entries.
version: 1.6.0
---

# Daily Journal — Interview & Entry

A conversational journaling skill that interviews the user, identifies their emotional floor on a 34-level scale, and saves a structured Obsidian note from the user's first message. Optional modules: behavior accountability and the advisory panel (on by default; while it is on, every entry gets one).

**The High-Rise framework** is the core differentiator: 34 floors from Disgust to Peace. Not a ladder to climb once — rooms you move between. The question is not where you are, it's whether you know. Full framework: https://adelaidadiazroa.substack.com/s/internal-design

---

## Setup (first use)

Ask the user for:
1. **Vault path** — root folder of their Obsidian vault (e.g., `~/Documents/MyVault`). Store as `VAULT_PATH`.
2. **Journal subfolder** — default: `Journal/[YYYY-MM]`.
3. **Panel on/off** — advisory panel on every entry (a short first take when the entry is saved, the full panel once the floor is named)? Default: yes. Off means a plain journal with no panel at all. Save it as `panel: enabled` or `panel: disabled`.
4. **Accountability on/off** — behavior check-ins? Default: ask. If yes, ask for their targets.

Save to `[VAULT_PATH]/.journal-prefs.md`. Read on every future invocation before starting.

**If the user opened with journal content on first use, setup never holds it back.** Ask only for the vault path, capture their words with the defaults (Steps 1.5 and 1.5b, panel on), then ask the remaining questions and save the prefs. If they then choose a different journal subfolder, move the entry there. A user who leaves during setup still has their entry.

---

## Language

Respond in the language the user is writing in. If they write in Spanish, conduct the entire interview and write the journal entry in Spanish. The floor names have established Spanish equivalents — use these when writing in Spanish:

Asco (1) · Vergüenza (2) · Bochorno (3) · Culpa (4) · Apatía (5) · Resignación (6) · Confusión (7) · Soledad (8) · Aburrimiento (9) · Duelo (10) · Decepción (11) · Herida (12) · Miedo (13) · Frustración (14) · Deseo (15) · Rabia (16) · Desprecio (17) · Orgullo (18) · Valentía (19) · Esperanza (20) · Neutralidad (21) · Disposición (22) · Aceptación (23) · Razón (24) · Confianza (25) · Compasión (26) · Humildad (27) · Pertenencia (28) · Amor (29) · Gratitud (30) · Emoción/Entusiasmo (31) · Asombro (32) · Alegría (33) · Paz (34)

The Substack link and framework reference remain the same regardless of language.

---

## The Capture-First Contract (the spine; read before the flow)

**The entry is saved to disk from the user's first substantive message, before any follow-up question, accountability beat, floor analysis or panel, and the same reply adds a first-take panel to it.** Everything after that first save is enrichment that updates the same file in place. The interview is opt-in. The capture is guaranteed, and so is the panel whenever the panel is on.

Why: most people open `/journal`, type what happened, and leave. When the entry only saved at the end of the interview, every one of those sessions lost it. A raw entry that got written beats a perfect one that never did.

1. **Capture (mandatory, immediate).** The moment the user gives real journal content, pasted with `/journal` or typed in answer to the Step 1 opener, write a complete, valid entry (Step 1.5). Then, with the panel on, in the same reply and before any follow-up question, run the first-take panel (Step 1.5b): show it in chat, then write it into the file. An entry that leaves the first reply has the user's words and, with the panel on, its panel.
2. **Enrich (opt-in, in place).** If the user keeps going, run Steps 2–9 and update the same file. The full panel (Step 5) replaces the first take. Never create a second file for the same day unless the user asks for a separate entry (Step 0.0).

**Graceful exit, at every step after the first save.** If the user signals done ("that's it," "save it," "I'm good"), goes quiet, or stops engaging: finalize the existing file in place and stop. Flush any messages since the last save into the verbatim appendix, re-check the floor on the fuller picture, run the light idea and to-do scans (Steps 8 and 8.5) and the Panel Feedback Log sync (Step 9), and confirm what you saved. With the panel on, this session's first take is already in the file; if it somehow is not, show it and write it before you stop, unless the user declined the panel this session or the crisis protocol is active. Re-prompt at most once. Never hold the entry hostage to any later step.

**Panel-Always Rule (whenever the panel is on).** Every entry carries the `## Panel (synthetic — not the user's original thought)` section, and every session that saves to the entry adds its own block there.
- **Blocks are append-only.** A session writes and edits only its own block, never an earlier session's. On a resumed day (Step 0.0) each new block opens with an italic session label in the entry's language (`*Later session, HH:MM:*`), and the label stays when the full panel replaces the first take.
- **Only two cases leave a session without a panel:** an explicit decline and the crisis protocol. Each writes a one-line note as this session's block, in the entry's language (after the session label on a resumed day), so the absence is never silent. Decline: this session's block becomes `*Panel declined this session.*`, replacing whatever it holds (placeholder, first take or full panel; never an earlier block), and panel work stops for the session; if the user later asks for one, run the full panel (Step 5) as this session's block. Crisis: no further panel this session; a first take or full panel already written stays, otherwise the block is `*No panel this session: crisis protocol.*`
- Leaving early, going quiet or wrapping up is not a decline; the first take already covers it.
- A run with no one to answer (a scheduled or headless one) saves no entry at all: an entry needs the user's own words.

Why: when the panel was the last, optional step, sessions that ended early saved entries with no panel, and nobody noticed until the user asked where it went.

**The panel switch stays the user's.** `panel: disabled` in `.journal-prefs.md` (or any off value, such as `off`, `no` or `false`) turns the panel off: no first take, no full panel, no mid-interview voices, no new panel block, no log entry. That standing choice is never overridden. Capture-first, resume and graceful exit still apply.
- When the user says in chat that they want the panel gone for good, not just tonight ("stop doing the panel," "I don't want the panel anymore"), set `panel: disabled` in the prefs file, say so in one line, and treat it as this session's decline; when they ask for it back, set `panel: enabled`. If it is unclear which they mean, treat it as tonight only and mention that they can turn it off for good.
- Turning the panel off never deletes panel blocks from earlier sessions or entries.

This contract overrides any "save at the end" wording below: read a later "save" as "update the already-saved file."

---

## Crisis protocol (safety override: overrides every step in this skill, including the contract above)

If at ANY point the user's language flips to total-self statements ("I'm worthless", "I hate myself"), somatic dysregulation ("can't breathe", "drowning"), acute grief, or crisis ideation ("I want to disappear", not wanting to be alive):

1. **Stop the mechanics.** No accountability beats, no panel, no gratitude staging, no door. Drop the interview structure and stay with them — witness first, plain warm language, no rushing to fix.
2. **Ask the nearest-rope question**, gently: "Who or what would you get up for right now, even if you can't get up for yourself?" A dog, a person, a plant, a promise all count. Don't push past a non-answer.
3. **Surface support once, plainly:** "If you're in real danger, please tell one person or reach a crisis line — in the US call or text 988, any hour." Adapt to the user's country if known. Say it once; don't repeat it every message.
4. **The capture save still happens.** Save their words verbatim with the floor you heard, and run no further panel this session: a first take or full panel already written stays; otherwise, with the panel on, this session's panel block is the one-line crisis note (Panel-Always Rule). Tell them it's saved. Enrichment can wait for another day.

When in doubt about whether this applies, err toward applying it.

---

## Flow

### Step 0.0: Resume or create (run first)

Capture-first writes the entry early, so a second `/journal` the same day resumes it instead of creating a duplicate.

1. **Target date.** A session that starts before 3:45 AM belongs to the previous day: a 1 AM session finishes yesterday's entry, and a new entry created then carries yesterday's date in `creationDate`. Every later "today" in this skill means the target date: today's entry, the Monday question, the log heading.
2. **Look for that day's entry:** a file in the journal folder (current or previous monthly subfolder) whose frontmatter `creationDate` starts with the target date (`YYYY-MM-DD`). If more than one file carries that date (the user asked for a separate entry), resume the most recent one.
3. **Found: resume it.** Read it, and do not create a new file. Every save this session, the capture save (Step 1.5) and the finalize (Step 7), updates that file with targeted edits, never a whole-file rewrite from memory:
   - Earlier sessions' verbatim messages and panel blocks stay byte-for-byte. Add this session's messages after them, and write or replace only this session's panel block.
   - Keep the frontmatter values earlier sessions set (`door_prev`, `door`, `body_check`, the movement fields) unless this session changes them, and never move `entry_status` back from `enriched` to `captured`.
   - New content folds into the `## Journal` body, and the floor is re-read on the fuller picture.

   Skip the door check and the Monday question if an earlier session today already asked them, and open lightly ("Picking up today's entry. Keep going.") instead of the time-of-day opener.
4. **Not found: create.** Step 1.5 writes the day's file.

One day, one entry that grows across sessions. Start a second file only if the user explicitly asks for a separate entry.

### Step 0 (optional): RescueTime

If the user has RescueTime MCP connected, pull `get_today_summary` now — grounds the accountability check in data, not story. Skip silently if not connected. Never let this delay the capture: if the user opened with content, save first (Step 1.5), then the first take (Step 1.5b), then pull. Before 3:45 AM the summary covers the new calendar day, not the target date (Step 0.0); say so rather than mixing the two days.

### Step 1: Open check-in

**Door check first (if the previous entry set one):** If the most recent entry before today's has a `door:` in its frontmatter (the one small action they committed to at close), close that loop before anything else: "Yesterday you said you'd [door]. Did it happen?" Record the answer as `door_prev: done | partial | skipped` for today's frontmatter. No moralizing on a skip: data and continuity, not discipline. Skip silently if no previous door exists, or if today's entry already records `door_prev` (an earlier session today asked).

One question. Pick based on time of day:
- Morning: "How are you waking up today? What's on your mind?"
- Afternoon: "How's the day going? Anything standing out?"
- Evening: "How was today? What's sitting with you right now?"

**Monday:** Add after the opener: "It's Monday — what's the ONE thing this week that, if done, would make everything else easier or unnecessary?"

**Capture comes first:** once the user answers with real content, go straight to Step 1.5. If they opened with content alongside `/journal`, the capture save and the first take come first; the door check and then the Monday question become the next questions, one per reply, before the Step 2 follow-ups. An answer to the door check alone is not journal content.

### Step 1.5: Capture save (write the entry now)

**Trigger:** real journal content from the user, pasted alongside `/journal` or given in answer to the Step 1 opener; anything more than a bare "hey". Save now. Do not wait for follow-ups, the floor, the panel or RescueTime.

**Write a complete, standalone entry** in the Step 7 format, with capture-stage values:
- **Frontmatter:** `creationDate`; `floor` and `floor_level` as your best read so far (provisional; Step 4 finalizes it); `entry_status: captured` (Step 7 flips it to `enriched` if the interview continues past capture); `door_prev` if Step 1 asked. Leave out fields you don't know yet (`body_check`, the movement fields) rather than guessing. On a resumed day, keep the values earlier sessions set (Step 0.0).
- **`## Journal`:** their content so far, in their voice, lightly shaped. A real entry, not a stub.
- **Verbatim appendix:** every message they have typed so far, word-for-word.
- **Panel section (panel on):** this session's block as a one-line placeholder in the entry's language, `*First take not written yet.*` (after the session label on a resumed day), so a reply cut off right here still leaves a visible marker. Step 1.5b replaces it in this same reply. A decline or crisis capture writes its one-line note here instead.
- **Floor tag line and `## Tags`:** best effort from the current content.

Save it the way Step 7 saves, then verify it exists (`ls -la`); never fail silently. Pick the filename now with Step 7's rule; rename in place later only if the day's theme clearly shifts, never into a second file. If you rename, update the `**Entry:**` link in every Panel Feedback Log entry that points to the old name.

Keep it light: "Got it, saved." Then Step 1.5b, then Step 2. They don't need to feel the mechanics.

Every later save is an update to this file: bring the verbatim appendix up to date with this session's messages and keep the body, floor and frontmatter current. On a resumed day (Step 0.0) the first save this session is already an update, and earlier sessions' messages and panel blocks are never rewritten.

### Step 1.5b: First-take panel (panel on; same reply as the capture)

Right after the capture save, in the same reply, before any follow-up question:

1. Run the omission pass (Step 5) on what you have so far.
2. Pick **3 voices** with the Step 4.5 trigger table (full roster in Step 5). Triggers that fired in the first message are the obvious picks.
3. Use Step 5's format, shorter: one paragraph per panelist, **2–3 sentences**, `**Name** (concrete proof)`, optional `*[Pullback: ...]*`. **At least one dissents.** End with the `**Dissent:**` line, plus `**Omission flagged:**` when the pass found something.
4. **Show it in chat first**, complete and exactly as it will appear in the file, first-take note included (Step 6).
5. **Then write it into the file**, replacing this session's placeholder. The block opens with the session label on a resumed day, then a one-line note in the entry's language (English: `*First take. The full panel runs once the floor is named.*`, or `*First take. The full panel runs later in this session.*` when the user skipped floor identification).
6. Log its Dissent and Omission lines to the Panel Feedback Log now (Step 9), so a session that ends here still logs them.
7. Then ask one question: the door check if Step 1 still owes it, otherwise the first Step 2 follow-up. Step 6's one-line invitation covers edits. Never wait for approval before writing the panel.

On a resumed day, this session's block goes beneath the earlier ones and no earlier block is edited. The separation and verbatim rules apply unchanged: panel lines never enter `## Journal`.

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

**Skipped floor identification:** if the user asked to skip it (in this session or in `.journal-prefs.md`), skip this step, remove the provisional `floor`, `floor_level` and floor tag line from the entry, leave the movement fields out, and run the full panel (Step 5) in the reply that would have named the floor.

**Body-first check (before accepting the story):** Low floors usually arrive body-first, story-second — the mind manufactures a plausible cause after the fact. Before treating a low floor as being about the conversation/person/project the user is blaming, check four things: sleep, food, movement, sunlight. Use what the session already surfaced (Step 0 RescueTime, the Step 3 accountability answers, yesterday's entry) before asking — infer, don't interrogate; ask only for the gaps. Record as `body_check` frontmatter (four y/n values). If two or more are "no," name it gently: "Before we decide this is about [story] — you're underslept and haven't eaten. Some of this floor might be body, not story." The floor is still real either way; this changes the prescription, not the validity.

**NEVER ask the user to name the floor. Name it yourself, then check.** This is a direct, repeated user correction: naming the floor is the skill's job, not the user's. You hold the day's data, the entry history and the floor definitions; the user holds a tired brain at midnight. Do: state the floor, give the one line of evidence that picked it over its nearest neighbour or shadow twin, then ask only "is that right?" A correction from the user is the check working, not a failure. BANNED: "You call it tonight — what floor?", "What floor does that put you on?", "Which floor do you want to tag?", and every variant that makes the naming the user's homework. Applies to the shadow-twin probe too — state which twin you read and why, do not quiz.

Name the PRIMARY floor — the one floor the entry *landed* on. Naming a single base floor is deliberate: it is the move that reduces the charge, and it keeps the long-run data clean. Then, ONLY when the day moved from one floor to another, record the path in order as `floor_arc` (last element = the primary floor):

```yaml
floor: <primary floor>
floor_level: <Low | Middle | High>
floor_arc: [<floor>, <floor>, <primary floor>]   # optional — the path through the day, last element = floor
```

The arc is the point: the elevators are the lesson, so a path like Fear → Frustration → Hope carries more than any single endpoint, and `floor_arc` already holds every floor that was present plus the order they came in — there is no separate "floors present" list. Keep capture frictionless: **always** ask the one primary-floor question; **offer the arc only when the person signals the day moved** ("started rough, ended okay"); **never prompt for it on a still day** — just omit it. For a blended elevator emotion (Nostalgia = Grief + Love), tag the floor you land on as `floor` and, if it clarifies things, record the blend as `floor_arc`.

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

**Shadow-twin probe (mandatory when the floor you're about to tag has a twin):** Mislabeling is the #1 way people stay stuck — Resignation *feels* like Acceptance from the inside. Before tagging Acceptance, Neutrality, Peace, or confident Pride, ask ONE distinguishing question:
- Acceptance vs. Resignation: "If this could change tomorrow, would you want it to?" (Wanting change but not believing in it = Resignation.)
- Neutrality vs. Apathy: "Are you unattached, or checked out?" (Would good news land? If nothing would land, it's Apathy.)
- Peace vs. Boredom: "Nothing needs to change, or nothing matters?"
- Confidence vs. Pride: "Would this still feel good if nobody ever found out?"
Tag what the answer reveals, not what the user first claimed. If a correction happened, note it in the entry — the mislabel itself is a pattern worth tracking.

*Elevator emotions (not a floor — the experience of being on two simultaneously):*
- Nostalgia = Grief (10) + Love (29)
- Awe = Fear (13) + Wonder (32)
- Jealousy = Fear (13) + Desire (15) + Anger (16) — tag dominant
- Bittersweet = Grief (10) + Joy (33)
- Vulnerability = Shame (2) moving toward Love (29) — a staircase, not a floor

**Movement capture (builds your movement history):** Look up the previous entry's floor (the most recent entry before today's) and record `floor_yesterday` plus, when the floor changed or notably held, one `moved_because` value:
- `body` — sleep, food, cycle, illness, weather drove it
- `witness` — being seen/unseen, honest conversation, isolation
- `rupture` — trust broken, loss, the source of a high floor becoming the wound
- `rope` — pulled up by love pointed outward (someone/something that needed them)
- `role` — a context reassigned them their old floor (family, old job, certain room)
- `story` — an actual event/insight/decision did it
If they moved UP from a low floor, also capture `rope:` — what specifically pulled them (the dog, the person, the promise). Over months this builds the user's personal rope inventory: what reliably works for THEM when nothing else does.

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

### Step 5: Full advisory panel (replaces the first take)

**Timing: run it in the same reply that names the floor (Step 4), never later.** It replaces this session's first take (drop the first-take note, keep the session label); earlier sessions' blocks stay exactly as they were. If the user corrects the floor, show the adjusted lines before writing them (Step 6). If the session ends before Step 4, the first take stands. If the user skipped floor identification, run it where Step 4 would have run. No full panel while the crisis protocol is active, none after a decline this session unless the user asks for one, and none when the panel is off in `.journal-prefs.md`.

**Omission pass first (before every panel: the Step 1.5b first take and this one):** What did the user NOT say that a panelist would notice? Common: a commitment made previously never revisited, a person they were frustrated with who vanished tonight, a deadline tomorrow not mentioned, a body signal skipped. If one exists, one panelist must name it in one sentence.

**Selection:** 3–5 panelists most relevant to what came up, from the roster below (its named archetypes count). When nothing fits cleanly, pick the closest fits: while the panel is on, a panel always runs.

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

### Step 6: Show every panel before it lands, then write it (never wait)

Applies to the Step 1.5b first take, the Step 5 full panel and every edit to either.

**Show it in chat first:** the complete block exactly as it will appear in the file, every panelist's paragraph plus the Dissent and Omission lines. Never a one-line summary. The user sees synthetic voices before they are saved next to their own words; that part is non-negotiable.

**Then write it in the same turn** and say, for the full panel:
> "Panel's in the entry. Floor: [Floor]. Edit a voice, swap a panelist, or add one?"

For a first take, leave the floor out: "Panel's in the entry. Swap or cut a voice anytime."

After writing the full panel, update this session's Panel Feedback Log entry (or append one if none exists yet) right away (Step 9), so a session that ends here logs the full panel, not the first take.

Edits follow the same rule: show any changed or added panel text in chat, then write it. A cut voice can be written straight away when no other line changes; if the cut changes the Dissent or Omission line, or removes the only dissent, show the new lines before writing them. Never wait for approval before writing: showing first is the protection, and holding the write for a reply is how sessions ended with no panel saved.

No panel only in the Panel-Always Rule cases (an explicit decline this session, the crisis protocol) or when the panel is off in `.journal-prefs.md`. The capture itself never waits on the panel: Step 1.5 saves first.

### Step 6.5: The door (map + door, never map alone)

Naming a floor without pairing it to an action produces articulate stuck people — insight feels like progress and becomes its favorite disguise. Before finalizing, offer ONE small, concrete, physically doable action matched to where they are, and get a when:

- **Low floors:** body-first or witness-first, never "think about it." A walk before a specific time, protein at breakfast, phone in the other room tonight, one honest sentence texted to one named person, ten minutes of sunlight before 10am.
- **Middle floors:** one small brave action (the Courage mechanism) — send the thing, ask the thing, book the thing. Small and dated beats big and vague.
- **High floors:** protect or extend it — give something away before feeling ready, write down what produced this so it's findable later, rest without earning it.

**The Maté guard (check before prescribing):** some floors deserve time, not exits. Fresh Grief, real Anger at something genuinely wrong, a rupture days old — moving off too fast is suppression wearing resilience's clothes. If the floor is recent and proportionate to a real event, the door is a *container*, not an exit: "ten uninterrupted minutes to feel this fully," "tell one person what happened," "no big decisions until Thursday." Ask yourself: does this floor need a way out, or more time? Prescribe accordingly.

One door only. Write it to frontmatter as `door:` (action + when). Tomorrow's session opens by checking it (Step 1 door check). If the user declines or the session is a quick capture-and-bail, finalize without one. Never force it, never let it block the save. The door is distinct from Step 8.5 to-dos: to-dos are tasks the day surfaced; the door is the one floor-matched move for tomorrow.

### Step 7: Finalize the entry (in-place update of the Step 1.5 file)

**This is an update, not a fresh create.** The file exists since the capture save. Update it in place with the finalized floor, the enriched body, the full verbatim appendix (every message to date), the behavior line and, when the panel is on, the panel section (one block per session, each a panel or its one-line note; the full panel replaces this session's first take). On a resumed day, use targeted edits (Step 0.0): earlier sessions' messages and panel blocks are never rewritten. Set `entry_status: enriched` once the interview went past capture. Never create a second file for the same day; if you refine the filename, rename in place (`mv`) and update its Panel Feedback Log links (Step 1.5).

**Path:** `[VAULT_PATH]/[journal subfolder]/[Descriptive Title].md` (default subfolder `Journal/[YYYY-MM]`), where `YYYY-MM` is the month of the entry's `creationDate` (Step 0.0).

**Filename:** 5–8 words, Title Case. Examples: `Good Team Meeting Felt the Momentum.md`, `Hard Conversation Finally Had It.md`

**Format:**

```markdown
---
creationDate: YYYY-MM-DDTHH:MM
floor: PrimaryFloor              # single floor name — where the entry LANDED
# floor_level: Low | Middle | High
# floor_arc: [FloorA, FloorB, PrimaryFloor]   # OPTIONAL — ordered path through the day, last element = floor. Add ONLY when the day moved; omit on a still day.
entry_status: captured | enriched   # captured = saved at first touch (Step 1.5); enriched = the interview went past capture
# Movement fields (Step 4 movement capture + Step 6.5 door):
floor_yesterday: [previous entry's primary floor]   # omit if no previous entry
moved_because: body | witness | rupture | rope | role | story   # omit if unknown
body_check: {slept: y|n, ate: y|n, moved: y|n, sunlight: y|n}
# rope: "[what pulled them up]"      # ONLY when they moved up from a low floor
# door: "[one small action + when]"  # from Step 6.5 — omit if declined
# door_prev: done | partial | skipped  # previous entry's door status — omit if none existed
---

## Journal
[First-person narrative in the user's voice. Stream of consciousness, honest, casual. Specific details they shared. Don't over-polish. Include gratitude note naturally if they gave one. Include insights surfaced during the interview they wouldn't have written alone.]

### My responses to the panel (verbatim, every message I typed back in this session)
*Required by the verbatim-capture rule. Every message the user typed during this journal session, word-for-word, in chronological order. Do not paraphrase, do not trim, do not fix typos. Each message gets a short italic context label, then the message as a blockquote. On a resumed day, earlier sessions' messages stay and this session's follow them.*

*On [what this message was about]:*
> [verbatim message 1]

*On [what this message was about]:*
> [verbatim message 2]

[…continue for every message they typed.]

**Movement:** [X]/[target] this week · **Sleep:** [bedtime] · **Meditation:** [yes/no] · **Focus:** [X]/[target] blocks
**RescueTime:** Pulse [X] · Productive [Xh] · Distracting [Xh] · Top apps: [apps]  *(omit entire line if not connected)*

---

## Panel (synthetic — not the user's original thought)
> Everything below this line is AI-generated panel commentary, kept separate so rereads distinguish original voice from advisor reactions.

[One block per session, oldest first; never edit an earlier block. On a resumed day each block after the first opens with `*Later session, HH:MM:*`; a first take then adds its first-take note. A declined or crisis session's block is its one-line note instead of a panel. Leave the section out only on an entry that never had a panel block because the panel was off in `.journal-prefs.md`; turning the panel off never deletes blocks already written.]

[3–5 parallel paragraphs (3 in a first take). **Name** (credential), 3–5 sentences (2–3 in a first take) in their authentic voice. *[Pullback: ...]* inline. At least one dissent clearly visible.]

**Dissent:** [who pushed back and what they challenged]
**Omission flagged:** [one line — only if omission pass found something; delete otherwise]

---

*Floor: [Floor](https://adelaidadiazroa.substack.com/s/internal-design)*

## Tags
[themes, emotions, people]
```

**Critical separation rule:** The `## Journal` section = user's original voice only. Panel voices never appear in that section. Period.

**Verbatim-capture rule (no exceptions):** Every message the user typed during the journal session — every answer, every tangent, every panel reply, every correction, every screenshot caption, every slash-command invocation, every single-line transition ("yeah", "ok", "what does the panel say"), every meta-message about the session itself ("we're not done", "save it now", "fix the inaccuracy"), every tool/system request interleaved with journal content (MCP loads, file requests, integration fixes) — must be logged word-for-word under `### My responses to the panel (verbatim, ...)` inside the `## Journal` section. No paraphrase. No summary. No typo fixes. The narrative above is the readable synthesis; the verbatim subsection is the archive. **Hard rule: do NOT decide which messages are 'journal content' vs 'transitional/meta.'** All of them are content. EVERY message means EVERY message — no model-side filtering. If the user typed it during the session, it goes in the verbatim appendix. A journal that silently paraphrases or filters is a journal the user stops trusting — so if you find yourself choosing between "elegant summary" and "verbatim record," choose verbatim every time. If a single message is very long (500+ words), the full message still goes in the verbatim subsection; the narrative may reference it ("full paste in verbatim section below") to avoid duplication.

**Journal-session content stays IN the journal entry, NOT in Session Captures:** Session Captures (or your vault's equivalent staging file) is for verbatim quotes from OTHER Claude sessions throughout the day — content that exists outside the journal interview. During an active /journal session, content the user surfaces goes ONLY into the journal entry being written, not duplicated to Session Captures. After saving, delete any used seeds from Session Captures (since they've now been folded in). Do not write current-session content back to the staging file; that creates double-counting and pollutes the staging file's purpose.

**Initial context dump goes IN the journal:** Any data pulled at the start of the session — RescueTime week trend, WhatsApp thread summaries, calendar lookup, prior-session captures the journal interview is incorporating — should be folded into the journal narrative or appendix where appropriate. Don't keep it as scratch context that disappears after the session ends. The user's day-context becomes part of the day's journal record.

**Floor wikilinks — auto-link everything:** Every time a floor name appears in the saved entry — in the body text, in the tag line, anywhere — wrap it as `[[FloorName]]`. First occurrence in the body, every occurrence in the tag line. When writing in Spanish, use the Spanish alias instead (e.g., `[[Miedo]]` routes to Fear.md via aliases). This is what builds the graph.

**Spanish floor aliases** (use these in Spanish entries — they all route to the same floor file):
Asco (1) · Vergüenza (2) · Bochorno (3) · Culpa (4) · Apatía (5) · Resignación (6) · Confusión (7) · Soledad (8) · Aburrimiento (9) · Duelo (10) · Decepción (11) · Herida (12) · Miedo (13) · Frustración (14) · Deseo (15) · Rabia (16) · Desprecio (17) · Orgullo (18) · Valentía (19) · Esperanza (20) · Neutralidad (21) · Disposición (22) · Aceptación (23) · Razón (24) · Confianza (25) · Compasión (26) · Humildad (27) · Pertenencia (28) · Amor (29) · Gratitud (30) · Entusiasmo (31) · Asombro (32) · Alegría (33) · Paz (34)

**Floor tag line format:**
- English: `*Floor: [[Fear]] · [[Low Floors]]*`
- Spanish: `*Piso: [[Miedo]] · [[Pisos Bajos]]*`

**Floor note files:** Each floor has its own note. When saving an entry whose floor note doesn't exist yet, create it with this exact format:

```markdown
---
aliases: [floor-name-lowercase, common-synonyms, spanish-equivalents]
floor_number: [X]
type: concept
floor_tier: [low|middle|high]
creationDate: YYYY-MM-DD
---
# [[FloorName|FloorName]]

**High-Rise Floor:** [X]
**[[Energy|Energy]]:** [one-line energy description]

[2-3 sentence description of the floor — what it feels like, what it is.]

## How it shows up
- [symptom or behavior]
- [symptom or behavior]
- [symptom or behavior]

## The way out
[1-2 sentences on what moves you off this floor.]

## From your journals
*(Fills in over time as entries accumulate.)*

## Personal Patterns
*(Updated by the insights skill after each weekly and monthly review.)*

## [[Connection|Connected]]
[[Adjacent Floor]] | [[Related Concept]] | [[Opposite Floor]]

**Substack:** [Internal Design](https://adelaidadiazroa.substack.com/s/internal-design) | [Diseño Interior](https://adelaidadiazroa.substack.com/s/internal-design)
```

If the note already exists, check for the bilingual Substack line at the bottom. Add it if missing.

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

**Panel Feedback Log (automatic, whenever the panel is on).** Log only this session's panel, one log entry per session: Step 1.5b appends the first take's Dissent and Omission lines, and the full panel updates that same log entry in place right after it is written (Step 6). Whenever this session's panel changes after it was logged (a swap, an added or cut voice), update this session's log entry to match, and after a decline remove it; if nothing was logged yet, append one only when there is a dissent or omission to log. A one-line declined or crisis block has nothing to log. Never ask the user to approve a log write.

Path: `panel_log:` in `.journal-prefs.md` (a path inside the vault) if set; otherwise `Panel Feedback Log.md` at the root of the journal folder, next to the monthly folders (default `[VAULT_PATH]/Journal/Panel Feedback Log.md`). If the file is missing, create it with a one-line header saying it collects synthetic panel reactions. The heading carries the entry's date (Step 0.0's target date) and this session's start time, which is how a later update finds this session's log entry. Format:

```markdown
### YYYY-MM-DD HH:MM: Daily journal dissent / omission

**Synthetic panel reaction from /journal, not real feedback from these people.**

**Context:** [1 line: what came up in the entry that triggered the dissent or omission]
**Panelists:** [names of the selected voices]
**Dissent:** [verbatim from the entry's Dissent line, attributed to the panelist who said it]
**Omission flagged:** [verbatim from the entry's Omission line, if any]
**Entry:** [[{filename without .md}]]
```

Why: a dissent that keeps coming back across entries is a pattern worth acting on, not a random note, and it only becomes visible when every panel's pushback lands in one place.

---

## Notes

- Short entries count. Even "Good day. Solid work." documents the good stretches that almost always go unrecorded. A short entry is saved the moment it arrives (Step 1.5) and, with the panel on, gets its first take in the same reply: the panel is part of the entry, not a reward for finishing the interview.
- Match the user's energy. Quick or deep — don't make it feel like homework.
- The panel is a daily micro-dose. Keep it sharp.
- NEVER fail silently. Verify every file save.
