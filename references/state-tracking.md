# Module: State Tracking (shared v2026110706)

Shared module: kept identical across the author's character-building Skills.
Purpose: once the host Skill decides a card needs persistent state (a tracker), this module defines the fields and decides **who maintains each field** (the backend). It is platform-neutral. How a backend is physically carried on a given platform lives in a platform adapter; for OurDream that is `od-state-adapter.md`. Field names, `{placeholders}`, HTML comments, and panel settings are adapter details, not part of the tracker's definition.

## 1. Field rules (every backend)

- **Field set:** track only state play needs that the recent story cannot reliably rebuild: what the card shows each turn (a date, place, outfit, resource, or HUD value), what events switch (an altered body state, a visible form, a suspended power), first-time latches, and counts. Each field gets a definition, an initial value, an update condition, and a reset or expiry condition. Most cards need one to three fields; every field is one more thing that can drift each turn, so each must earn its place.
- **Representation:** prefer latches and discrete states; a band (LOW / MID / HIGH) when coarse progress is useful; a number only when counting is part of play. Free-form text is appropriate when the state itself is descriptive and must persist, such as current outfit or location.
- **Tracking pins:** a tracked value persists until its rule changes it, and a persisted value works as an anchor. Track only state the card actually has: an outfit field on a character with no designed wardrobe pins the first outfit, so a character who would otherwise change clothes on their own stops doing so. When the card does have the state, the update rule keeps ordinary changes possible (a new day, a scene change, the character dressing for an occasion), not only the changes the user causes.
- **Store and derive:** store causes; derive labels, tells, and permissions from them; never keep two fields for the same fact. Exception: store a derived value when deriving it is error-prone (a weekday from a date).
- **Partial progress:** a band that rises only after several qualifying events also stores the running count (for example `SharedLife: LOW 2/4`), with the same numbers as the thresholds.
- **One-turn opportunities:** a door that is open only while a specific question is on the table is judged each turn from the rules and stored values; it is never stored. A pause that holds until a named event, and a timed effect, are lasting states and are stored.
- **Ordered beats and presence:** a card whose beats must happen in order stores the next one due by name. A character who leaves scenes has their whereabouts stored (`present / away@place`), so they cannot overhear or reappear by coincidence.
- **Update rules:** for each field, in plain language: what event changes it, by how much, what never changes it, plus a few hard positive and hard negative examples. The character's own actions and the mere passing of time never raise a relationship value by themselves. Write progression in narrative language (what becomes reachable in the scene), not in consent or legal vocabulary (`drift-checklist.md` §E).
- **Intensity is not meaning:** arousal or scene-intensity values never turn into trust, love, or disclosure.
- **Player authorship:** no backend ever invents the player's thoughts, feelings, consent, or actions.

## 2. Backends and causal timing

| Backend | Who maintains the state | Strengths | Weaknesses | Best for |
|---|---|---|---|---|
| **Internal** | The chat model, during its own reply-generation loop | Can recompute a formal value before the current reply uses it; understands nuanced story meaning; simple to deploy | Can slip or drift over a long chat; weaker at exact counting | **Pre-response control state**: a tracker value that must be formally updated before this reply because it gates, branches, permits, suppresses, or otherwise changes what the character may do now |
| **External** | A separate tracker model or the platform's state system, typically settling after the reply | Persists independently of the chat model's own memory; supports HUD/display, reader editing, structured carry-forward, and post-turn bookkeeping | Understands the story less completely; counts can still go wrong; on post-reply systems the newly settled value is naturally available from the next turn | **Post-response record state**: a value whose main job is to settle, persist, display, count, or expose the result of the exchange for later turns, HUDs, images, or auditing |
| **Hybrid** | Split by execution job | Keeps immediate control with the chat model while offloading durable record/display work | Ownership must be explicit or the two sides fight | Cards that genuinely need both pre-response control and post-response record/persistence |

**Primary routing rule: route by causal timing, not by semantic category.** Do not decide a backend merely because a field is called trust, outfit, mood, location, relationship, or resource. Ask what job its **updated value** performs in the turn:

- If the tracker must formally compute the new value **before the current reply is composed** because ED uses that value as a gate, branch, control, or legality condition for this reply, use **Internal**.
- If the field mainly **settles or records the exchange after the reply** for persistence, display, image state, counts, later turns, or reader inspection, prefer **External** when the platform supports it.
- Fresh conversation facts are not the same thing as a pre-response tracker update. The chat model may react to an explicit event in the current user message or visible history even when an External snapshot has not settled yet. Do **not** move a field to Internal merely because the player or another character can change the underlying scene fact. Internal is needed when the card requires a newly computed tracker value itself before acting.
- If one concept has two genuinely different jobs, split the jobs rather than mirroring one field. Example: an Internal `DisclosureGate` may decide whether a reveal is available this reply while a separate External `Affection HUD` records a coarse player-facing relationship summary. They are not two copies of the same truth.

**One authoritative owner per field.** Hybrid is a split, never a mirror: a field is either Internal or External. Card text may read an External field's value; the chat model never writes or re-derives an External-owned field, and an Internal field is never also configured externally.

Dice and random numbers usually fit External when the draw is a post-turn result, persistent record, HUD value, or input for a later turn. If a newly generated roll must decide **this same reply**, a post-reply External tracker cannot be the current-turn source; use an Internal/pre-response mechanism or consume a value already established before generation. If the user explicitly chooses an all-Internal deployment, respect it and note in 06 that randomness and exact counts will be weaker. Do not promise mathematically fair randomness from a model-based tracker unless that backend has been separately verified as a true RNG.

## 3. Router (run only when a tracker is actually needed)

1. If the card needs no persistent state, ask nothing about trackers.
2. Is the target platform known? If not, ask.
3. Does that platform offer an external tracker or state system? If not, or if unknown and the user cannot say, use **Internal**.
4. If it does, ask once: **all internal, all external, or split?** Give a short recommendation per field from §4 in the same message. If the user says "you decide", allocate by §4. When the card is meant to be added to group chats, say so in the recommendation: on OD its Internal block sits in the shared chat history where every character can read it, while External values stay out of that history; whether other cards also receive them is still unverified (§4). Group-chat behavior is platform-specific: everything this module says about group chats is verified on OD only; on another platform, find out how its group chats handle state before applying it.
5. Record the backend of every field in 06 Notes as a decision.

The user may answer any of these in advance; never re-ask what they already said.

## 4. Default allocation (when the user leaves it to the builder)

Use this order. The examples below are secondary clues, not semantic buckets.

1. **Current-reply dependency:** does the newly computed tracker value itself have to exist before this reply because it gates, branches, permits, suppresses, or selects behavior? -> **Internal**.
2. **Post-reply settlement:** is the field mainly recording what the exchange has established so it persists, displays, feeds image state, counts, or becomes available next turn? -> **External** when supported.
3. **Both jobs:** split responsibilities only when they are genuinely different facts or abstractions; never mirror one value across both backends.
4. **Neither job:** do not track it. Let ordinary conversation context carry it.

Secondary clues:

- Nuanced interpretation, multi-condition gates, and values whose **formal updated result** controls the current reply lean Internal. A relationship construct may be Internal when it opens or closes a disclosure gate now, but the word `relationship` does not make it Internal by itself.
- Stable persistence, HUD/display, reader editing, structured descriptive snapshots, numeric resources, exact-ish counts, time/date, later-turn dice results, and image-facing state lean External. External does **not** mean numeric: Outfit or Location can be excellent External text fields when their main job is durable snapshot/display.
- Conversely, a coarse relationship meter may be External when it is only a persistent/displayed summary and does not directly legislate the current reply.
- A fresh event in the user message or visible history can still shape the current prose directly. Do not add an Internal tracker merely to restate a scene fact the chat model can already see; add Internal state when the card needs a persistent **formal control value** computed before acting.
- With no field that benefits from External settlement, stay fully Internal even when an External backend exists: it is simpler to set up.
- **Cards meant for group chats** (OD-specific): External keeps a value out of the shared reply history, where the Internal block is readable by every character. Whether other cards also receive a card's External values is unverified, so External is not a secrecy boundary for load-bearing hidden information. OD's External tracker settles after the owning card's reply; that timing is normal for record/display state. Do not route by **who changed the scene fact** alone. Use Internal only when this card needs a formally recomputed value before its current reply. State shared by the whole scene (time, weather, scene location) gets one owner, usually the starter/narrator card, or stays in prose.
- **Route-bound control state** defaults to Internal in the Scenario supplement slot (§5), because it often drives route gates or phases. Route-bound **record/display state** may be External when HUD, image state, exact persistence, or reader editing is worth the setup; give it an activation marker (§5). The causal-timing rule above wins over the field's name or category.

## 5. Placement in the card files

All **reusable tracker runtime** lives in **ED**: backend protocol, the internal block format, cross-route and generic field logic, and any route-neutral update rules. Scenario may provide declarative route-specific **Internal** state payloads; it never owns a second tracker engine. This keeps the single-chat runtime simple after initialization while preserving the Scenario swap test.

- **Cross-route fields:** hold under any route (a body state, a latch about the character, presence). Internal cross-route fields are defined and defaulted in ED. External cross-route fields live in the platform's external tracker configuration.
- **Generic slots:** fields every route has, whose referent the route supplies. ED defines the field, its values, its update rule, and its default in route-neutral terms; Scenario only says what it refers to. Example in ED: `Secret: Hidden / Suspected / Known` tracks the current route's main secret, as named in the Scenario in use. Scenario: what the secret is and who holds it.
- **Scenario supplement slot — Internal only:** fields that exist only when a route provides them **and are assigned to the Internal backend**. The Scenario in use may carry an addressed data entry with keys, defaults, and one short route-specific update condition each, for example `[Scenario State: <Character Name>] FavorOwed: No (Yes once Anna agrees to cover for them; No again once repaid)`. At initialization the character appends those fields after its fixed Internal fields, in Scenario order, then carries them forward from the previous state record. An entry addressed to another character is never used; an entry addressed `all` is used by every character in the chat.
- **Route-specific External fields:** never appear in `[Scenario State: ...]` and never enter the Internal block. Their name, start value, and update rules live in the platform's external configuration (for OD, `07 State`). Scenario holds only the story facts those rules refer to. If a Scenario swap removes or replaces such a field, regenerate/remove the corresponding external configuration and record the change in 06.
- **Activation marker for route-bound External fields:** an External field travels with the card into every chat, including group chats with another Scenario, and keeps its HUD panel there. Do not delete it for that; mark it inactive instead. The card's own Scenario carries one line naming the route-bound External fields it activates, for example `[Active External: <Character Name>] Dependency Value`. ED says: a field listed as route-bound is active only when the Scenario in use carries an `[Active External: <Character Name>]` line naming it; otherwise ignore its value and do not refer to it in play. Whether the tracker keeps updating it meanwhile does not matter, because the character does not read it. The field may still show in an unrelated group chat's HUD, since OD offers no confirmed conditional field visibility; that is one reason route-bound state defaults to Internal. Cross-route External fields need no marker.
- **Binding rule:** a generic slot or Internal supplement binds only to what the Scenario in use states explicitly (named for this character, or for the whole scene). When the Scenario states nothing for it, the slot stays at its default and inactive; never invent a referent.
- **Carry-forward rule:** every Internal field that appeared in the character's previous state record appears in the next one; when unsure of a new value, carry the previous value unchanged.
- **Greeting** (single chat) ends with the complete **Internal** state record only: every Internal cross-route field, every Internal generic slot, and every Internal supplement field from the card's own Scenario, at their opening values. External values are initialized by the external backend, not mirrored into this block.
- External backend configuration is its own deliverable in the platform's format (for OurDream, `07 State`; see the adapter). It is never pasted into a text field.

## 6. Recovery

- **Internal:** if the latest state record is missing or garbled, rebuild the state from established story facts and continue. Never reset to the initial value.
- **External:** read external values as given. If one clearly contradicts what has just happened in the story, narrate from the story and do not argue with the value in-fiction; fix the external rule or value outside the scene if needed.

## 7. Checks (only when a tracker is installed)

- Every field has a backend, exactly one owner, an initial value, and update, never-changes, and reset conditions; every change comes from an established event.
- ED carries reusable runtime and route-neutral Internal logic. Scenario carries only generic-slot referents and, when needed, an addressed **Internal-only** `[Scenario State: <Name>]` data entry.
- Every route-specific External field exists only in the external configuration, never in the Internal supplement or block, and is named in an `[Active External: <Name>]` line in the card's own Scenario, with ED ignoring it when that line is absent.
- ED names no route-specific person, event, or secret.
- Stored and derived values never contradict.
- The backend choice is recorded in 06.
- A card with state the recent story cannot rebuild (a displayed date or place, a first-time latch, a suspended power, a timed effect, a stage that gates beats) gets a tracker even when the interview was skipped.
