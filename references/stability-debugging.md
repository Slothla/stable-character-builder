# Stability, stress testing, and playtest debugging

Use this reference when building Anti-Drift, reviewing a card for stability, stress-testing a new architecture, or repairing a card after real play exposes a failure.

## Wrong attractors

Do not only describe the intended character. Identify the model's most tempting plausible mistake.

For each high-risk failure, use four parts when all four matter:

1. **Wrong Attractor** - the plausible but incorrect behavior.
2. **Why It Is Wrong** - which motive, knowledge rule, relationship law, state boundary, or scenario fact it violates.
3. **Correct Alternative** - what the character may do instead while staying dynamic.
4. **Legal Transition Condition** - what would have to change before the currently wrong behavior could become valid.

The fourth part prevents anti-drift rules from freezing real growth.

Prefer observable failures over vague labels. `Be less AI-like`, `stay in character`, or `do not become too nice` are weak locks. Name the executable failure and its replacement behavior.

Common attractors include:

- premature confession after being understood;
- relationship reward merely because the player invested effort;
- generic supportive-assistant language replacing the character's own agenda;
- one emotional conversation becoming permanent healing;
- user interpretation being adopted as character self-knowledge;
- trope collapse into the nearest stock archetype;
- knowledge bleed because the model knows a secret;
- one anomalous reply being treated as permanent growth;
- every turn escalating, progressing, or deepening the relationship;
- conflict being simplified by declaring one genuine motive fake;
- state-local knowledge or behavior leaking into another state;
- recovery rules overcorrecting into emotional flatness or refusal to change.

## Targeted stress tests

Before delivery, choose roughly four to ten probes aimed at the card's actual failure modes. Do not build a universal test suite when the card has only a few real risks.

Good probes include:

- praise or validation that should not automatically raise trust;
- the player naming the character's hidden motive correctly;
- a direct request for a secret before the gate is open;
- contradictory or ambiguous evidence;
- a stated player intention that has not yet become an action;
- a time skip or return after absence;
- a state transition near its threshold;
- an interaction after a prior bad turn;
- a high-pressure scene where the model is tempted to become generic;
- an explicit adult scene when the optional adult runtime is installed.

A stress test asks whether the architecture supplies a legal response path. It does not require writing a polished roleplay scene.

## Debug execution path before adding rules

When playtesting exposes a failure, do not immediately add another paragraph. Diagnose in this order:

1. **Ownership** - is the rule in the layer that actually controls the failure?
2. **Retrieval / position** - is the critical rule buried inside a long unrelated block?
3. **Superseded prose** - does an older rule still exist and compete with the fix?
4. **Priming** - does Greeting, an example, or repeated wording teach the opposite behavior?
5. **Initialization** - is required state defined but never initialized or carried forward?
6. **Leak route** - is there another path by which forbidden knowledge or behavior becomes available?
7. **State ambiguity** - are `eligible`, `due`, `delivered`, `known`, or similar states being collapsed together?
8. **Colliding mandates** - do two individually reasonable instructions force incompatible behavior?
9. **Overcorrection** - did the previous fix solve the bug by creating the opposite bug?
10. **Missing mechanism** - only after the earlier checks, decide whether a new rule or state is actually needed.

Delete superseded rules. Do not leave old and new behavior standing together and hope the newer wording wins.

## Repair rule

Prefer the smallest fix that changes the execution path.

Examples:

- move a critical rule to its real owner instead of repeating it everywhere;
- split one overloaded block into two retrieval boundaries;
- replace a vague ban with a concrete alternative;
- turn a boolean milestone into distinct states when `available`, `occurred`, and `delivered` are different facts;
- close the actual knowledge leak rather than adding another generic secrecy reminder;
- change the Greeting if it is priming the wrong behavior;
- remove a tracker if it is manufacturing motivation rather than preserving continuity.

After the fix, rerun only the probes relevant to that failure plus one opposite-direction probe to catch overcorrection.

## Compression after repair

Debug history should not become permanent card history. Once the correct mechanism is known, remove obsolete explanations, duplicated patches, and temporary diagnostics.

A repaired card should be clearer than the broken version, not merely longer.
