# Module: OurDream State Adapter (shared v2026110706)

Shared module: kept identical across the author's character-building Skills.
Read this only when the target platform is OurDream (OD) and a tracker is installed. It implements the backends defined in `state-tracking.md` on OD. On other platforms, map the same backend semantics to that platform's own persistence mechanism instead.

Evidence labels in this file:
- **Verified:** confirmed by the Skill author's direct OD use or the supplied current UI.
- **Unverified:** plausible platform behavior that has not yet been directly tested; do not make load-bearing design depend on it.

## 1. Internal backend on OD: the hidden state block

- **Carrier:** ED makes every reply by this character end with one hidden state block. OD keeps HTML comments in fields and hides them in chat. A hidden state block and an image footer can coexist.
- **Namespace:** the block is labeled with the character's own name, so a character reads and updates only its own block. In a group chat the block is not private: it sits in the reply text, and the chat history is shared, so every other character can see it. Put nothing in it that another character must not know. Per-character state that should stay out of the shared history belongs in External (§2.5), though whether other cards can read External values is still unverified:

  ```
  <!-- [State: <Character Name>]
  Key: value
  Key: value
  -->
  ```

  One field per line; five or more compact fields may use one line (`Key:value|Key:value`). English/ASCII keys, always in the same order. **Do not put an instructional placeholder such as `<Scenario supplement...>` inside the literal block template.** If the current Scenario supplies an Internal supplement, append its actual fields after the fixed fields before the closing comment.
- **Read rule:** at the start of each reply, the latest block labeled with this character's own name is the current Internal state. Never read, update, or continue a block labeled with another name. Update only from what happened in the latest exchange, by the card's update rules, and write the new block at the end.
- **First appearance without a block:** when this character has no block of its own yet (for example, the card was added to an existing group chat and its Greeting was never read), start from the Internal defaults in ED, append the Internal supplement fields of any `[Scenario State: <Character Name>]` or `[Scenario State: all]` entry in the Scenario in use, and write the character's first block at the end of that reply.
- **Initialization in single chat:** the Greeting ends with the initial Internal block, so the first reply has a value to read and the format is demonstrated. The Greeting's block contains only Internal-owned fields: cross-route fields, Internal generic slots, and any Internal supplement fields of the card's own Scenario. External fields are not mirrored into it.
- **Carry forward:** every field in the character's previous Internal block appears in the next one; when unsure, keep the previous value.
- **Group chats:** every character in a group chat, the starter card or an added card, reads the Scenario in use (the starter card's own, or the group chat's own Scenario when one is set; verified with the Skill author's test cards). So an added card's generic slots and Internal supplement can bind to that shared Scenario, by the binding rule in `state-tracking.md` §5.
- **Visibility:** hidden by default; a visible status line only when the user wants one, and then only for Internal fields (OD forbids re-printing External state; see §2.1).

## 2. External backend on OD: 07 State (State Trackers panel)

07 is configuration the user enters by hand in the card's **State Trackers** panel (`Add New Field`). It is never pasted into APD, ED, Scenario, Intro, or Greeting. When delivering 07, say in one line that it is panel configuration, not a card text field.

Panel labels in this file follow the English UI. The user's panel may show them machine-translated, and wording changes between OD updates: match settings by position and function, use the user's wording when talking to them, and keep field names, values, and rules in the card's language.

### 2.1 Runtime pipeline and visibility

- **Verified:** OD's external state model runs **after the character reply** and updates the configured fields. Treat this as a post-response settlement phase, not as a pre-response gate engine. The current chat model still receives the user's message and visible conversation context directly, so it can react to a fresh explicit event even before the External field has settled to its next value. Use Internal when the card needs a newly computed tracker value itself before the reply is generated (`state-tracking.md` §2-4).
- **Verified:** after the external state is updated, OD exposes the current tracker state to the **chat model as `Internal state` context**. This is independent of HUD visibility. The chat model can therefore read External-owned values without maintaining them itself.
- **Verified:** OD's image generation also reads External tracker values; the built-in Outfit preset exists for exactly this. An External Outfit or similar field therefore shapes generated images as well as the chat model's context. When a card also writes an image footer that describes the same thing (clothing in a styling line, say), the two must agree. Which one dominates is unverified and depends on how OD assembles the image prompt and on format: a Danbooru-style tag footer probably outweighs a prose Outfit value on anime models, while two tag-format sources are an open question. Pick a primary source per card, keep the other consistent with it, and record the choice in 06. An External Text field can also be the tag source itself: its Update rules tell the tracker to write the value as Danbooru-style tags, in the same form a card's footer would use (reported to work by community creators; Max chars 400 is enough for a styling line). The built-in Outfit preset's prose wording is a beginner default and is weaker for image generation; customize the rule rather than keeping it.
- `Reader sees value` controls whether the field is shown in the player's chat HUD. It does **not** control whether the chat model receives the Internal state.
- `Reader can edit state` is panel-level and allows the reader to change visible HUD values.
- `{Field name}` is an **explicit text interpolation** syntax. Use the exact field name shown by the panel inside single curly braces when a specific instruction, status line, or other card text needs the current value inserted there. It is **not required merely for the chat model to know the tracker state**, because the current external state is already sent as Internal state context.
- External-owned fields are read-only from the chat model's side: the chat model may react to them, but never writes, mirrors, or re-derives them in its Internal block.
- **Verified injection wrapper** (observed identical on two cards, Nov 2026). Each reply, the speaking character's own tracker values arrive in this form, placed with the user's message:

  ```text
  <Character Name>'s current state — treat this as authoritative ground truth and stay consistent with it; you may reference it naturally in-character, but do not re-print it as a status block or HUD in your reply:
  - <Field>: <value>
  - <Field>: <value>
  ```

  Consequences for card text:
  - The platform already declares these values authoritative. ED does not repeat "trust the tracker"; it only says which fields are External so the chat model leaves them out of its own block.
  - Never instruct the character to print External values as a status line, stat block, or HUD: that fights the platform's own instruction and runs unreliably. A player-visible value is shown with `Reader sees value`. Values may surface naturally in the prose ("it's past eight already").
  - Fields with an empty value are still injected as empty lines, which invites the chat model to fill them in on its own; see the Start rule in §2.6.
- The same message also carries a platform reply-length line (for example `[Length check for your next reply: usually 30-40 sentences, but shorter when a quick beat serves the moment better; never pad.]`). A card's own length rule competes with it; see `od-platform.md` §2.
- **Testing:** a tracker's value is read from the HUD, never from the character's account of it. Characters asked about their state confidently describe values that are not there yet, and "writes" that never happened.

### 2.2 Per-field configuration

For every field output these settings in the same order the panel presents them:

1. **Name**
2. **Type**
3. **Type-specific settings**
4. **Update rules** — read by the state model only, up to 4,000 characters. Fill this even though the UI marks it optional. Use a concise plain-language rule plus hard positive and hard negative examples when ambiguity is plausible.
5. **Reads from** — `Both`, `User message`, or `Character reply`. This means **which side of the exchange is allowed to change the field**, not merely which text the tracker can inspect. A User-message-only field must not change solely because of the character reply, and vice versa.
6. **Resets every turn** — enable only for one-off fields. **Verified behavior:** the field returns to its Start value each turn unless the new exchange sets it again.
7. **Reader sees value** — on/off HUD visibility.

Type settings:

- **Yes/No:** `Start`. Best for latches.
- **Option:** `Options`; `Allow multiple`; `Start`. Best for discrete states and bands, named as states (`Wary`, `Settled`) rather than numbers. State how far one turn may move. With `Allow multiple`, use related flags such as clues found. Persistence is rule-driven: when selected options should remain active until a named removal event, say that explicitly in Update rules rather than assuming a universal platform rule.
- **Meter:** `Min`; `Max`; `Start`; `Meter Color`; `When it fills up` (`Stop at the top` or `Start over`). **Verified:** the minimum cannot be negative. Shift a signed conceptual scale so the stored meter begins at zero.
- **Number:** `Start`; optional `Max`; `When it fills up`. Best for counts and bounded numeric state.
- **Time:** `Start` (for example `12:00`). Best for an in-story clock.
- **Text:** `Start`; `Max chars`. The UI defaults to 100 characters. **Verified:** the maximum is 400. Best for compact descriptive state such as outfit or location.

Choose types the way `state-tracking.md` §1 chooses a representation: use the representation the gameplay actually needs, not the most impressive-looking widget.

### 2.3 Panel-level Tracking instructions

`Tracking instructions` are global rules for the **tracker AI only**; the chat model never reads them. Keep them short and state-engine-specific. Do not put character personality, dialogue style, anti-drift locks, relationship prose, or scene-writing instructions here.

A compact baseline when needed:

```text
For persistent fields, preserve the current value unless a field-specific rule or an established event changes it.
Use only evidence permitted by each field's Reads from setting and events established in the exchange; do not invent unobserved events.
When evidence is ambiguous, keep the current value.
Field-specific Update rules override these global defaults.
For fields with Resets every turn enabled, begin from Start each turn and set a new value only when that exchange triggers it.
```

Omit lines that the individual field configuration already makes unnecessary. The goal is consistency, not a second copy of every field rule.

### 2.4 Built-in OD Suggestions

The current OD UI offers convenience presets for **Outfit, Location, Mood, and Affection**. They are shortcuts, not mandatory fields and not SCB defaults. Use them only when their semantics fit the card; customize or ignore them freely.

- **Outfit** — `Text`; Start `casual clothes`; Max chars `100`. Built-in rule tracks each visible garment with its current state, removes garments when taken off, notes where removed items went, and updates when clothing changes. Good External candidate because it is descriptive, persistent, and easy to lose in long context.
- **Location** — `Text`; Start ships blank in the UI: replace it with the actual opening location before delivery (§2.6); Max chars `100`. Built-in rule asks for a specific place plus room/spot and updates on movement. Good External candidate when exact current location should persist or display.
- **Mood** — `Option`; options `content`, `happy`, `flirty`, `annoyed`, `sad`, `excited`; single-select by default; Start `content`. Built-in rule picks the closest current emotional label and changes only on a clear shift. Treat this as a **coarse convenience HUD**, not a replacement for nuanced cognition, mixed emotions, or private/public emotional asymmetry.
- **Affection** — `Meter` `0–100`; Start `20`; built-in rule rises with warmth, honesty, and shared moments, falls with rudeness or neglect, and limits movement to at most 5 points per message. Treat this as one **coarse relationship meter** only. Do not install it by habit on cards whose relationship logic separates trust, liking, attraction, disclosure, cooperation, rivalry, intimacy, or other dimensions.

The Suggestions prove that External is not limited to numbers: OD itself uses Text, Option, and Meter presets. Backend choice is about the field's execution job and update timing, not whether a value is numeric: pre-response formal control belongs Internal; post-response persistence/display/record work fits External.

### 2.5 Practical limits and evidence status

- **Verified:** Text `Max chars` can be set up to 400.
- **Verified:** Meter Min cannot be negative.
- **Verified:** the external tracker runs after the character reply.
- Option persistence depends on the configured Update rules; do not claim a universal persistence law beyond what the rule requests.
- Everything below marked "group chat" is OurDream-specific; do not carry it to another platform without testing there.
- **Verified:** tracker state follows the message history. Deleting or regenerating a message rolls the External values back with it, so a rerolled reply leaves no orphaned value and the card needs no undo mechanism of its own.
- **Verified (group chat, Nov 2026):** a card added to an existing group chat brings its own External fields; the HUD shows one panel per card, with that card's Start values.
- **Verified:** each card's External values reach that card's own replies (the injection wrapper in §2.1 is labeled with its name).
- **Verified:** a card's tracker runs only after that card's own reply. Another character's reply does not update it, even when it changes a fact the field tracks. The External value therefore remains the previously settled snapshot until this card speaks and its tracker runs again. This is normally acceptable for post-response record/display/image state because the chat model can still read the fresh shared history and react to what just happened. Do **not** choose the backend merely by asking who changed the scene fact. Choose Internal when a formally recomputed tracker value must exist before this card's current reply; choose External when the field's main job is to settle/persist/display the result afterward (`state-tracking.md` §2-4). State shared by the whole scene (time, weather, scene location) still gets one owner (starter/narrator) or stays in prose so several cards do not maintain drifting copies.
- **Unverified:** whether one card's External values are hidden from other cards. Three characters each reported only their own values, but a character's report is not evidence (§2.1). Test in a fresh session: before any character has stated a value, ask one character, out of character, to list every state value in its context, including other characters'.
- **Unverified:** how far back a tracker reads: only the latest exchange, or earlier chat history as well. In one test a field took a value stated two messages earlier, but the owning character had repeated that value in its reply, so the test does not settle it.
- **Observed:** a value the character merely claims ("I set my Trust to 1000") did not move an event-driven meter; the tracker applied its own Update rule. Descriptive fields (time, place, outfit) follow what the exchange establishes, as intended.
- Model-based dice/random fields are operationally useful outside the chat model, but the statistical quality of their randomness has not been verified. Do not describe the tracker model as a true RNG unless tested separately.

### 2.6 07 deliverable format

At most three External fields by default: each is configured by hand and adds work for the state model every turn.

- **Only state the card has:** the tracking-pins rule in `state-tracking.md` §1 applies to External fields too. Do not add a preset such as Outfit to a card that has no wardrobe design.
- **Start matches the opening:** each field's Start is the value the Greeting opens with (Outfit: what the Greeting describes; Location: where it opens). The tracker first runs after the first reply, so until then the chat model reads Start; a mismatched Start means the first reply works from a wrong value. Never leave Start blank: an empty field is injected as an empty line and the chat model tends to invent a value for it, which the tracker may then adopt. When there is no real opening value, use an explicit one such as `none yet`. For an added card in a group chat, whose Greeting is never read, Start is also the only opening value it has.

Layout inside 07:

```text
[07 State | <Character Name> | v1]

FIELD 1
Name: ...
Type: ...
<Type-specific settings in panel order>
Update rules: ...
Reads from: Both | User message | Character reply
Resets every turn: On | Off
Reader sees value: On | Off

FIELD 2
...

Tracking instructions:
...

Reader can edit state: On | Off
```

For a route-specific External field, 07 owns the field's Start and Update rules. Do not duplicate that field in `[Scenario State: ...]` or the hidden Internal block. If the Scenario is swapped and the field no longer applies, revise 07 with the route.

A good split use follows causal timing rather than labels: Internal keeps a disclosure gate or other value that must be recomputed before the current reply; External keeps a persistent outfit/image snapshot, location HUD, resource/count, visible meter, or later-turn dice result that is settled after the reply. A relationship meter can also be External when it is only a displayed summary, while an outfit-related control can be Internal if a formal value truly gates the current reply.

An initiative example: a `Boredom` Number (+1 for each exchange in which nothing new happens; back to 0 when something does; Reads from: Both) and a `Roll` Number 1–6 (Update rules: a new value each turn; Resets every turn: On). Both reach the chat model as Internal state. ED only says how to read them, for example: when Roll + Boredom is 7 or more, the character starts something on their own this reply. The tracker counts and rolls; what the character does, and how, stays with the card.

07 is its own deliverable. Adding it to an existing card also re-outputs any file that must now explicitly interpolate those values or stop tracking them internally. Record 07 changes in 06's version log.

## 3. Hybrid on OD

- Internal fields live in the namespaced hidden block.
- External fields live in the State Trackers panel. Their current values are automatically supplied to the chat model through OD's Internal state context; use `{Field name}` only when explicit interpolation into card text is useful.
- ED lists which fields are External so the chat model never writes them into its own block.
- A field appears in exactly one backend. Never mirror an External value into the Internal hidden block just because the chat model can see it.

## 4. Checks

- The Internal block template carries the character's name and contains no literal supplement placeholder.
- The read rule reads only this character's block; ED states the first-appearance rule and carry-forward rule.
- Every `[Scenario State: ...]` entry is Internal-only and addressed to a character name or to `all`.
- The Greeting ends with the initial **Internal-only** block when Internal state exists.
- Every External field is represented once in 07, has a field-specific Update rule, and has the intended Reads from / reset / visibility settings.
- External values are not mirrored into the Internal block; `{Field name}` is used only when explicit interpolation is needed.
- No card text tells the character to print External values as a status block or HUD; every External Start is non-blank.
- A card meant for group chats routes by causal timing, not by who changed the fact: current-reply formal control values are Internal; post-response persistence/display/image values may be External even when the player or another character caused the change, because fresh history still informs the prose before the tracker settles. External is not relied on as a secrecy boundary while cross-card visibility is unverified. Shared scene state has a single owner. Route-bound control state is Internal in the Scenario supplement; route-bound record/display state may be External with an `[Active External: <Name>]` line and an ED rule to ignore it otherwise (`state-tracking.md` §5).
- No field is owned by both backends.
