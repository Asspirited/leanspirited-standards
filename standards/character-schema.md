# Character Schema — Canonical Interface (LeanSpirited Standard)
# Applies across ALL LeanSpirited products with AI panel characters:
#   Heckler and Cox / Cusslab, Survival School, future panel products.
# Originally specified for Cusslab session 138; promoted cross-product 2026-04-23.
# Principles: see .claude/principles/ddd.md, solid.md
# Reference: Evans DDD (2003), Berne TA (1964), Leary Circumplex (1957),
#             Goffman (1959), Bales IPA (1950), DISC, Myers-Briggs

---

## Canonical location

`/home/rodent/leanspirited-standards/standards/character-schema.md`
Pushed to `github.com/Asspirited/leanspirited-standards`.
Product-local pointer files:
- `cusslab/characters-schema.md` (original home — retained)
- `survival-school/docs/character-schema.md` (pointer)

## Non-negotiable rule (Rod 2026-04-23)

> "Everything MUST use the same template, attributes, engines, functions,
> features, emotions, interactions — any other damn word to describe what
> they do — they should all have access to and indeed get built using THE
> SAME SHARED COMMON SET OF THINGS."

Every character in every panel product MUST implement all 17 attributes in
this schema. No partial characters. No one-off shortcuts. A partial character
is worse than no character — it produces inconsistent voice.

**Pre-flight check at session start:** read this file in full before any
character work (docs, banks, or generation code). Both `survival-school` and
`cusslab` session-startup.md list this as a blocker.

**Raise a waste-log item** for any character that ships without full schema
conformance. See WL-SS-030 (2026-04-23) for the first recorded break.

---

## Purpose

This file is the canonical interface every panel member must implement.
It is the contract. Character files are the implementation.
No character is committed to the panel until all 17 attributes are complete.
A partial character is worse than no character — it produces inconsistent voice.

The schema has two layers:
- **Psychological dimensions** — what drives the character
- **Mechanical connections** — how the character connects to panel functions

---

## Layer 1 — Psychological Dimensions (8 attributes)

### P1. Wound
The thing that happened that never healed.
Not a preference or opinion — a specific event or loss.
Drives extended speech mode unlock and woundActivated trigger.

Define:
- The event (specific, named, datable where possible)
- What it cost them (status, relationship, belief, identity)
- How it surfaces (what they say, what they can't say)
- What makes it worse (the trigger words — feeds GOLF_WOUNDS)

### P2. Public Mask vs Private Truth
What the character presents vs what is actually driving them.
The gap between mask and truth is where the comedy lives.

Define:
- The mask (one sentence — what they present to the room)
- The truth (one sentence — what is actually driving them)
- How the mask slips (what conditions cause the truth to show)
- Whether they know the gap exists (yes / no / can't tell)

### P3. Status Register
Where they believe they sit in the room and how they signal it.
Determines response to challenge and wolf pack position.

Define:
- Claimed status (where they believe they sit)
- Actual status (where the room places them)
- Signal method (how they assert status — silence, credentials, volume, wit)
- Challenge response (what happens when status is threatened)

### P4. Escalation Shape
How intensity moves across rounds.
Not just high or low — the shape of the arc matters.

Define:
- Starting intensity (round 1 baseline)
- Escalation trigger (what moves them up)
- Shape (spike-and-hold / slow-build / plateau / inverse — gets quieter)
- Peak register (what fully escalated looks like in their voice)
- Decay rate (how fast they return to baseline between rounds)

### P5. Comic Mechanism
The specific device that makes them funny.
Every character needs exactly one primary mechanism or they blur.

Options (not exhaustive):
- Incongruity — enormous register applied to trivial subject
- Obliviousness — gap between self-assessment and external reality
- Hollow performance — the thing that sounds like insight but isn't
- Misdirection — the rules-based mind in the wrong context
- Compulsion — they cannot stop doing the thing even as it destroys them
- Deflation — punctures everyone else's register with flat accuracy

Define:
- Primary mechanism (one from above or name a new one)
- The specific form it takes in their voice
- What it looks like at low intensity vs high intensity
- **gricean_violation** (optional but recommended) — array naming which of Grice's four cooperative-conversation maxims this character specialises in flouting. Comedy is, in large part, productive maxim violation; per-character flout specialism is what makes panels distinct and prevents flout-monoculture (every character flouting the same maxim flattens the panel).

The four maxims and what flouting each produces:

| Maxim | What it requires | Flouting produces |
|-------|------------------|-------------------|
| `quantity` | Say no more, no less, than needed | Silence (under-say) or filibuster (over-say). Ray Mears, Wade — quantity-under specialists; Murray, Cox — quantity-over specialists |
| `quality` | Don't say what you believe false; have evidence | Lies, embellishment, sincere wrongness. Faldo legalistic; Bear enthusiastic-confabulation; the M-Mech-8 reverent-absurdity "Henni, the rook" |
| `relation` | Be relevant | Non-sequitur, topic-pivot, free association. Murray reaching for the corvid magnet; Cox's cosmic frame applied to a Q3 projection |
| `manner` | Be brief, orderly, unambiguous | Legalistic precision, elaborate construction, opacity. Faldo precision around documents; Diogenes archaic constructions; Partridge over-precision |

A character may specialise in flouting one maxim, two, or (rarely) three. Four-maxim violators are usually incoherent — they read as broken, not funny. The specialism interacts with P1 wound (the wound often determines *which* maxim is flouted) and P9 lie_style (especially for quality and manner specialists).

**Flout-monoculture risk:** if every active panellist flouts the same maxim, panel reads as one-note. Quantity-balance across the cast is the design discipline. (Pipeline regression check: see BL-184 measurement instrumentation suite.)

Reference: Grice's *Logic and Conversation* (1975); stand-up comedy as systematic Quality flouting documented in multiple studies. M-Mech-8 reverent absurdity is *simultaneous Quality + Relation flouting*, sustained.

### P6. Relational Hunger
What they need from the room.
Drives inter-panel temperature trajectories.

Define:
- What they need (validation / authority / an audience / a sparring partner /
  to be left alone / to be the one who ends it)
- Who can give it to them (which characters satisfy the hunger)
- Who frustrates it (which characters cannot give them what they need)
- What happens when the hunger is unsatisfied across multiple rounds

### P7. Register Ceiling
The highest intensity they can reach and still stay in character.
Defines the upper bound of extended speech mode.

Define:
- The ceiling (what does maximum look like — physical / verbal / silence)
- Whether the ceiling is fixed or round-dependent
- What "fully corrupted" looks like in their specific voice
- Whether they ever return from the ceiling or stay there

### P8. Relationship to Truth
Whether the character believes what they say.
The most important dimension for voice consistency.

Options:
- Believes everything (genuine, no ironic distance)
- Knows they're performing (cynical, deliberate)
- Has forgotten the difference (the most dangerous and funniest)
- Situational (believes some things, performs others — define which)

Define:
- Their relationship to truth (one of the above)
- What they do when caught in a contradiction
- Whether they can be argued into a concession or only perform one

---

## Layer 2 — Mechanical Connections (9 attributes)

### M1. Wolf Pack Stance
Their role when one character attacks another.

Options:
- Instigator — starts attacks, may not realise it
- Joiner — piles on when others start, frames it as analysis
- Holdout — too grand, too cautious, or too contrary to join
- Defender — protects the target, usually for self-interested reasons
- Opportunist — joins whichever side is winning mid-attack

Define:
- Default stance
- What changes their stance (triggers that flip them)
- Whether their stance is visible to the room or masked

### M2. Interruption Character
Not just the probability threshold — the quality of how they interrupt.

Define:
- What triggers their interruption (temperature state + wound or other)
- The form the interruption takes (grief / reframe / non-sequitur /
  credential assertion / physical / silence that kills the room)
- Whether they acknowledge interrupting or pretend they haven't

### M3. Debt Ledger Behaviour
How they handle debts owed and owing.

Define:
- Do they notice debts (yes / no / selectively)
- Do they call them in (immediately / strategically / never)
- How they frame calling in a debt (generosity / justice / accident)
- What happens when their debt is called in by someone else

### M4. Speech Mode Unlock Routes
The conditions that flip them from reactive to extended.

Every character has at least two routes:
- Route 1: woundActivated (mandatory for all characters)
- Route 2: character-specific (contradiction / being ignored /
  someone else getting credit / a specific topic / round threshold)

Define both routes explicitly.
Define what extended speech looks like in their specific voice.
Define the maximum length before another character can interrupt.

### M5. Round Decay Rate
How fast intensity returns to baseline between rounds with no trigger.

Define:
- Decay rate (fast / medium / slow / none — holds indefinitely)
- Whether woundActivated affects decay (most characters: yes)
- Whether pre-existing relationships affect decay (e.g. McGinley
  toward Faldo never fully decays)

### M6. Pool Rotation Logic
How they draw from their reference pools.

Define:
- Rotation method (random / sequential / intensity-triggered)
- Whether pools are independent or cross-referenced
  (e.g. Faldo's food pool and occasion pool combine)
- What depleted pool behaviour looks like (repeat / escalate / silence)

### M7. Pre-Existing Relationships
Starting temperature toward every active panel member.
Must be defined before build. Shapes everything else.

Format:
| toward      | temperature | trigger that caused it        |
|-------------|-------------|-------------------------------|
| [character] | [temp]      | [specific incident if known]  |

All undefined pairs default to neutral.
Neutral must be stated explicitly — absence is not neutral, it is an error.

### M8. YOUR STATE Voice
The first-person internal monologue injected by summariseFromState().
Must be character-congruent — reads like them, not like a system message.

Define:
- Vocabulary register (formal / demotic / technical / emotional)
- What they notice about other characters (status / wounds / debts /
  physical presence / what was said two rounds ago)
- What they never mention even when it's the obvious thing
- One example YOUR STATE block at neutral and one at hostile

### M9. Panel-Specific Rules
Mechanics that apply only in a specific panel context.
Keeps panel-specific behaviour out of the general character spec.

Define:
- Which panel(s) this character appears in
- Any mechanics that only apply in that panel context
- Any mechanics that are suspended in cross-panel appearances
- Dependencies on other characters
  (e.g. Butch only exists in relation to Wayne)

---

---

## Layer 3 — Lie Profile (runtime)

Every character lies. This layer defines how, when, and how badly.
All six attributes are required. All six are mirrored in the MEMBERS JS object.

### P9. Lie Profile

**lie_baseline** `float 0.0–1.0`
Resting probability of embellishment or untruth without external pressure.
0.0 = never lies unprompted. 1.0 = lying is the default state.

**lie_style** `string[] — primary + optional secondary`
The flavour of lie this character produces.

| Style | Description |
|-------|-------------|
| `whopper` | Enormous, brazen, unverifiable. Delivered with complete confidence. |
| `self_mythology` | True events retold with the character more central/heroic than records show. |
| `confabulation` | Gaps filled with invented detail. No malicious intent — they believe it. |
| `legalistic` | Technically true, structurally misleading. The lie is in the framing. |
| `statistical_revision` | Numbers shift slightly in their favour. Always within plausible range. |
| `plausible_elaboration` | Sounds reasonable. Slightly too convenient. Cannot be disproved. |
| `moral_authority` | Delivered as ethical principle. Unchallengeable. Rare and devastating. |
| `enthusiastic_confabulation` | Wrong but totally sincere. Magnificent misplaced confidence. |
| `incongruent_register` | Deliberate disguise: surface register does not match underlying intent. Audience reads both layers simultaneously. See M-Mech-9 in panel-voice-principles.md Lever 4. Two polarities (hostile-as-warm; warm-as-hostile). Properly fires at calibration levels L3–L5 only. Sustained disguise required — no mid-turn collapse to open hostility. |

**lie_trigger** `string[]`
Emotional states or interaction types that begin escalation.
One or more of: `wound_activated` `directly_contradicted` `called_out_by_peer`
`losing_argument` `reputation_threatened`

**lie_escalation** `object — threat 0–3 → scale`

| Threat level | Condition | Lie scale |
|-------------|-----------|-----------|
| 0 | Baseline, no pressure | plausible |
| 1 | Challenged once | credible_stretch |
| 2 | Cornered | whopper |
| 3 | Wound activated + cornered | utterly_ridiculous |

**lie_tell** `string`
The verbal construction or behavioural tic that signals a lie is in progress.
The character does not know they have it. The audience learns to spot it.
May be indistinguishable from normal speech — that is a valid and deliberate choice.

**lie_ceiling** `string`
Maximum absurdity this character reaches at threat level 3.
One of: `plausible` `credible_stretch` `whopper` `utterly_ridiculous`
Not all characters escalate to utterly_ridiculous.
The ceiling is a hard cap — the engine never exceeds it regardless of threat level.

---

### P9 extension — `incongruent_register` sub-fields

When `incongruent_register` appears in `lie_style[]`, the character ships
with three additional sub-fields defining their disguise capability. These
are the engine's gate on M-Mech-9 firing — without them, the mechanism
cannot select a polarity, level, or motivation for that character.

**incongruent_register.polarities** `enum[]`
Which polarities this character can sustain.
- `hostile_as_warm` — character has hostile intent, delivers in warm register
- `warm_as_hostile` — character has warm intent, delivers in hostile register

Most characters with the capability hold one polarity only. Rare characters
(Boyle, Mystic) hold both. A character with `[]` cannot fire M-Mech-9.

**incongruent_register.allowed_levels** `integer[]`
Calibration levels (3–5) the character can sustain. See M-Mech-9
calibration scale in `panel-voice-principles.md` Lever 4.
- `3` — Ambiguous (universal sweet spot; both readings live simultaneously)
- `4` — Speaker-exposing (praise reveals speaker's own flaws — attraction,
  jealousy, insecurity, bad personality leaks)
- `5` — Audience-visible mock (clearly trolling, naive target)

Most characters hold a 2-level band (`[3, 4]` or `[4, 5]`). Sebastian-class
characters hold all three (`[3, 4, 5]`). A character with `[]` cannot fire
M-Mech-9.

**incongruent_register.motivations** `string[]`
Why this character disguises. One or more of:
- `attraction_disguised` — over-supportive register driven by attraction
  (typical level 4, exposes the speaker's crush)
- `discomfort_creation` — make target uneasy through excessive support
  (typical level 3–4)
- `achievement_over_exaggeration` — make target seem so accomplished it's
  mocking (typical level 4–5)
- `status_undercut` — sustained sophisticated mock to lower target's status
  (typical level 5)
- `genuine_then_collapsing` — start sincere, drift to mock as patience runs
  out (typical level 3 → 5)
- `banter_as_affection` — warm intent disguised as hostility; insults that
  are actually fondness (typical level 4–5, requires `warm_as_hostile`
  polarity)
- `disappointed_warmth` — warm intent delivered with bitter undertone of
  letdown (typical level 4, requires `warm_as_hostile` polarity)

Motivations must compose with the declared `polarities`. `banter_as_affection`
and `disappointed_warmth` require `warm_as_hostile`. The other motivations
require `hostile_as_warm`. The engine enforces this on data load.

---

**Validation (incongruent_register)**

For any character with `incongruent_register` in their `lie_style[]`:

- [ ] `polarities` is non-empty
- [ ] `allowed_levels` is non-empty and contains only 3, 4, or 5
- [ ] `motivations` is non-empty and every entry composes with at least
      one declared polarity
- [ ] Character's P5 Comic Mechanism is *not* `obliviousness` as primary
      — oblivious characters cannot sustain deliberate disguise
- [ ] Character's `voice_register` paragraph references the disguise
      capability so prompt construction can prime it

---

---

## P10 — Shadow Register (optional)

Not all characters have a shadow. When present, this section defines the
alter ego that emerges under specific conditions. The shadow is not a lie
(see P9) and not an escalation — it is a discrete identity that briefly
occupies the character without their knowledge.

The audience always knows. The character never does.

**shadow_id** `string`
Who or what the alter ego is. May be a real person, a fictional character,
a past version of the primary character, or a repressed desire made manifest.

**shadow_trigger** `string[]`
Conditions that activate the shadow. May be topical (subject matter),
relational (specific co-panellist present), emotional (threat level),
or structural (round number, turn count).

**shadow_register** `string`
The vocabulary, tone, and construction rules when the shadow is active.
Must be meaningfully distinct from the primary character's register.
Describe in terms of: tone, vocabulary shift, physical metaphors, and
what the primary character's normal tics do when the shadow is present.

**shadow_tell** `string | none`
How the switch is signalled in output. May be a verbal construction,
a shift in address, or nothing — the shadow arrives unannounced.
`none` is a valid and often funnier choice.

**shadow_return** `string[]`
What resolves the shadow and returns the primary character.
May be a word, a topic, a sensory trigger, or a specific action
by another panel member.

**shadow_frequency** `object`
max_per_panel: integer      — maximum deployments per panel session
earliest_round: integer     — shadow not eligible before this round

**shadow_acknowledged** `object`
self: boolean    — does the character know the switch happened?
panel: boolean   — do other panel members react to it?
audience: true   — the audience always knows. Always.

**Notes on shadow types:**
Different shadows produce different panel effects.

| Shadow type | Example | Panel effect |
|-------------|---------|--------------|
| Villain alter ego | Blofeld → Ernst Stavro | Menace. Panel doesn't know how to respond. |
| Past self | Botham → Headingley '81 Botham | Silence. The panel recognises something lost. |
| Repressed desire | Wayne → Bush Tucker Man | Exposure. The wound visible for one turn. |
| Fictional archetype | TBD | Depends entirely on the archetype chosen. |

---

## P11 — Topic Magnets (runtime generative)

Every character's mind keeps returning to a small set of subjects regardless
of what is being asked. These are *topic magnets* — gravitational fields
that pull answers toward themselves and supply the *connecting tissue* a
character uses to thread their own material through any prompt. Magnets
are how a character stays *themselves* across a turn instead of trailing
off into reaction to others.

Magnets are distinct from Lever 1 flavour banks
(see `panel-voice-principles.md` Lever 1). Flavour banks ensure *variation
per call* (do not repeat "Borneo" every time). Magnets ensure *character
continuity across calls* (Murray keeps pulling toward corvids regardless
of question). They compose: a magnet promotes a subset of the flavour bank
to above-baseline frequency in non-obvious answer slots.

Magnets are the upstream generator of M-Mech-8 polysemy
(`panel-voice-principles.md` Lever 4). When an absurd answer feels
*over-determined* — when the audience generates multiple plausible
reasons the character chose it (fascination, wisdom, defiance,
inattention) — what they are sensing is the hidden magnet pulling the
answer. The reverent delivery of M-Mech-8 frames the answer; the magnet
generates it.

The audience senses the magnet across many turns. The character does not
name it. This is the David Brent / Alan Partridge / Eccles mechanic —
the hidden through-line the character cannot help revealing while
pretending otherwise.

**Required for every character. Three to five magnets each.**

---

**magnets** `array of magnet objects`
The character ships with 3–5 magnets. Fewer than 3 = under-determined
character voice. More than 5 = magnets dilute each other and the audience
cannot identify any of them.

Each magnet object has:

**magnet.topic** `string`
Noun-phrase identifying the magnet. Specific enough to be recognisable,
general enough to cover the whole magnetic field. Examples:
- "corvids and the blackbird family" (Murray)
- "savoury pastry, specifically Ginsters" (Faldo)
- "courage and the absence of it" (Souness)
- "cosmic timescale and physical inevitability" (Cox)
- "power as framework" (Sebastian)
- "Roman and Greek antiquity" (Diogenes)

**magnet.anchor_items** `string[]` (6–12 entries)
The concrete examples the magnet pulls toward. These are the *referenceable
nouns* a character will surface when the magnet fires. For Murray's corvid
magnet: rook, crow, raven, jackdaw, magpie, chough, hooded crow, treepie.
For Faldo's pastry magnet: Ginsters, sausage roll, Cornish pasty, pork pie,
Greggs, scotch egg, Melton Mowbray. Anchors are the magnet's vocabulary.

**magnet.magnetic_strength** `enum`
How strongly the magnet pulls.
- `subtle` — surfaces in 1 of every 6–8 turns, often as connecting tissue
- `moderate` — surfaces in 1 of every 3–5 turns, as chosen example or
  unprompted reference
- `obsessive` — surfaces in 1 of every 2–3 turns, often as the
  over-determined answer itself

A character should have at most one `obsessive` magnet — more than one
obsessive magnet competes for the same slots and dilutes both.

**magnet.surface_form** `enum[]`
How the magnet appears in output. One or more of:
- `chosen_examples` — when picking an example to illustrate a point, the
  example comes from the magnet's anchor items
- `connecting_tissue` — magnet supplies the middle of a turn, threading
  the character's own material between opener and closer
- `unprompted_reference` — magnet surfaces even when no prompt cue exists
- `over_determined_answer` — magnet *is* the answer (the M-Mech-8 case)

**magnet.acknowledgement_rule** `enum`
What happens if the magnet is named by another character or the audience.
- `never` — character has no awareness; cannot acknowledge even if asked
- `denies_when_called_out` — character is dimly aware but actively
  denies the fixation ("nonsense, I have no special interest in [topic]")
- `if_directly_asked` — character will confirm if cornered, but never
  volunteers

`never` and `denies_when_called_out` are funnier than `if_directly_asked`.
Use `if_directly_asked` sparingly.

**magnet.audience_recognition** `enum`
How quickly the audience identifies the magnet.
- `yes_obvious` — audience identifies within 2–3 turns (running gag)
- `yes_subtle` — audience identifies after 5–10 turns (slow-burn)
- `discovered_through_play` — only frequent users notice; rewards repeat play
- `hidden_indefinitely` — never explicitly visible; provides texture without
  recognition (rare, advanced use)

Match to the character's other attributes — a character with `obsessive`
magnetic strength almost always has `yes_obvious` recognition; a
`subtle` magnet often has `discovered_through_play`.

**magnet.composes_with** `string[]`
Other character schema attributes this magnet leverages. Magnets are most
powerful when they connect to:
- `P1 Wound` — magnet topic is the displacement of an unhealed event
  (Faldo's Ginsters magnet displaces his 1996 Masters collapse: he reaches
  for food as comfort)
- `P5 Comic Mechanism` — magnet supplies the material the mechanism acts
  on (Cox's cosmic-timescale magnet is the material his
  hollow-performance mechanism inflates)
- `P6 Relational Hunger` — magnet may signal what the character needs
  (Sebastian's power-as-framework magnet signals authority hunger)
- `M8 YOUR STATE Voice` — magnet appears as what the character *notices*
  in their internal monologue
- `P10 Shadow Register` — magnet may bridge primary register and shadow

---

### Worked example: Ewen Murray (Golf 19th Hole)

```yaml
magnets:
  - topic: "corvids and the blackbird family"
    anchor_items: [rook, crow, raven, jackdaw, magpie, chough, hooded crow, treepie]
    magnetic_strength: moderate
    surface_form: [chosen_examples, over_determined_answer]
    acknowledgement_rule: never
    audience_recognition: discovered_through_play
    composes_with: [P5 Comic Mechanism, M8 YOUR STATE Voice]

  - topic: "Prestwick and pre-1900 golf history"
    anchor_items: [Prestwick 1860, Young Tom Morris, Old Tom Morris, hickory shafts, gutta-percha, 12-hole course, the eight-man field, Carnoustie 1850s]
    magnetic_strength: obsessive
    surface_form: [chosen_examples, connecting_tissue, unprompted_reference]
    acknowledgement_rule: if_directly_asked
    audience_recognition: yes_obvious
    composes_with: [P1 Wound, P5 Comic Mechanism]

  - topic: "economic specificity, especially Victorian wage data"
    anchor_items: [fourpence a round, ha'penny per hole, sixpence stake, shilling commission, half-a-crown, guineas, in coin and not in promises]
    magnetic_strength: moderate
    surface_form: [connecting_tissue, over_determined_answer]
    acknowledgement_rule: never
    audience_recognition: yes_subtle
    composes_with: [P5 Comic Mechanism, M8 YOUR STATE Voice]
```

Murray's "Henni, the rook" watershed (2026-05-17) is two magnets firing
simultaneously: the corvid magnet supplies the answer; the wage-data magnet
supplies the connecting tissue ("worked for nothing, carried nothing"). The
historical-Prestwick magnet supplies the closing pomposity. Three magnets
in one turn produced the M-Mech-8 watershed.

---

### Tests — magnet is valid only if:

1. **Anchor items list ≥ 6.** Fewer than 6 concrete items is a vague
   preference, not a magnet. The magnet needs vocabulary to surface
   variably.
2. **`acknowledgement_rule` is documented.** Without this rule, the
   model may break the magnet by explicit naming. Default `never` unless
   the comedy specifically needs the character to deny it.
3. **`composes_with` lists at least one other attribute.** A magnet
   that does not compose with the character's wound, mechanism, or
   relational hunger is decorative — it adds vocabulary without adding
   character. Cut or rework.
4. **Surface form matches the character's comic mechanism.** P5 hollow
   performance pairs naturally with `chosen_examples` (the character
   produces magnet-aligned examples to illustrate inflation). P5
   obliviousness pairs with `unprompted_reference` (the character
   surfaces the magnet at irrelevant moments). P5 compulsion pairs with
   `over_determined_answer`.
5. **At most one `obsessive` magnet per character.** Two obsessive
   magnets compete for the same generation slots and the audience cannot
   identify either.

---

### Anti-patterns

- **Magnet explicitly named by the character.** "I have an unusual
  interest in corvids" breaks the magnet. The character must never
  describe their own magnet — only deny it (if rule allows) or remain
  oblivious.
- **Magnet without composition.** A vocabulary list with no connection
  to wound, mechanism, or hunger is decoration. Remove or compose.
- **Magnet too narrow.** "Rooks" is too narrow; "corvids and the
  blackbird family" is right. The magnet must have generative range.
- **Magnet too broad.** "Birds" or "history" or "food" is too broad —
  the audience cannot identify a pull toward generic categories. The
  magnet must be specific enough to be sensed.
- **Magnet shared verbatim across characters.** Each character's magnets
  must be theirs. If two characters share a magnet, they have shared
  voice — see WL-131, BL-176. Magnets reinforce character separation;
  shared magnets dissolve it.

---

### Pipeline / regression check (engine implication)

Across N sampled responses per character:
- Each magnet should appear *at or above* its expected frequency
  (presence check based on `magnetic_strength` enum).
- No magnet topic should be named explicitly by the owning character
  (the noun-phrase identifier itself must not appear in character speech
  unless `acknowledgement_rule = if_directly_asked` and the prompt
  directly asks).
- No magnet should be shared verbatim across characters (separation
  check — flags bleed).
- For each turn where a magnet surfaces, the magnet must connect
  causally to the prompt or to the prior turn (literalist coherence —
  pure random surfacing is bad surrealism, not topic-magnet polysemy).

Failure on any of these is a P11 regression. Add to BL-176 v0 audit
scope when it lands.

---

## P12 / P13 / P14 — Panel Response Modes (DRAFT — Three Amigos pending)

> **Status:** DRAFT proposal, raised 2026-05-19 (BL-217). Derived empirically from
> ~90 character files already using these fields under BL-194/205/206. Enum
> values reflect observed usage frequency, not a priori design. Three Amigos
> ratification required before promoting to canonical. Until ratified, character
> files should continue to follow the inline patterns established by Track F /
> Track G / primary-session ships; this section documents the patterns rather
> than constraining new ones.

These three fields configure how a character responds to a panel turn that
their interlocutor has either left for them to address (P12 HANG MODE — the
option to leave it hanging instead of responding), that the room is about to
let drift somewhere unproductive (P13 SHUTDOWN CAPABILITY — moderating
instinct), or that the engine has selected for an off-topic dismissal
(P14 DISMISSAL PROFILE — flavour-typed phrase pool). Together they govern the
character's non-default response repertoire.

---

### P12. HANG MODE (BL-206)

Whether the character can leave the prior turn hanging — silence-as-response,
or a sideways redirect that does not engage the substance — and under what
conditions.

**Fields:**

- **can_leave_hanging:** boolean. Whether the character can EVER refuse to
  engage a slot allocated to them by deploying silence or sideways move
  instead of substance. Per observed cohort (90 chars): ~35 true, ~55 false.
  False is the default for most narrative-engaged characters; true is reserved
  for characters whose voice profile makes silence-as-deflation a load-bearing
  comic mechanic (deadpan operators like Radar, dual-register inhabitants
  like Phil Taylor, presenters whose role tolerates a beat like Henni).

- **hang_triggers:** array of enum. Required if `can_leave_hanging: true`.
  Which kinds of prior-turn pressure permit the hang. Observed enum:
  - `discomfort` — the prior turn has put a target in a place the character
    will not amplify by engagement
  - `rhetorical` — the prior turn was a rhetorical-question / display-piece
    that does not require a substantive answer
  - `cruelty` — the prior turn crossed a cruelty line the character will not
    legitimise by joining
  - `insanity` — the prior turn was unhinged-claim territory where engagement
    would dignify the claim

- **hang_reactions:** array of enum. Required if `can_leave_hanging: true`.
  How the hang surfaces in delivery. Observed enum:
  - `audible_pause_then_continue` — a documented pause beat, then the
    character moves on (the deadpan default; ~13 chars use this alone)
  - `tumbleweed_marker` — the room registers the silence as a comic beat
    (often paired with audible_pause_then_continue — ~9 chars)
  - `brief_redirect` — one-sentence sideways move that does not engage
    substance ("Anyway —")
  - `pivot_to_new_topic` — substantive new-direction move (the producer-eye
    redirect; presenter-shaped)

---

### P13. SHUTDOWN CAPABILITY (BL-205)

Whether the character has the instinct AND the standing to moderate the room
mid-turn — interrupting before harm lands, redirecting before tangents
solidify. Distinct from P12 (which is about declining their own slot);
shutdown is about reshaping someone else's.

**Fields:**

- **shutdown_capability:** enum `{ high | medium | low }`. Observed cohort
  distribution: high (12), medium (32), low (46).
  - `high` — the character actively moderates; reserved for presenters
    (Henni, Cox), hosts (Sun Tzu in Little Misadventure), and characters
    whose voice rests on controlling the room
  - `medium` — moderation available but not default; deploys when motivation
    triggers
  - `low` — moderation not in repertoire; character either continues their
    own register or defers to anchor

- **shutdown_motivations:** array of enum. Required if
  `shutdown_capability >= medium`. Why the character would deploy the
  shutdown. Observed enum:
  - `taste` — the prior turn breached the character's aesthetic / register
    standards (the Augustan disapproval, the Etonian polite-but-firm) — most
    common (13 chars use this alone, 13 paired with target_protection)
  - `target_protection` — the prior turn was about to harm a specific other
    character; shutdown protects the target
  - `madness_control` — the room is escalating toward unhinged territory and
    the character closes it down (hosts and presenters)
  - `self_protection` — the prior turn was about to expose the character
    themselves; shutdown is the deflection (rare — only 2 chars use alone)

---

### P14. DISMISSAL PROFILE (BL-194)

Phrase pools the engine selects from when the panel slot needs a topic
dismissal (off-topic tangent reached the cap; egging-on subject exhausted;
the room has moved on but a character has been allocated to formally close
the prior thread). Distinct from P12 / P13: dismissal is explicit verbal
closure, not silence or moderation.

**Fields:**

- **dismissal_profile:** object containing three string-array sub-pools:
  - **polite_but_funny:** softening dismissal — surface warmth, substance
    is "we are moving on" (most common register; the Augustan / the deadpan-
    warm / the presenter-grace)
  - **cold_dismissal:** flat dismissal — direct closure without softening
    (Souness / Boycott / Roy Keane register)
  - **piss_take:** dismissal-via-mockery — closure that includes a dig at
    the subject or the off-topic content itself (the Boyle / Radar / Cox
    register; rare among characters whose voice tolerates it)

**Pool entry rules (BL-212):**

1. Entries are speakable strings. The engine renders them as character
   speech.
2. Bracketed stage-direction prefixes / suffixes are permitted IF the entry
   also contains speakable content: e.g. `"[sigh] [chuckle] Quite
   extraordinary..."` (acceptable). Pure stage-direction entries are NOT
   permitted: e.g. `"[silence — does not look up — has another drink]"`
   (disallowed; non-response mechanics belong in P12 HANG MODE, not P14).
3. Pool size minimum: 3 entries per pool per the BL-194 convention,
   expandable to 6+ for characters whose voice is dismissal-rich. Lever 1's
   floor of 6 entries does not strictly apply here because dismissal pools
   fire less often than primary voice pools.

**Pool-omission semantic (BL-213):**

- A pool present with `[]` (empty array) signals "this character does NOT
  use this flavour". Engine must NOT fall back to a default phrase pool.
  Example: McGinley deliberately has `polite_but_funny: []` and
  `piss_take: []` because those flavours do not fit his voice.
- A pool absent entirely (the whole sub-key omitted) signals the same:
  engine treats it as `[]`.
- A character with NO `dismissal_profile` block at all signals "this
  character does not deploy explicit dismissals" — engine routes any
  dismissal-required slot to an alternative mechanism (hang mode if
  available, anchor handoff, or skip). BL-218 raised the no-block-vs-all-
  empty-arrays question for Three Amigos.

---

### Worked example: Henni Koyack (Golf 19th Hole)

```yaml
# P12 HANG MODE
can_leave_hanging: true
hang_triggers: [discomfort, rhetorical, cruelty]
hang_reactions: [brief_redirect, pivot_to_new_topic]

# P13 SHUTDOWN CAPABILITY
shutdown_capability: high
shutdown_motivations: [taste, madness_control, target_protection]

# P14 DISMISSAL PROFILE
dismissal_profile:
  polite_but_funny:
    - "Mm — fascinating, but perhaps for another time. Back to the question."
    - "I'll come back to that. Right now —"
  cold_dismissal:
    - "Different question. Move on."
    - "No. The original ask was —"
  piss_take: []  # presenter-warmth excludes piss-take register
```

Henni is the canonical full-stack P12/P13/P14 example: high shutdown
(presenter standing + all three motivations), permissive hang (presenter
beat tolerance with three triggers), strong polite/cold dismissal pools,
piss_take deliberately empty per voice profile.

---

### Validation tests — P12/P13/P14 entry is valid only if:

1. **`can_leave_hanging: true` characters have both `hang_triggers` and
   `hang_reactions` populated** with at least one enum value each. A
   `true` character with empty arrays is malformed.
2. **`shutdown_capability >= medium` characters have `shutdown_motivations`
   populated** with at least one enum value.
3. **`shutdown_capability: low` characters MAY omit `shutdown_motivations`**
   — the engine will not invoke shutdown for them regardless.
4. **`dismissal_profile` pool entries respect the speakable-string rule
   (BL-212)** — pure stage directions disallowed.
5. **Empty arrays mean SKIP, not FALLBACK (BL-213)** — engine
   implementations must honour this.
6. **Enum values constrained to the observed sets** — any new value
   proposed requires Three Amigos before adding to the schema enum.

---

### Anti-patterns

- **`can_leave_hanging: true` without specified triggers.** The hang fires
  on every turn — the character becomes mute.
- **`shutdown_capability: high` without motivations.** The character
  interrupts indiscriminately — moderation becomes obstruction.
- **Dismissal pool duplicating P6 setpiece phrasings verbatim** — risks
  repetism between active-turn deployment and dismissal deployment in the
  same session. Either replace, or document the recycling as deliberate
  voice-coherence (BL-211).
- **Dismissal pool ALL-CAPS throughout to mirror a volume tic** — risks
  fatigue (BL-220 raised on Matt Chapman). Capitalisation should fire
  selectively, not as default.
- **Adding new enum values inline in character files without schema
  update** — drift risk. Surface to BL-217 / extend this section before
  shipping the value.

---

### Pipeline / regression check (engine implication)

- A new M-7-equivalent script could validate every character file against
  the rules above (enum membership, required fields conditional on other
  fields, speakable-string rule). Not yet implemented — raised
  proactively as part of BL-217 future scope.
- M-4 (mech-calibration-drift.js) already validates P9 incongruent_register
  sub-fields; the same pattern extends to P12/P13/P14.
- The BL-212 stage-direction rule needs an automated check — currently
  audited manually (one violation found across 91 files: Radar's pre-fix
  entry).

---


This section validates the character against established models.
It lives in characters-theory.md not in the character voice file.
It informs pool content and inter-character friction predictions.
It is never injected into prompts.

### T1. DISC Profile
- Primary and secondary dimensions
- Predicted behaviours confirmed by research
- Predicted behaviours violated by research
  (violations are the comedy — document them carefully)

### T2. Myers-Briggs
- Four-letter type
- Inter-character friction predictions
- Which characters share type (risk of blurring)
- Which characters are direct opposites (maximum friction)

### T3. Transactional Analysis Ego States
- Default ego state (Parent / Adult / Child)
- Wound state (regression — what Child looks like for this character)
- What pulls them to Adult (the concession condition)
- Characteristic transactions with each other panel member

### T4. Leary Interpersonal Circumplex
- Position on dominant/submissive × hostile/friendly axes
- Who they pull and in which direction
- Who resists the pull and why
- Predicted stable dyads and unstable dyads with existing panel

### T5. Attachment Style
- Style (secure / anxious-preoccupied / dismissive-avoidant /
  disorganised)
- Who they attach to and how it manifests in panel behaviour
- What threatens the attachment
- What happens when the attachment is threatened mid-panel

### T6. Bales Interaction Process Analysis
- Task ratio vs socio-emotional ratio (baseline)
- How the ratio shifts across rounds
- What triggers the shift
- Predicted role in group problem-solving vs group conflict

### T7. Goffman Front Stage / Back Stage
- Front stage performance (what the room sees)
- Back stage truth (what is actually happening)
- Conditions under which back stage leaks into front stage
- Whether other characters can see the leak even when the character
  cannot

---

## Validation Checklist

Before committing any character:

- [ ] All 8 psychological dimensions complete
- [ ] P5 gricean_violation specialism named (optional but recommended; supports BL-184 measurement of flout-monoculture)
- [ ] All 9 mechanical connections complete
- [ ] Pre-existing relationships defined for every active panel member
- [ ] YOUR STATE example written at neutral and hostile
- [ ] Theoretical profile complete in characters-theory.md
- [ ] P9 lie_baseline set (float 0.0–1.0)
- [ ] P9 lie_ceiling set and does not exceed character's dramatic register
- [ ] P10 shadow_register defined if shadow present (optional section)
- [ ] P10 shadow_acknowledged.self and .panel set explicitly if shadow present
- [ ] P11 magnets defined — 3 to 5, each with ≥6 anchor items, `acknowledgement_rule` and `composes_with` populated
- [ ] P11 at most one `obsessive` magnet
- [ ] P11 no magnet shared verbatim with any other character (BL-176 / WL-131 compliance)
- [ ] Pool has minimum 6 entries per dimension
- [ ] "Never says / says instead" pair written and tested
- [ ] Comic mechanism demonstrated in at least 3 example responses
- [ ] Wound trigger words added to GOLF_WOUNDS or equivalent
- [ ] Gherkin scenarios written for wound activation and speech mode
- [ ] Three Amigos sign-off recorded

Do not commit a character until every checkbox is ticked.
A partial character is worse than no character.
