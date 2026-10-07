# Guided start

Use this when the user has a rough idea and wants help discovering the character through conversation. Keep it conversational. Do not present a form or march through a fixed questionnaire.

## First questions

Start with the smallest high-value set. Normally ask two to four questions at once, phrased naturally.

Prioritize:

- **Gender.** Resolve it explicitly. The user may name it or say that you should decide. Do not silently guess.
- **Attraction core.** Ask what quality, contradiction, relationship dynamic, atmosphere, or other trait should make this character especially compelling to the user. "I only know the feeling" is a valid answer.
- **What already exists.** Invite the user to share whatever is already clear: role, job, setting, relationship, premise, appearance, scene, or fragments. Do not demand every category.

If age is unspecified, default the focal character to an adult. Ask age only when it materially changes the design. If the user explicitly requests a minor, acknowledge that and keep the design age-appropriate. Do not ask about the Explicit Adult Scene Runtime, and do not design romantic or sexual relationship content for that character.

## Follow the useful gaps

After each reply, ask only questions whose answers could materially change the character, the interaction logic, or the opening. Useful gaps include:

- **Identity or role.** What kind of person are we actually playing with?
- **Interaction premise.** Why do this character and the player keep having reasons to interact?
- **Reaction logic.** When the player approaches, challenges, helps, disappoints, or surprises them, what value or judgment pattern drives the response?
- **Opening situation.** What is already true when play begins, and what gives the first exchange pressure or direction?
- **Explicit adult-scene runtime, when relevant.** Only for adult focal characters. If the user already asked for detailed / explicit NSFW play, treat the full Explicit Adult Scene Runtime as enabled and do not ask again. If sexual content seems important but detailed explicit scenes are still ambiguous, ask one binary question: enable the full explicit-scene runtime, or keep sexuality at the character / relationship level only? Do not ask for an explicitness level, anatomy slider, act-by-act preference checklist, or "how far" the user wants the description to go. When enabled, the default is direct, specific, physically detailed adult rendering. The user can tune style later if they want. Never enable or ask about this module for a minor focal character.

Do not ask for trivia merely because more detail could make the card richer. Do not confuse missing trivia with missing character logic. A birthday may be optional; a reason for the second conversation may not be.

Avoid leading questions that secretly choose the trope for the user. Instead of "What cute habit hides under the cold exterior?" ask whether there is an inner/outer contrast at all, and let the user decide what it is.

## Conditional progression-state check

Do **not** ask tracker questions by default. First make a silent design judgment: does this character have a cross-turn change that genuinely needs persistent state because later behavior, disclosure, access, risk, or availability depends on accumulated evidence?

Use a quick failure test: if the model forgot this state about three responses later, would that plausibly cause a continuity error, knowledge leak, repeated milestone, relationship jump, impossible combination, pacing error, or gate mistake? If not, do not track it.

Good reasons include a relationship variable that changes slowly, a suspicion or knowledge state that must persist, a one-way milestone, a recurring resource or condition, or a threshold that actually controls what becomes available. A tracker is not needed merely because the character has emotions, because the story is long, or because a template has room for one.

If no real tracking job exists, skip this section entirely and never ask the user about trackers.

If a tracking job does exist and the needed design is not already clear from the user's material, ask only the smallest useful set, normally two to four questions in one turn. Adapt the wording to the concept rather than presenting a form. Resolve:

- **What needs to persist?** Identify the one to three dimensions whose change would materially affect later play. Do not create a meter for every relationship facet.
- **What representation fits?** Prefer a latch or discrete state such as `Unknown -> Suspected -> Confirmed`, then a simple band such as `LOW / MID / HIGH`. Use a numeric counter or `0-100` scale only when counting, accumulation, or thresholds are themselves meaningful to the fiction.
- **What changes it?** Require observable evidence or an established event. A private realization, message count, praise, or a changed number is not automatically enough.
- **Does it gate anything?** Ask only when relevant whether reaching a state makes a behavior, disclosure, location, ability, or relationship move available. A gate permits; it does not force.
- **Should the state be visible?** Ask only when output presentation matters. Hidden runtime state is a valid default; visible summaries are optional.

Treat the tracker as a continuity aid, not a personality engine. The causal order is **event/evidence -> character interpretation -> choice/consequence -> state update**. Never reverse this into **state changed -> therefore the character must act differently** without character-level reason.

If the user says to decide for them, choose the lightest representation that works and continue.

## Generation readiness

Treat a point as resolved when the user supplied it or explicitly delegated it to you.

The character is ready enough to generate when these are resolved or can be safely completed from what the user already gave:

- gender;
- the attraction core;
- identity or role;
- the ongoing interaction premise with the player;
- enough reaction logic to predict ordinary responses without inventing a new personality each turn;
- an opening situation.

Wrong Attractors, future growth, exact appearance, detailed history, and special mechanisms can improve the card but are not universal generation gates.

## Generation checkpoint

After roughly four rounds of guided questions, or earlier when the character is already ready enough, stop and tell the user that generation can begin. Offer three choices in plain language:

1. generate now;
2. continue the interview;
3. deepen one specific area.

Do not continue questioning by default after this checkpoint. If the user chooses more interview, continue naturally and offer another checkpoint when a meaningful block is complete.

When the user chooses to proceed toward a finished card, treat confirmation as an optional workflow mode rather than a required approval gate.

- If they already asked for direct generation, generate immediately and do not ask again.
- If they already asked to review or confirm first, provide a compact confirmation summary and wait for corrections or approval.
- If no preference is known, ask one concise mode-selection question:

> Would you like a brief confirmation summary first, or should I generate the card directly?

If they choose confirmation-first, provide only a compact summary and wait. If they choose direct generation, generate immediately and do not ask for a second confirmation. Do not turn this into another questionnaire.

If the user says "generate now," "you decide," "skip the rest," "no need to confirm," or equivalent at any point, skip confirmation, stop the interview immediately, and complete unresolved noncritical details yourself. Preserve every decision the user already made.
