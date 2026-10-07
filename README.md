[English](README.md) | [简体中文](README_ZH.md)

# Stable Character Builder

**Stable Character Builder** is a design, rebuilding, diagnostic, and stability tool for **single-protagonist RP character cards**.

Its goal is not merely to generate a longer or more polished profile. It treats a character as a **playable runtime**: a system that can consistently answer who the character is, how they interpret the player, why they make decisions, what they are allowed to know, what evidence changes a relationship, when story possibilities become available, and how the character can recover after model drift.

The Skill is designed to remain as **platform-neutral** as possible. It does not assume a specific RP platform, model, tracker implementation, or formatting system. Platform-specific features can be adapted when needed without making them the foundation of the character architecture.

## Installation

Download the latest **`skill.zip`** from the repository's [Releases](https://github.com/Slothla/stable-character-builder/releases/latest) page and install it as a ChatGPT Skill.

> Use the attached `skill.zip` from the Release assets. GitHub's automatically generated **Source code (zip)** is the repository source archive, not the packaged Skill installer.

## Quick Start

You do not need to understand the architecture or choose modules in advance.

You can simply:

- describe a character you want to build;
- provide an existing card for review or rebuilding;
- ask for a local edit to a specific field or mechanism;
- report a real playtest failure you want diagnosed;
- request a complete architecture rebuild;
- request another language, combined document, or platform-oriented output format.

Stable scales the architecture to the actual character problem, uses only structures that earn their space, and asks questions only when a missing choice would materially change the character, interaction logic, or delivery format.

## Supported Tasks

Stable can build a character from scratch or work on an existing card.

It supports discussion and diagnosis, local edits, structural rewrites, full architecture rebuilds, format conversion, and new character creation.

When rebuilding an existing character, it preserves established canon, identity, relationships, facts, and approved voice unless the user asks for changes. It does not preserve weak architecture merely because that architecture already exists.

A full rebuild aims to **preserve the person, not the old document layout**.

## Adaptive Architecture

Stable does not require every character to use the same machinery.

Before expanding a build, it assigns an architecture budget: **Light, Standard, or Runtime-heavy**.

Simple characters stay compact. More complex characters can gain persistent state, gates, trackers, knowledge systems, progression logic, or other runtime mechanisms only when those mechanisms have a real job.

Substantial optional modules must pass a simple admission test:

1. What real failure or capability does this solve?
2. What state or output does it read or write?
3. What important behavior would actually break if it were removed?

If nothing important would break, the mechanism probably does not belong in the card.

A full architecture rebuild may reorganize the whole card, but it does **not** mean installing every available mechanism. Adjacent functions may be merged, irrelevant functions stay absent, and longer cards should gain clearer semantic retrieval boundaries rather than simply more headings or prose.

## Character / Runtime / Scenario Architecture

Stable separates three different responsibilities.

**Character** answers: who is this person, and why do they choose what they choose?

It may contain the character kernel, true motive, self-model, ordinary life, attention model, interpretation biases, decision tendencies, voice, inner/outer gap, and relationship functions.

**Runtime** answers: how is this person turned into stable play?

It handles player authorship, knowledge scope, continuity, persistent state, trackers, gates, beats, relationship change, anti-drift, recovery, delivery guards, and execution rules.

**Scenario** answers: what is true in this story right now?

It contains the premise, current relationship, established facts, secrets and knowledge distribution, active pressure, open opportunities, story gates, beat candidates, long-term attractors, continuity anchors, and the exact opening state.

This prevents APD from becoming a rule dump, ED from becoming a second biography, or Scenario from quietly redefining the character.

## Executable Character Models

Stable does not stop at labels such as shy, intelligent, possessive, or confident.

It focuses on a causal chain:

**what the character notices → how they interpret it → what they prioritize → what they choose → how they express that choice**

This turns personality into behavior-generating logic rather than decorative description.

True motive and self-explanation may also be separated where useful. A character may understand themselves accurately or misunderstand their own motives, but the Skill does not manufacture hidden contradictions merely to make a character appear deeper.

## Ordinary Life Beyond the Player

Characters can have work, interests, responsibilities, routines, relationships, and stakes that exist independently of the player.

This helps prevent a common failure where a character gradually collapses into nothing but reactions to the player.

A well-built character should still make sense as a person even if the player is temporarily removed from the scene.

## Multidimensional Relationships

Stable does not assume that a single affection score can represent an entire relationship.

Relevant dimensions may include trust, liking, cooperation, disclosure, attraction, intimacy, rivalry, dependence, or other character-specific functions.

As a result:

**Attraction is not trust.  
Trust is not disclosure.  
Being understood is not automatic romantic reward.  
Sexual intimacy is not automatic relationship progression.**

Meaningful change requires relevant evidence that actually occurred.

## Player Authorship

The player's explicitly stated words and actions are authoritative.

The model should not invent unstated player thoughts, feelings, desires, consent, memories, history, decisions, or completed actions.

This includes a common failure where a player's stated intention is treated as an action that has already happened.

If the player says they plan to go somewhere later, the runtime does not silently move them there.

Player Authorship is treated as a core runtime responsibility, not an optional stylistic preference.

## Knowledge Scope and Information Asymmetry

Author knowledge is not automatically character knowledge.

Stable can distinguish states such as Known, Observable, Inferred, Hidden, and Forbidden, or use an equivalent structure suited to the card.

Characters may suspect, misread, discover, or confirm information, but changes in knowledge require actual evidence, witnessing, disclosure, or justified inference.

This is especially useful for secrets, mystery plots, hidden identities, slow-burn relationships, and asymmetric information.

## State, Trackers, and Continuity

Stable supports persistent state without assuming that everything should become a number.

The normal preference is:

**discrete state or latch → qualitative band → numeric tracker only when real counting or thresholds matter**

A state is worth tracking only when forgetting it several turns later would create a real continuity error, knowledge leak, repeated milestone, relationship jump, impossible combination, pacing failure, or gate mistake.

Trackers record consequences of established events. They should not manufacture character motivation.

Whenever possible, Stable stores causes and derives consequences rather than maintaining redundant independent values.

## Gates, Beats, and Long-Term Attractors

Stable separates three functions that are often mixed together.

A **Gate** determines what is now legally available to the simulation.

A **Beat** represents a possible next event under current conditions.

A **Long-Term Attractor** describes a direction the story may gradually move toward.

Opening a Gate does not force an event. A Beat is a candidate rather than a railway schedule. An Attractor is not a mandatory ending.

This allows structured long-form play without turning the story into a railroad.

## Anti-Drift

Stable identifies the character-specific failure modes most likely to flatten or distort the character.

Examples may include generic softness, premature confession, automatic player reward, archetype collapse, excessive agreeableness, or a trait being exaggerated until it replaces the rest of the person.

For important risks, Stable can use:

**Wrong Attractor → Why Wrong → Correct Alternative → Legal Transition Condition**

The last step matters because anti-drift rules should not permanently freeze a character.

If a behavior could become valid later through earned development, the card can define what evidence or state change makes that transition legitimate.

## Recovery Architecture

A single bad model response does not need to permanently redefine the character.

Stable uses:

**Detect → Classify → Preserve → Reframe → Reassert**

It identifies the failure, preserves observable events where possible, reinterprets unsupported meaning through the actual character logic, and reasserts core motive, judgment, voice, or relationship stance on the next turn.

This allows recovery from OOC behavior without casually rewriting history.

## Design-Time Simulation

When abstract rules still do not predict behavior confidently, Stable can run a small number of disposable design-time probes.

Typical probes may include ordinary interaction, refusal, being correctly understood, vulnerability, secret boundaries, a nearly-open gate, recovery after a bad turn, or an adult-intimacy probe when that module is enabled.

Each probe traces:

**state → knowledge → perception → interpretation → priority → decision → expression → consequence**

The rehearsal prose is disposable.

Only reusable causal rules, response shapes, gates, continuity latches, or anti-drift findings are retained.

Stable does not pretend to validate hundreds of unseen turns through imaginary long-run testing.

## Targeted Stress Testing

Before delivery, the architecture can be challenged with a small number of adversarial probes aimed at its actual risks.

Examples include premature confession, unsupported relationship reward, knowledge leakage, treating stated intentions as completed actions, opening a gate too early, continuity after a time skip, or recovery after an OOC turn.

The purpose is not to prove that a character can never fail.

It is to catch obvious architectural failures before delivery.

## Root-Cause Debugging

When real play exposes a problem, Stable prefers root-cause repair over adding another patch.

It checks ownership, retrieval and rule placement, stale or superseded instructions, priming from examples or Greeting text, initialization, alternate leak routes, state ambiguity, colliding mandates, and opposite-direction overcorrection before adding new machinery.

Once the problem is fixed, obsolete patches should be removed rather than accumulated indefinitely.

## Optional Explicit Adult Scene Runtime

For fictional adult characters intended for **detailed explicit sexual play**, Stable can enable an optional Explicit Adult Scene Runtime.

The module is not installed merely because a character is attractive, flirtatious, romantic, or sexually confident.

When explicit detailed play is clearly requested, the full module can be enabled directly. It does not introduce a separate explicitness ladder, anatomy slider, or long questionnaire.

When enabled, the default is direct, specific, anatomically clear, physically detailed adult rendering. Softer, more literary, less physiological, or fade-to-black styles can be requested later as normal revisions.

The module adds scene-stage pacing, physical choreography, body continuity, somatic response, pattern variation, climax and continuation logic, and adult-specific anti-drift checks.

It is designed to avoid both instant escalation from first contact to climax and the opposite failure of slowing the scene into one trivial micro-action per reply.

## Adult Intimacy Pattern Grammar

Explicit interaction is not treated as a fixed act list.

Stable uses a generative pattern grammar across dimensions such as initiation, control and reciprocity, body geometry, body focus, clothing and material state, rhythm, sensory emphasis, somatic response, verbal mode, intensity transitions, climax state, and aftermath.

These patterns are generative ingredients, not a closed whitelist.

Unlisted behavior remains possible when it follows naturally from the Character Model and does not violate an explicit exclusion, gate, control, authorship rule, or continuity fact.

The character remains the selector.

## Physical Choreography and Body Continuity

Detailed scenes can preserve relevant spatial facts such as orientation, distance, contact surfaces, limb placement, support points, weight distribution, environmental constraints, and clothing state.

Major position changes should be physically legible rather than functioning as scene teleportation.

This does not mean inventorying every joint in every reply. The runtime tracks only the geometry needed by the active movement.

## Somatic Response Grammar

Physical response is generated from the current stimulus, position, intensity, fatigue, relationship context, and the character's attempts to maintain or surrender control.

Possible dimensions include breathing, muscle tension, grip, posture, gaze, vocal response, skin response, localized sensitivity, and recovery state.

Physical response does not automatically establish consent, emotional agreement, or relationship progress.

## Climax and Continuation

Within the adult runtime:

**Climax is a state change, not an automatic END SCENE signal.**

A scene may continue, reduce intensity, change focus, pause for recovery, build again, move into character-specific aftermath, or end.

Stable does not impose universal rules requiring everyone to climax, requiring aftercare, requiring multiple climaxes, or treating climax as automatic confession, trust, healing, tenderness, or romantic progression.

## Interaction Controls

Safewords, stop commands, pause/resume systems, or comparable interaction controls can be added when requested or already canonical.

These controls are optional.

When a safeword or stop command is enabled:

- **ED contains the full operative rule**;
- Intro may repeat a concise player-facing notice;
- the control does not depend on the character having explained it in-character;
- Greeting and normal IC prose do not need to mention it unless the user explicitly wants that presentation.

Player-facing disclosure and runtime authority are kept separate so that an important control is not merely mentioned in Intro while remaining undefined in the actual runtime.

## Intro and Greeting

For a complete card, Intro and Greeting are derived from the Character, Runtime, and Scenario architecture rather than written as independent creative-writing exercises.

Intro presents the playable premise and attraction without automatically revealing gated information.

Greeting performs the exact opening state, expresses the character's judgment and immediate action or speech, and leaves genuine room for player response.

In the default five-file format, Intro is limited to **2000 characters**. Greeting has no default 2000-character cap unless a target platform requires one.

## Output Format

The default complete delivery is a five-file English set:

`01_APD.txt`  
`02_ED.txt`  
`03_Scenario.txt`  
`04_Intro.txt`  
`05_Greeting.txt`

The output can instead be delivered in another language, as one combined document, or adapted to another requested platform schema or format.

## How to Use It

The user does not need to understand the architecture or choose modules in advance.

They can describe a character concept, provide an existing card, report a real playtest failure, or request a complete rebuild.

Stable scales the architecture to the actual problem, installs only structures that earn their space, and asks questions only when a missing choice would materially change the character, interaction logic, or delivery format.

The goal is not to build the character card with the **most systems**.

The goal is to build the **smallest architecture that still behaves reliably in play**.


## Repository Structure

```text
stable-character-builder/
├── SKILL.md
├── README.md
├── README_ZH.md
├── LICENSE
├── agents/
│   └── openai.yaml
└── references/
    ├── adult-intimacy-patterns.md
    ├── adult-intimacy-runtime.md
    ├── architecture-rebuild.md
    ├── character-core.md
    ├── design-time-simulation.md
    ├── guided-start.md
    ├── optional-mechanisms.md
    ├── output-modes.md
    ├── stability-debugging.md
    └── user-guide.md
```

## Responsibility

Users are responsible for the character cards they create and how they use them.

## License

Licensed under **Creative Commons Attribution 4.0 International (CC BY 4.0)**.

## Author

Created by **sloth03**

- Discord: `@sloth_la`
- GitHub: [`@Slothla`](https://github.com/Slothla)
