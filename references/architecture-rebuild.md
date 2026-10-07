# Full architecture rebuild

Use this reference when the user asks to rebuild, structurally improve, optimize, or recompile an existing complete character card.

The goal is not to preserve the source document's shape. The goal is to preserve canon while producing a clearer, more executable runtime.

## 0. Set the architecture budget

Before extracting modules, classify how much runtime architecture the card actually needs. This is a structural budget, not a hard token quota.

### Light

Use when the protagonist is behaviorally clear and play does not depend on a state machine, staged secret system, or multiple conditional mechanics. Typical needs are: a compact character generator, player-authorship and knowledge limits, relationship change only where relevant, continuity, a few anti-drift anchors, and a playable scenario. Merge adjacent jobs freely.

### Standard

Use when long-form play depends on several persistent consequences, meaningful information asymmetry, nontrivial relationship evidence, or a few gates / latches. Make those distinctions explicit, but keep unrelated machinery absent.

### Runtime-heavy

Use when the premise genuinely depends on interacting trackers, staged discovery, multiple gates, recurrent conditional permissions, complex state transitions, or comparable systems. Here the fuller schema may be justified.

For Light and Standard cards, absence is the default. A section or mechanism must earn space by changing generated behavior, preventing a plausible failure, or preserving something that would otherwise be forgotten. Merely being theoretically useful is not enough.

Specialized output systems such as image footers, rigid formatting protocols, visible HUDs, or platform adapters have their own cost. Keep that cost separate from the character's architecture budget.

As the card grows, increase semantic sectioning. Long files should have clearer retrieval boundaries, not just more prose. Natural prose inside a section is fine; mixing several unrelated execution jobs in one large block is not.

## 1. Extraction pass

Before drafting, silently recover the source into these buckets:

### Character facts
- identity, age, role, body or appearance facts that matter in play
- ordinary life, competence, habits, relationships outside the player
- values, desires, fears, pride, shame, limits

### Cognitive generator
- true motive
- self-model or self-account
- attention preferences
- interpretation biases
- recurring misreads
- decision tendencies
- inner and outer expression
- relationship-specific judgment

### Runtime logic
- player authorship constraints
- knowledge boundaries
- state or tracker logic
- gates
- beat conditions
- evidence for relationship or character change
- continuity rules
- interaction controls
- output format rules
- anti-drift rules
- existing recovery behavior

### Scenario state
- premise
- opening relationship
- established history
- secrets and knowledge distribution
- active threads
- available locations, resources, threats, NPC pressure
- unresolved consequences
- exact opening situation

Mark ambiguous source claims as ambiguous. Do not silently reconcile contradictions by inventing new canon.

## 2. Normalization pass

Reassign every extracted item to Character, Runtime, or Scenario.

Remove **same-layer duplicate wording** and control cross-layer repetition with a primary-owner rule. Keep repetition only when the second occurrence performs a distinct execution job.

For example:
- APD may own why the character values kept promises.
- ED may state only the operational consequence: fulfilled promises can increase cooperation; praise alone does not.
- Scenario may record which promises have already been kept.

Do not re-explain the whole value system in ED or Scenario merely because the principle matters there. Prefer one full explanation plus brief consequences or state facts in secondary layers.

## 3. Convert traits into generators

Replace adjective piles with executable distinctions.

Weak:
- shy
- possessive
- intelligent

Stronger:
- notices whether the other person hesitates before answering;
- interprets voluntary return as more meaningful than verbal reassurance;
- under embarrassment, speech fragments while private thought stays precise;
- protects control over the situation before protecting social comfort.

For every central trait, try to expose at least one of:
- what it makes the character notice;
- how it changes interpretation;
- how it changes priority;
- how it changes action;
- how it changes voice.

Do not manufacture mechanisms for decorative traits.

## 4. Build APD first

APD must make the person independently legible before scenario mechanics are added.

A good APD should survive replacement of the current scenario. If removing the current plot makes the personality collapse, too much story logic leaked into Character.

For Light cards, prefer a few semantic blocks over a field-by-field personality form. Attention, interpretation, and decision may share one block when they form one clear causal chain. Ordinary life may live beside the character kernel when it needs no separate control logic. A Reaction Library is optional; add examples only when they teach behavior that the generator itself does not already make clear.

## 5. Build ED second

ED is not a summary of APD. It is the operating layer.

Start from the smallest runtime that can preserve player authorship, knowledge boundaries, meaningful change, continuity, and the character's actual failure risks. Add gates, trackers, beat logic, interaction controls, or detailed expression rules only when the premise needs them.

Use readable natural language, tables, compact conditions, or short process lines. Avoid turning the card into fake executable code unless the target platform actually requires it.

### Knowledge scope
Use categories such as:
- Known
- Observable
- Inferred
- Hidden
- Forbidden Knowledge

The exact labels may change. The distinction must not.

### Runtime state
Prefer discrete state and latches:
- Unknown / Suspected / Confirmed
- Closed / Open / Released
- Inactive / Active / Resolved
- No / Yes

Use numeric trackers only when the fiction genuinely depends on counting or thresholds. Otherwise prefer latches, discrete states, or coarse bands. Track consequences, not personality itself: an established event supplies evidence, the character interprets it, a choice or consequence follows, and only then does runtime state update. A changed score or label must never become its own motive.

### Gate engine
A gate answers: **Is this now legally available to the simulation?**

Opening a gate does not cause the event. It adds the event, revelation, action, or relationship move to the candidate space.

For gates that unlock materially stronger actions toward the player, alter what the character may impose on the player's body or choices, or change the relationship structure, inspect whether the gate can open solely because the model narrates a private realization. That may be intentional for some premises, but it should be an explicit design choice rather than an unnoticed self-authorization loop.

### Beat engine
A strong default flow is:

Condition -> Opportunity -> Interpretation -> Decision -> Event -> Consequence -> Update

The Interpretation step is essential. Input should not jump directly to event unless the premise defines a deterministic external mechanism.

### Anti-drift
Prefer concrete wrong-attractor analysis over vague bans. For high-risk failures, use:

Wrong Attractor -> Why It Is Wrong -> Correct Alternative -> Legal Transition Condition

A shorter `NEVER X / INSTEAD Y` pair is enough when no future legal transition matters.

Example pattern:
- Never turn vulnerability into generic therapist language.
- Instead answer through the character's own value system, agenda, humor, avoidance, control style, or relationship stance.

### Recovery
Use:

1. Detect - notice the previous turn drifted in voice, behavior, relationship, knowledge, gate, or timing.
2. Classify - identify the kind of error.
3. Preserve - keep observable events that already happened when possible.
4. Reframe - reinterpret the event through the real character logic rather than promoting the mistake into new canon.
5. Reassert - show at least one core motive, attention pattern, decision habit, voice feature, or relationship stance on the next turn.

Retcon only when the error cannot be repaired coherently.

## 5.5. Design-time simulation when behavior is still uncertain

If the rebuilt Character + Runtime rules still do not predict a high-value situation confidently, run a few disposable probes using `state -> knowledge -> perception -> interpretation -> priority -> decision -> expression`. Extract only the recurring generator, gate, response shape, or wrong-attractor rule. Do not ship the rehearsal prose by default. See `design-time-simulation.md`.

## 6. Build Scenario third

Scenario should answer "what is true now," not "what must happen later." Keep it proportional to the actual story engine. A domestic or low-plot premise may need only premise, entry relationship, active pressures, important knowledge asymmetry, continuity anchors, and the exact opening. Do not invent gates or beat catalogs just to make Scenario look complete.

Separate:
- established facts;
- hidden facts;
- knowledge distribution;
- gates;
- beat candidates;
- long-term attractors.

Do not use a day-by-day plot track unless calendar timing is itself part of the premise.

## 7. Derive Intro and Greeting

Intro advertises the playable tension without dumping runtime machinery. In the default five-file format, keep Intro at or below 2000 characters. If an interaction control such as a safeword is enabled, Intro may state it as an OOC/player-facing backdoor, but the ED must also contain the literal trigger and complete operative behavior. Intro disclosure never replaces ED authority.

Greeting must be derivable from:
- the character's current judgment;
- the runtime's knowledge limits and authorship rules;
- the exact scenario opening.

Greeting has no default 2000-character cap. Do not force a safeword or other interaction control into the Greeting, dialogue, narration, or inner thought merely because the player-facing Intro mentions it.

If Greeting contains a player thought, motive, consent state, or prior decision that exists nowhere in established canon, remove it.

## 8. Structural-delta requirement

A full rebuild must create a visible difference in architecture.

It is not enough to:
- split long prose into headings;
- rename "personality" to "character kernel";
- move paragraphs between APD and ED without exposing decision logic;
- add a generic anti-drift list;
- add a tracker that merely restates emotion.

A successful rebuild should make the execution questions that actually matter to this card answerable. Common examples include:
- what the character notices;
- how they interpret;
- why they choose;
- what they know;
- what evidence changes an important relationship;
- what must persist;
- which actions or revelations are genuinely gated, if any;
- which local beats need explicit conditions, if any;
- how likely drift can be corrected after it has already happened.

Do not add a mechanism merely so every question on this list has an answer. If the premise has no real gate or beat system, absence is the correct architecture. If the answers that do matter are not clearer after the rebuild, keep revising before delivery.
