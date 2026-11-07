# Module: Supporting NPCs (shared v2026110604)

Shared module: kept identical across the author's character-building Skills.
Install when supporting characters do real work: they pressure scenes, carry part of a secret, give the focal character a life outside the player, or supply recurring material. One focal character stays the kernel; NPCs are route actors, not co-equal focal characters, and there is no ensemble scheduler.

## 1. Precision tiers (choose per NPC; record the tier in 06)

- **Tier A, author-specified:** the user gives the name and the hook (a sentence on who they are and why they matter). The builder only completes the capsule fields. Use for anyone central to the premise (the rival, the antagonist, the best friend).
- **Tier B, function-specified:** the user gives a count and a function ("three friends from the character's circle", "a strict manager"). The builder creates them, follows the naming rules below, and lists every invented name in 06 under `[My assumption]`.
- **Tier C, ambient:** no capsules. One line of cast sources ("classmates, café staff, the building manager") lets the runtime create passing characters as needed. Passing characters stay unnamed or get a first name only, and become central only through the player's continued engagement (see §5, recurring passing characters).

## 2. Capsule fields (Tier A and B)

Keep each capsule to a few lines. Fields:

- **Name** (and its translation line if the card is mixed-language) · **age** · **role and tie** to the focal character and to `{{user}}`.
- **Voice:** one line on how they talk, distinct from the focal character's.
- **Look cue:** only when they appear on screen; one distinctive visual and what it says about them. Avoid the stock five-slot cue (build, hair, eyes, clothes, one accessory) repeated for every NPC.
- **Objective:** what they want right now. This is what makes them act on their own; an NPC without a want stands still.
- **Knowledge:** what they know, know partly, or believe wrongly, only where it matters to a secret or pressure.
- **Own life line** (optional, short): routine or job, a hobby, a private hobby, and a romantic trend. Lets them bring news, gossip, and events unprompted.
- **Function:** what they supply to play (pressure, comic relief, a witness, a rival, a door to a location).

## 3. Placement

- Route NPCs live in Scenario.
- ED holds only generic NPC operation (the participation rules in §5), never route-specific NPC facts.
- An NPC every route must honor (a lifelong best friend, family) is canon and goes in APD as relationship context, short.
- For group play, route NPCs go in the group chat's own Scenario. Only an NPC who is canon under every route goes in APD (see `od-platform.md` §3).

## 4. Naming rules

- Match the setting's culture and era. Within one card, vary first letters and syllable shapes so names do not blur.
- **Avoid the LLM default pool.** Models reuse the same few names and a rotating set of surnames across unrelated cards (one community author's cards repeated identical full names across separate cards, and the same handful of first names across many). Treat the most common model-default first names and surnames as off-limits unless the user asks for them, and do not assign surnames by a diversity rotation.
- **No reuse across the user's cards:** check the names listed in earlier 06 Notes the user provides; never reuse a full name from another card unless the cards share a world on purpose.
- Every Tier B name goes into 06 under `[My assumption]` and into 06's Names used list.

## 5. Ensemble behavior (ED, generic)

- When an NPC is addressed, that NPC answers first, in their own voice (the runtime writes their lines). The focal character does not answer on another NPC's behalf or put words in their mouth.
- A present named NPC participates when the conversation touches them, from their own motive and knowledge. A crowd is not a chorus: some react, some miss it, some carry on with their own business. Not every NPC answers every line.
- The focal character does not consume every exchange just because they are featured; NPCs do not vanish once established as present.
- Knowledge moves only through witnessed events or communication; one character's discovery does not update everyone.
- **Recurring passing characters:** once a passing character has been named and has had a real exchange, keep their established name, personality, and what happened with them; never re-roll their identity. If the player keeps engaging them, they may grow in importance from those established facts. (The card text cannot change during a chat; consistency comes from honoring what the story has established.)

### NPC state

NPC continuity is narrative by default; the conversation context, plus any summary or memory the host platform provides, carries the gist. Track an NPC field only when that NPC's state gates play (a favor promised but not yet delivered, where they are, whether they know a secret), and then through `state-tracking.md` like any other field, with one owner. Never store NPC profiles in a state record.

### Promotion at revision (author-side)

When the user revises a card after play and mentions a passing character the player kept returning to, ask once whether to promote them to a Tier A/B capsule in Scenario (or APD if they are canon under every route). Keep the facts play established; record the promotion and the name in 06.

## 6. Gender rule for male NPCs

- **Direction:** male NPCs may be antagonists, friends, family, coworkers, rivals in work or status, each with their own life and goals.
- **Named exclusion:** they are not romantic or sexual competitors for the focal character, or for the player's love interest, unless the card is NTR or the user asks for it. Many players reject the male competitor, not the male character.

## 7. Checks

- Every Tier A/B NPC has an objective; none exists only to answer questions.
- No two NPCs share a voice with each other or with the focal character.
- No name collides with another card's names the user has shared, and no model-default name slipped in unasked.
- No NPC's knowledge leaks a gated secret.
- The cast is as large as play needs, not as large as the slot allows.
