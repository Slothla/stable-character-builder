# Module: OurDream Platform Layer (shared v2026110706)

Shared module: kept identical across the author's character-building Skills.
Status: these are the Skill author's observations of OurDream (OD), dated where it matters. They are project assumptions, not universal LLM facts. When the user supplies newer evidence, it wins. Never present a guess about platform internals as fact; say it is a guess and suggest a quick test.

Read this module for every build, rebuild, or review aimed at OD.

## 1. Field caps (observed Oct-Nov 2026)

- Intro: under 2,000 characters. Target about 1,600 so the cap is never hit.
- Greeting: under 10,000 characters.
- Scenario: under 50,000 characters.
- APD field: 50,000 characters. ED cap not yet observed.
- Suggested reply: one only, at most 100 characters.

## 2. What the chat model actually receives

- APD arrives as "Personality Details", after one sentence the platform writes from the card's Personality option. Choose the Personality option that is the closest match to APD, because its sentence is read every turn.
- ED arrives as the extended details. Scenario arrives as `<scenario>`.
- Age, Occupation, Relationship, Hobby, and Fetish arrive as short labeled fields. A filled Fetish field acts as an always-on trait; fill it only with what should be always on.
- The player's persona arrives as `<user_details>`.
- **The Appearance panel and the image prompt never reach the chat model** (observed Nov 2026, single and group chat). They serve image generation only. So the character's look exists in chat only if APD describes it in prose: hair, eyes, height and build, the body details play will need, skin and texture, species or form traits and when they show, usual clothing. Fixed visual invariants still belong in the Appearance panel for images; APD carries the prose version for the chat model.
- Which tag wraps APD and ED has changed between checks. Tell files apart by their headers and content, never by tag.
- Each reply, the platform adds to the user's message the speaking character's External tracker values (wrapper in `od-state-adapter.md` §2.1) and a reply-length line such as `[Length check for your next reply: usually 30-40 sentences, but shorter when a quick beat serves the moment better; never pad.]` (observed Nov 2026). A card that sets its own reply length competes with this line every turn; state a card-level length only when the card truly needs one, and expect the platform line to pull against it.

## 3. Group chats

- The card the chat was started with loads every field except Intro. A card added to an existing chat loads only APD and ED; its Scenario and Greeting are never read there.
- A group chat's own Scenario replaces the cards' Scenarios; each character can get its own opening message on that page.
- Every character in the chat, starter or added, reads the Scenario in use: the starter card's own, or the group chat's own when one is set (verified with the Skill author's test cards). An added card's Scenario is never read, but the shared Scenario is.
- In group chats `{{user}}` is replaced by the player's persona name, and reading other cards can be slightly lossy and mixed with platform text.
- The chat history is shared, so any state a card writes into its replies (a hidden block, a footer) is visible to every character. Each card's External tracker fields are kept per card and updated only after that card replies (`od-state-adapter.md` §2.5). An added card's External fields come with it even when its own Scenario is not in use; route-bound ones need the activation marker in `state-tracking.md` §5.
- If a card will be added to other chats, what holds under **any** route lives in APD or ED: stable character facts and cross-route runtime (formats, interaction controls, generic knowledge and NPC operation, reusable tracker protocol and route-neutral field logic; see `state-tracking.md` §5). What belongs only to one route (that route's NPCs, events, secrets, relationship state, tracker-slot referents, an Internal-only addressed `[Scenario State]` payload, or route-specific External tracker configuration) stays route-owned. Never move route-only content into ED just so a group chat can see it; that breaks the Scenario swap test. When a bug appears only in group use, check this placement before writing any rule.

## 4. Macros, hidden text, memory

- `{{user}}` and `{{char}}` macros work. Runtime files use `{{user}}` with they/them unless the user fixed the player's gender; Intro and Greeting address the player as "you".
- HTML comments are kept in card fields and hidden in chat. State blocks and image footers use them.
- Updating a card's definitions does not override patterns already established in an ongoing chat (recent context wins). Test changes in a new chat.
- OD's long-chat summary memory keeps the gist only. Do not design mechanics that need exact long-range recall (a running ledger, an exact count from fifty turns ago) unless a tracker carries the value (see `state-tracking.md`). Relying on the model's internal memory for such values is a defect.

## 5. Language and translation

- When a card is published, OD auto-translates the Greeting for players whose language is Chinese; it does not do this while the card is unlisted for testing.
- Every card with names that could be translated inconsistently carries one name-translation line (in APD by default), for example: `Name forms in Chinese: 森瑞希 (Mizuki Mori) · 三叶书店 (Mitsuba Books)`. Mixed-language cards always carry it.
- Project convention: for published cards the English version is the main release; a Chinese version may be kept alongside it.

## 6. Length budget

- Persistent text (APD + ED + Scenario) of a single-focal-character card has a **soft reference ceiling of about 90,000 characters**. It is a ceiling, not a target: the proportionality rules of the host Skill still decide how long a card should be, and most cards should be far shorter. The Skill author's best-performing cards were under 10,000 characters in total.
- Evidence: a card with about 49,000 Chinese characters of persistent text runs well for many players, so raw capacity is not the bottleneck; attention dilution is. Count length in characters, the way the user measures on OD.
- RPG and heavy sandbox cards may exceed the ceiling (100,000-150,000 characters is seen in the community). When a card exceeds it, record the reason in 06 Notes.
- Specialized presentation machinery (footers, HUDs, formats) adds length without making the character more complex; it never justifies a heavier character core.

## 7. Models

- For building and revising cards with an OD-side builder, recommend the strongest thinking model the chat offers. For running a finished card, suggest trying a few rounds on the models the platform offers.
- Keep model-specific adaptation (which model or version suits a card) out of cards and out of this Skill; models change too often.

## 8. Art-style variants

- Project convention: realistic-style variants use emoji in inner thoughts; anime-style variants use kaomoji and carry an appearance footer.
- A player may generate images with a different image model than the one the author trained the character on. Realistic-style image prompts must work across models; natural language is the more universal choice. Some realistic models read Danbooru-style tags, others natural language.
- Kaomoji and emoji in cards come from a closed library the model uses as-is: at most one per inner-thought reaction, kaomoji only in the first slot, emoji anywhere. If a kaomoji / emoji library Skill is available, take the set from it. If an image-tag library Skill is available, use it for image tags; tags only need Danbooru-style format, not tags that actually exist on Danbooru.
