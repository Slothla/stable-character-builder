[English](CHANGELOG.md) | [简体中文](CHANGELOG_ZH.md)

# Changelog

## 2026110706

The previous public release dates from early October 2026. This release consolidates a month of rebuilding and play-testing.

### Added

**State tracking with selectable backends** (`state-tracking.md`)
- A tracker is installed only when the card needs persistent state. Each field has one owner:
  - **Internal**: a hidden block that the chat model rewrites every reply.
  - **External**: the platform's own tracker system.
  - **Hybrid**: split by field, never mirrored.
- Routing follows causal timing:
  - Values that must be recomputed before the current reply (gates, branches) are Internal.
  - Values that record, persist, or display the result of the exchange fit External.
- A lightweight router asks about trackers only when one is needed. It asks which backend to use only when the platform offers an external system.
- Route-neutral fields live in ED. Scenarios supply referents for generic slots, plus an optional addressed `[Scenario State: Name]` entry for route-only Internal fields.
- External fields that belong to one route are named in an `[Active External: Name]` line in the card's own Scenario. In any other Scenario they are ignored instead of deleted.
- A new **tracking-pins** rule: a tracked value persists, so only track state the card actually has. For example, an outfit field on a character with no designed wardrobe freezes the first outfit.

**OurDream adapter** (`od-state-adapter.md`)
- A complete configuration format for OD's State Trackers panel, delivered as `07 State`, with field types, settings, and limits.
- The platform's verified state-injection wrapper, and what it implies for card text:
  - Don't tell the character to re-print External values as a status bar.
  - Show values through the HUD instead.
- Verified behavior:
  - External values reach the chat model whether or not they are visible in the HUD.
  - Image generation also reads tracker fields.
  - Deleting or regenerating a message rolls tracker values back with it.
- Group-chat behavior, marked OD-specific:
  - An added card brings its own fields.
  - Each card receives only its own values.
  - A card's tracker runs only after that card's own reply.
  - Internal blocks sit in the shared chat history and are readable by every character.
- Practical rules:
  - Never leave a field's Start value blank.
  - Match Start values to the opening.
  - A tag-format External field can drive image tags.

**OurDream platform layer** (`od-platform.md`)
- Field caps.
- What the chat model actually receives. The Appearance panel never reaches it, so the look must be written in APD prose.
- Group-chat loading rules.
- Translation notes.
- A soft reference ceiling of about 90,000 characters of persistent text.

**06 Notes** (`author-notes-06.md`): a default author-side file in the user's own language. It records decisions, assumptions, names used, installed modules, and a version log. It is never pasted into the card.

**Opening funnel** (`opening-funnel.md`): the title, the card-tile line, the Intro, the Greeting, and the first 5-10 exchanges decide whether a chat starts and continues.
- The first sentence of the Intro must work alone as the tile line.
- The Greeting must carry a charged hook and end on something easy to answer.
- Scenarios offer beats reachable early.

**Supporting NPCs** (`npc-module.md`):
- Precision tiers.
- A capsule per NPC with objective, knowledge, and a life of their own.
- Naming rules that avoid the model's default name pool.
- Male NPCs are not romantic competitors unless the card is built for that.

**Secrets and reveals** (`secrets-and-reveals.md`): secret kinds, and whether the Intro reveals them.

**Drift checklist** (`drift-checklist.md`): an author-side catalogue of common drift patterns. The builder selects the few that apply to the card.

### Changed

- **Adult module**: `adult-intimacy-runtime.md` is replaced by `adult-intimacy-module.md`. The module is compiled into each character:
  - what they notice first;
  - how they initiate;
  - how their responses change with intensity;
  - what generic persona they risk drifting into.

  Diagnosis questions and a compile check confirm it is not merely mentioned.
- **Player authorship** now separates inferable content from non-inferable content:
  - *Inferable*: observable results and involuntary physical consequences of what the player set up. These may be rendered.
  - *Non-inferable*: the player's decisions, voluntary actions, dialogue, thoughts, feelings, consent, or new facts about them. These are never authored.
- **Scenario independence**: APD and ED must stay valid under any Scenario. A swap test flags route-specific content in them.
- **Safety and interaction-control budget**: one authoritative rule for each job, with no repeated generic consent prose. When adulthood needs emphasis, it is established through positive adult facts, not scattered negations.
- **Out-of-character agreements** (a safeword, an opted-in premise) are ED runtime rules, not part of the character's knowledge.
- **APD always describes the look in prose.**
- **The Scenario's opening situation** is written as story fact, not as instructions to whoever writes the Greeting.
- **Traits are a repertoire**, not a per-turn checklist. Tracker and progression rules use narrative language, not consent or legal vocabulary.
- **Acceptance tests** now apply to new builds as well as rebuilds. New tests:
  - identity-swap;
  - Scenario-independence;
  - opening-funnel;
  - OurDream platform;
  - decision-coverage;
  - safety budget;
  - priming.
- `agents/openai.yaml` gains icon and policy metadata, with `assets/icon.svg`. A `VERSION.txt` file is added.

### Removed

- `references/adult-intimacy-runtime.md`, superseded by `adult-intimacy-module.md`.
