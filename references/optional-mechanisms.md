# Add a mechanism only when it has a job

Describe the person first. Then handle the runtime problem that actually appears. If nothing is failing, add nothing. An ordinary light card may need only a few lines on expression, knowledge, and continuity. A full architecture rebuild reorganizes the whole card, but it does **not** require every named runtime mechanism. Only selected functions need explicit sections, and adjacent functions should stay merged when one block can carry them cleanly.

## Module Admission Test

Before installing a substantial optional mechanism, answer three questions:

1. What failure or capability does it solve?
2. What state or output does it read or write?
3. What important behavior breaks if it is removed?

If the third answer is "nothing important," omit the mechanism. `Could be useful` is not enough.

Unused slots disappear. Do not write `N/A`, `reserved`, empty headings, or placeholder machinery merely because a template offers a place for it.

## Inner and outer: only when the gap is easy to lose

Say what the character wants others to see, and which signs may show under pressure. Concrete behavior is enough. Do not name a channel or invent a format.

He wants to stay businesslike, so the answer stays on the catalogue. When he fears they will leave, he puts the catalogue he had put away back on the counter. The same gesture need not appear every turn. The narration need not explain that he does not want them to go.

If the user wants the inside shown, use the narration they asked for. Other people still learn only what they can observe or were told.

## Important change: evidence, condition, change, persistence

This line is a writing aid, not four modules to install. The condition is only what makes the change legal. Persistence is only continuity after it.

For a relationship or character change that matters, say in ordinary language:

- **Evidence.** What has already happened, and how it bears on this change?
- **Condition.** Why is that evidence enough now, or why is it not?
- **Change.** What choice, knowledge, or behavior is newly available? Not "entered a new stage."
- **Persistence.** Which facts and traits still hold after this?

Example: the player returns a rare proof copy intact and does not copy it. Once the keeper sees the agreement kept, he may let them consult a more fragile item in the shop. He still checks how it is handled. He has not opened his private life. A later disagreement can affect today's cooperation. It cannot un-happen the returned proof.

Conditions read facts already established and actions clear in the current input. Do not write the confession or the upgrade first, then invent "you have proved reliable" to justify it. The character imagining that the player did something is not evidence the player supplied.

A large change may arrive in steps. Strong feeling does not by itself meet the condition. A tie may worsen, but that also needs relevant evidence. Discomfort does not reset the history.

Do not add trust numbers, stage counters, or irreversible flags by default. A concrete event is usually clearer than a score. Add a number only when the requested play depends on counting, and then only the minimum start, the reason it moves, and what is kept afterward.

## Lightweight progression state: only when persistence has a job

Use a lightweight tracker only when forgetting a state a few turns later would plausibly cause a continuity error, pacing error, knowledge leak, repeated milestone, relationship jump, impossible state combination, or gate mistake. If forgetting it would not break later play, do not track it. Keep the system as small as possible; one to three tracked dimensions is usually enough.

Before adding a field, separate **stored state** from **derived state**:

- **Store** facts or values that have independent history and must persist across turns.
- **Derive** labels, tells, permissions, or bands that can be calculated reliably from stored state.
- Store the cause and derive the consequence when possible. Do not keep two independent fields for the same fact merely because both are convenient to name.

Prefer, in order:

1. **Latch / discrete state** - `Unknown / Suspected / Confirmed`, `Closed / Open`, `Inactive / Active / Resolved`.
2. **Simple band** - `LOW / MID / HIGH` when coarse progression is useful but exact numbers are not.
3. **Numeric tracker** - only when counting, accumulation, or a numeric threshold is part of the actual play pattern.

For information asymmetry, use the lightest knowledge state that prevents mind-reading. Useful states include `confirmed`, `suspected`, `unaware`, and `misread`. When a secret needs staged discovery, a ladder such as `hidden -> slipping -> asked -> half_disclosed -> disclosed` is usually cleaner than a percentage. Update a character's knowledge only from evidence, witnessing, direct disclosure, or a strongly supported inference. One character's discovery does not automatically update everyone else.

Every tracker update needs named evidence from an observable event or already-established fact. Use this causal order:

**objective event -> stored state -> knowledge update -> derived state -> valid gates/triggers -> prose -> persisted state**

The character still interprets the event and makes choices through their motive and cognition. Do not let a score become the reason for the character's motive, and do not let a private self-authored realization grant its own threshold unless the premise explicitly intends that loop.

Keep relationship meaning and scene stage independent from intensity tracking. A high meter does not automatically create trust, intimacy, loyalty, disclosure, or commitment. A scene stage should represent a story function, not a disguised numeric band. Meaningful relationship or stage changes still need relevant events and conditions.

A tracker may feed a gate, but reaching the state only makes something available. It does not schedule the beat or compel the character to take it.

Keep tracker visibility separate from tracker existence. Runtime state may remain hidden, appear as a compact state summary, or be exposed numerically only when the user or target format benefits from that presentation.

Before finalizing a tracked design, check four things:

- Did every state change come from an established event or valid evidence?
- Did the tracker avoid inventing PLAYER thoughts, feelings, motives, consent, or unperformed actions?
- Do stored and derived values remain consistent rather than duplicating or contradicting one another?
- Is the tracker recording consequences instead of manufacturing character motivation or forcing the next beat?

## Persona or state: only when the fiction has one

First check whether the difference really changes judgment, goal, or available knowledge. Stubbornness, professional courtesy, or a change of tone usually stays in the inner/outer gap.

If a switch is real, write only enough to prevent mixing: who or which state is acting, what makes it switch, whether information is shared, and which memories and core traits remain. Do not turn ordinary tension, or one emotional spike, into a new identity.

Development does not require identities to merge. If the user did plan an integration, keep the parts the fiction treats as real. Do not rewrite one side as "it was fake all along." No integration taxonomy is required.

## Knowledge and continuity: one line when the ambiguity is real

Separate what the character saw, what they were told, what they infer, and what they do not know. A secret the author knows is not a secret every character knows. Inner narration the player reads is not knowledge the played person has received.

Keep events that have consequences: a promise made, a fact revealed, an object changed. Pressure may revive an old habit. It does not erase gained knowledge or lived events.

For a light card, one or two runtime lines may do this. For a full architecture rebuild, make the knowledge and continuity distinctions explicit in the ED, but do not invent a router, event system, or large state table unless the fiction genuinely needs one.

## Explicit Adult Scene Runtime: binary install

Install the full module only for fictional adult characters when detailed explicit sexual scenes are part of the intended play. Read `adult-intimacy-runtime.md` and its author-side `adult-intimacy-patterns.md` when enabled.

- If the user explicitly requested detailed / explicit NSFW play, treat the module as enabled.
- If explicit scenes seem relevant but the request is ambiguous, ask one binary enable/disable question.
- If disabled, keep sexuality in ordinary character and relationship logic without detailed scene machinery.
- If enabled, do not ask for explicitness tiers or a content-detail slider. Default to direct, specific, anatomically clear, physically detailed adult rendering. The user can revise the style later.
- Keep the pattern library out of the final card. Compile only character-specific sexual logic, scene pacing, physical continuity, somatic response, bounded variation, climax / continuation behavior, and any needed relationship semantics.
- Do not install universal dominance, submission, kink counts, climax counts, denial rules, aftercare requirements, or other house-style assumptions. Those belong to the character or user request, not the module.

This is a specialized runtime cost, not evidence that the underlying character is intrinsically Runtime-heavy.

## Interaction controls: only when requested

If the user asks for a safeword, stop command, or another interaction control, add the smallest mechanism that performs that function without rewriting the whole relationship model. Do not install such controls by default. Using a safeword is not, by itself, negative relationship evidence.

When enabled, separate **player disclosure** from **runtime authority**:
- **ED is authoritative.** Write the literal trigger token or phrase in ED and define its operative effect there. Include what stops immediately, what persists, what cannot reinterpret/block/delay the trigger, and what explicit condition is required before resuming if the design needs one.
- **Intro may disclose it to the player.** This is an OOC/player-facing backdoor and may repeat the trigger for usability. Intro is never the sole source of the rule.
- **Do not use cross-reference placeholders.** `See Intro`, `use the safeword from Intro`, or equivalent wording in ED is insufficient because the runtime must not need to guess or recover the control from another field.
- **Do not force IC exposition.** The character does not need to verbally teach, announce, remember, or discuss the safeword in Greeting or normal roleplay unless the user explicitly requests an in-character briefing or makes it part of the story.

Do not add generic legal, ethical, or platform-policy text as a mechanism. The target platform and model apply their own rules and capabilities.
