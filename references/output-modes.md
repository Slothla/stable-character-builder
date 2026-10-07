# Format and delivery modes

Handle transformation depth, target format, language, and edit scope separately. The user's request overrides the default. Changing delivery format must not silently change the person.

## Transformation depth

### Local edit
Preserve the source structure and change only the requested area.

### Structural rewrite
Reorganize the affected document or documents. Preserve canon and approved voice; do not preserve wording or headings merely because they already exist.

### Full architecture rebuild
Use the full rebuild workflow from `architecture-rebuild.md`. Preserve canon, not document architecture. Recompile the card into Character / Runtime / Scenario ownership and use the required functional schema from `SKILL.md`.

### Format conversion
Preserve the person's logic while mapping it into the target platform's fields. Do not also attach the default five-part set unless requested.

## Default five-part set

| Piece | Default language | Writes |
|---|---|---|
| 01 APD (Character Profile) | English | Who the person is and how their cognition generates choices |
| 02 ED (Runtime Rules) | English | How the simulation enforces authorship, knowledge, state, gates, change, continuity, anti-drift, delivery guard, and recovery |
| 03 Scenario | English | What is true now, who knows what, what pressures are active, and what possibilities are currently open |
| 04 Intro | English | Player-facing premise and attraction |
| 05 Greeting | English | The first real exchange from the exact opening |

For a full default build or rebuild, deliver five separate plain-text files named:
- `01_APD.txt`
- `02_ED.txt`
- `03_Scenario.txt`
- `04_Intro.txt`
- `05_Greeting.txt`

## Structural floor for a new build

A simple new character may use a lighter version of the architecture. Named sections are still required in APD, ED, and Scenario, but do not manufacture empty machinery.

Useful minimums:

### 01 APD
- Identity and ordinary life
- True motive and self-model
- Attention, interpretation, and decision habits
- Voice and inner/outer expression
- Relationship logic
- Wrong Attractors and stable boundaries

### 02 ED
- Player authorship
- Knowledge limits
- Decision and expression rules
- Relationship or character change rules where needed
- Continuity
- Anti-drift guidance
- Recovery rule when drift risk is meaningful
- Interaction controls only when installed

### 03 Scenario
- Premise
- Entry state and current relationship
- Established facts
- Knowledge distribution and hidden facts where relevant
- Active pressure or unresolved threads
- Possible directions without forcing an ending
- Exact opening situation

For a **full architecture rebuild**, use the full functional coverage map in `SKILL.md`, not only this minimum. Do not force one heading per function.

## One principle, three jobs

The same design principle may appear in different files when it serves different functions.

- APD: the character trusts completed promises more than flattering claims.
- ED: let fulfilled agreements change willingness to cooperate; do not treat praise, perceptive guesses, or long conversation as sufficient evidence for disclosure.
- Scenario: record which promises have actually been completed before the opening.

This is functional repetition, not waste.

## Intro and Greeting

Intro lets a player decide whether to enter. It does not automatically reveal unreleased secrets. When an interaction control such as a safeword is enabled, Intro may contain a concise OOC/player-facing notice explaining the trigger and its basic purpose. That notice is disclosure to the player, not character dialogue and not a substitute for the ED rule.

In the default five-file format, **Intro is hard-capped at 2000 characters**. Prefer a clean shorter Intro over squeezing extra lore into the limit.

Greeting performs the person, runtime, and situation. It must:
- begin from the exact opening state;
- have the character do or say something consistent with current knowledge and priorities;
- leave real room for player response;
- avoid inventing unstated player thoughts, feelings, choices, consent, intent, or history.

Greeting has no default 2000-character cap. Use the length the opening needs unless the target platform supplies another verified constraint.

If an interaction control is enabled, ED must independently contain the literal trigger and full operative behavior. Never write only `see Intro` or an equivalent cross-reference in ED. The character does not need to explain the control in Greeting or normal IC prose unless the user explicitly requests an in-character briefing.

Inner thought appears only when the requested narration or character design needs it. Promotional text and OOC notices in Intro do not become character knowledge.

## Another target format

Start from the card, fields, version, or import format the user supplied. Place Character, Runtime, and Scenario responsibilities where that platform will actually load them.

- Description-like fields usually hold Character.
- Situation or lore fields usually hold Scenario.
- First-message fields hold Greeting.
- Runtime rules must go into a field that is actually injected; do not hide critical behavior only in an author note that the model never sees.
- Intro may become the platform's public blurb. If there is no public-blurb field, omit or merge it as requested.
- Follow a user-provided sample or verified official format for importable files. Do not claim import compatibility when the version or schema was not verified.

## Language override and partial edits

The default five-part set is all-English, but the user may request Chinese or mixed-language output. Preserve identifiers and proper names they want kept.

If the user asks only for one piece, deliver that piece. Do not rewrite the rest just to complete the set.

Do not attach an architecture report, test log, or design commentary unless asked. The delivered artifact should be usable as the card itself.
