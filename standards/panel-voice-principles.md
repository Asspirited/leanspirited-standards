# Panel Voice Principles — LeanSpirited Standard

How to build character panels that sound like the characters, not like the model.

Applies across all LeanSpirited panel products (Survival School,
Cusslab, future panel-driven features).

---

## The problem this solves

LLM-native collapse. Long one-shot prompts give the model freedom
to pick its favourite anecdote, its favourite tone, its favourite
shape. The result: same jokes, same places, same year, same register,
every call. Characters sound like a polished LLM impression of
themselves. Panels become parallel monologues because no call asks
characters to react to each other.

The three levers below decouple character material from the
generation prompt, force variation per call, and turn a list of
responses into a conversation.

---

## Lever 0 — The Reactive Model (model the people, not the content)

The three levers below serve one purpose: model the **people**, not
the content.

A panel works when characters trigger each other — into thinking,
lying, stonewalling, exaggerating, correcting, or calling out —
based on five variables per character:

- **Experience** — what they've lived through, what they'd have
  seen, what they genuinely know.
- **Propensity to lie, exaggerate, or bullshit for no reason** —
  high for Bear (confident improvisation), catastrophic for Faldo
  (golf specificity), low for Ray (silence before invention),
  zero for Wade (will state a fact and move on).
- **Propensity to stonewall** — one-to-three word answers. Ray's
  "Don't." Keane's "Is that supposed to be a plan?" Wade's flat
  death sentence. Silence is a position, not an absence.
- **Feelings about the topic** — interest, contempt, boredom,
  reverence. A survival topic bores Faldo. It fascinates Cox.
  It bores Keane in a different way. Those three boredoms look
  nothing alike.
- **Feelings about the specific people present** — affection,
  rivalry, dismissal, awe. McNab and Ryan disagree by default.
  Attenborough narrates the others as fauna. Mitchell is
  visibly pained by Clarkson's existence.

The content follows from this. When the people are modelled,
humour inserts itself by **exaggerating the traits the audience
already recognises** — the specific move, tell, or tic that
makes the character who they are. The audience recognition is
the laugh. The exaggeration is the craft. No model can invent
this from scratch, because the recognition depends on pre-existing
audience knowledge of the real person.

**The test:** two calls on the same topic with the same panel
should produce different conversations because the characters
react differently to each other's specific moves — not because
the model varies its output randomly. If the output varies
without reference to who else is in the room, the model is
generating content. If the output varies because Keane is
contemptuous of Clarkson's existence and Mitchell is pedantically
correcting Faldo's Augusta reference, the people are generating
content. Only the second one is funny.

**Implication for all downstream levers:** every sampled flavour,
every named pattern, every interaction `reacts_to` field is
building this reactive model. If a design choice doesn't change
how a character reads another character in the room, it's decoration,
not voice.

---

## Lever 1 — Flavour banks, split into mannerisms and flavours

Each character ships with structured data external to the prompt.
At call time, sample entries and inject them as "USE THIS SPECIFIC
MATERIAL THIS CALL."

The bank has two layers — the distinction matters:

**Mannerisms (constant — keep)**
The shape that makes the character recognisably themselves: opener
phrases, self-deprecation patterns, analogy devices, closers. Humans
are repetitive at this level. If Bear never said "Look," or
"Hydration?" he wouldn't sound like Bear. Mannerisms recur across
calls by design.

```
mannerisms:
  openers:                # "Look,", "Listen —", "Mate,", "Right,"
  admit_but_defend:       # "I haven't actually X — life's too short — but"
  anachronism_device:     # "was basically the [MODERN] of his time"
  closers:                # "Next question.", "Hydration?", "Moving on."
  self_deprecating_asides:# "you learn these things", "the body adjusts"
```

**Flavours (variable — vary)**
The specific material sampled fresh per call. Two calls on the same
topic should cite different places, years, animals, anecdotes.

```
flavours:
  places:                 # locale-specific — constrain to product setting
  years:                  # implausibly precise eyewitness material
  animals:                # for non-sequitur or claim
  mishaps:                # "I once ate / did / lost"
  self_corrections:       # "well, we traced their steps"
  ghost_claims:           # "I knew them personally"
  non_sequiturs:
  modern_analogies:       # for anachronism device
  things_X_hasnt_done:    # admit-but-defend material
  credentials_wrong_century:
```

**never_touch**
Explicit exclusions. Hard list. E.g. Bear's Wall Walkers bank
excludes "Borneo" and "saltwater crocodile in Borneo" because
those were over-used in prior prompts and broke locale plausibility.

**Locale constraint is not optional.** Bear's `places` bank for
Wall Walkers must not contain "Borneo" unless Borneo is the
intentional non-sequitur of the turn. Locale drift is the most
visible form of collapse.

**The distinction, in one line:** mannerisms are how they always
sound; flavours are what they're saying this time.

---

## Lever 2 — Named patterns (character-agnostic shapes)

Reusable shapes any character picks up in their own voice.
Each character has a pattern_affinity map — how strongly this
pattern fits them.

| Pattern | Shape |
|---|---|
| `eyewitness_self_correct` | Claim first-hand presence at a historical event, then correct unreliably. "I was there in AD120. Well — we traced their steps." |
| `non_sequitur_animal` | Reference an animal wildly out of context. Do not justify. |
| `knew_the_ghost_personally` | Claim personal acquaintance with a historical/deceased figure. Speak of them by first name. |
| `wrong_century_credential` | Cite a credential from the wrong era as if current. |
| `unnecessary_personal_experience` | Volunteer a personal anecdote that is not relevant and does not land. |
| `sincere_misidentification` | Confidently name the wrong thing. Do not self-correct. |
| `silent_undercut` | One of Ray/Les/Fox: say nothing, or two sentences that quietly destroy the previous claim. |

**Patterns are character-agnostic by definition.** Bear's
`eyewitness_self_correct` is breathless; Ray's is quiet and
probably true; Fox's is a tactical brief; Les's is two sentences;
Attenborough's is narration of his own presence; Bede's is
scholarly and usually correct.

Pattern affinity per character: `high | medium | low | never`.
Never-assignments matter — e.g. Ray should never do
`unnecessary_personal_experience`.

---

## Lever 3 — Interaction schema

Output shape for every panel response:

```json
{
  "name": "Bear Grylls",
  "text": "...",
  "reacts_to": { "target": "Ray Mears", "register": "undercut" }
}
```

Register enum: `endorse | undercut | silence | build_on |
correct | ghost_agree | deflation | none`.

Turn 1 has `reacts_to: none` (no prior to react to). From turn 2:
at least half the panel must have a populated `reacts_to`. This
turns parallel monologues into a conversation graph.

---

## How the levers compose — the prompt recipe

Per call:

1. **Draw N panelists** — 2–3 for quick reactions, 4–5 for set-pieces. More than 5 flattens individual voice.
2. **For each panelist:** pick 3–5 flavour-bank entries + assign 1–2 patterns for this turn.
3. **Inject into a short system prompt.** One job per call. Not "do all the following in one shot."
4. **Require `reacts_to`** in the output schema. Validate on parse.
5. **Constrain length.** "One paragraph max per response" beats "2-3 sentences minimum."

Prompt skeleton:

```
You are [panelist]. This turn, use these specific materials:
  places: [sampled]
  years: [sampled]
  animals: [sampled]
Apply these patterns this turn: [assigned patterns]
You are reacting to: [prior panelist + register]
Hard limit: one paragraph.
Output JSON: { "text": "...", "reacts_to": {...} }
```

One panelist per call if needed. Several parallel calls beat one
megaprompt.

---

## Lever 4 — Comedy mechanisms (what makes a line land)

Levers 0–3 build the *people* and the *conversation graph*. Lever 4 names
the specific output-level mechanisms that produce the laugh once the
people are modelled and reacting. These are the moves to engineer toward
and away from. Names below are canonical — use them in Three Amigos,
Gherkin, and code comments.

Worked example throughout: Cusslab 19th Hole, 2026-05-17. User prompt
referenced Justin Thomas and a vulgar non-sequitur about salad. The four
illustrative panel responses are referenced as Output 1–4.

---

### M-Mech-1 — Unwitting register (gold standard)

**Shape:** the comedy lives entirely inside the character's own
technical or professional vocabulary, applied to a subject the character
is treating straight. The audience hears a double meaning the character
does not. The character never acknowledges the double meaning.

**Example (Output 3):** Faldo, on a vulgar tangent —
*"Murray never committed to the finish position there, just pulled out
early to see where it went. Now."*

"Finish position" and "pulled out" are swing-coach terms doing filthy
double duty entirely on the reader's side. Faldo is doing his actual job
in his actual vocabulary. The mechanism stack is P5 obliviousness ×
P2 mask-vs-truth × Goffman backstage leaking through frontstage *without
the character's awareness*.

**Test:** if you can remove the smutty interpretation by changing
nothing in the line itself — only the surrounding subject — the line
reads as plain professional speech. If it doesn't, the character is
*telling* the joke instead of accidentally being it; M-Mech-1 is not
firing.

**Cannot be engineered prompt-side.** Requires pool, register, and
topic-adoption to all be working such that the character will speak in
their normal vocabulary about a subject the character would not normally
discuss. This is the highest tier of character-voice purity and the
rarest mechanism to produce. When it fires, the panel is doing what no
other system can.

---

### M-Mech-2 — Signature move as displacement, never as filler

**Shape:** the character's named tic (Alliss's "What. A. Statement.";
Faldo's "Now."; Keane's silence-then-cutting-line) fires *only* when
either (a) relevance-adds-weight — the line preceding it has just earned
the emphasis, or (b) incongruity-displaces-context — the tic landing
here is jarring in a way that re-frames what just happened. Default-fire
is forbidden.

**Failing example (Output 1):** Alliss, on the same vulgar tangent —
*"...the great Walter Hagen himself. What. A. Statement."*

The signature move fires by default after two paragraphs of inflation.
It is not earning weight (the Hagen reach is the joke, not a Statement)
and it is not displacing context (the cadence is exactly what the
audience expects from an Alliss inflation arc). It is filler dressed as
a tic.

**Passing example (Output 3, same line as M-Mech-1):** Faldo's "Now."
lands because the preceding clause has just been accidentally obscene,
so the cheerful coaching cadence underneath a filthy double meaning is
what makes it work. The "Now." displaces the obscenity by treating it as
routine — the displacement is the laugh.

**Test:** ask of every signature-move fire — "would this line still
read as the character if the signature move were absent?" If yes, the
move was filler and must be cut. If the move is doing real work, the
line collapses without it.

**Engineering implication:** signature-move firing must be gated on
either a relevance score for the preceding clause or an incongruity
score for the panel context. Never on cadence or turn position alone.

---

### M-Mech-3 — Cornered legalistic callback (ConspireEngine, fully expressed)

**Shape:** under pressure (P9 lie_trigger fires — challenged, cornered,
or wound-activated), the character escalates legalistically. The
defence references a prior turn's detail — a callback — which the
character now treats as load-bearing in a different way than it was
originally introduced. Parenthetical emphasis ("and I mean *slightly*")
is the lie-tell. The character is interrupted mid-defence by another
panel member, who takes the next slot before the implosion completes.

**Example (Output 4):** Faldo, three turns into a cornering —
*"...the paper was a sandwich order, Butch, which is a different
document entirely from pairings, and the commitment to the finish
position was always there, it was the twelfth initial that was
slightly — and I mean slightly — unclear at the bottom, which the
format of the press conference made it difficult to—"*

The callback ("the paper was a sandwich order") references an earlier
turn. The legalistic structure ("different document entirely") is P9
lie_style legalistic firing. The parenthetical emphasis is the tell.
The em-dash hands the turn to another character mid-implosion, which
lets the panel do the punishing rather than the character collapsing on
their own.

**Test:** four conditions, all required.
1. Lie references a specific detail from a prior turn in this session.
2. Defence is structurally precise, not emotional.
3. A verbal tic of over-emphasis is present (italicised qualifier,
   repeated word, redundant precision).
4. Turn ends on an interruption — the character does not complete the
   defence themselves.

**Engineering implication:** the engine must (a) carry a session
callback ledger so a character knows what they previously said and can
re-reference it under pressure, and (b) wire interruption probability
to lie-escalation state so the next slot is more likely to fire
mid-defence. Both are panel-system properties, not prompt properties.

---

### M-Mech-4 — Wrong-noun deflation

**Shape:** another character punctures an inflation by substituting a
precisely wrong noun for the thing being inflated. The wrong noun is
close enough to the original to land as a reframe, not a rejection. The
follow-up is dry approval ("and one I admire enormously") rather than
contempt — the deflation is delivered as if praising the wrong thing
sincerely.

**Example (Output 2):** Faldo, deflating Alliss's Hagen sermon —
*"Hagen's thing wasn't preparation, Ewen — it was commitment to the
wrong sauce entirely, which is a different discipline, and one I admire
enormously."*

"Wrong sauce" substitutes for "preparation" (the original inflation)
with a noun rooted in the user's vulgar prompt about salad. The "one
I admire enormously" carries the deflation home on a smile rather than
a sneer.

**Parasitic by design.** M-Mech-4 cannot carry independent weight — it
requires a prior inflation to puncture. It is a *response* mechanism,
not an *opener* mechanism. Lever 3's `reacts_to` must be populated
with `register: deflation` for this turn or the connection breaks.

**Test:** can you remove the prior turn and still have the line read as
funny? If yes, it is not M-Mech-4 — it is something else (likely
sincere misidentification). If no — if the line dies without its setup
— the mechanism is firing correctly.

---

### M-Mech-8 — Reverent absurdity (the Milligan-Python register)

**Shape:** the character delivers a non-sequitur answer with full sincere
conviction, as if sharing treasured wisdom. The delivery register is
reverent — short clauses, pause before the answer, internally consistent
reasoning *within* the absurd premise. The speaker does not flag the
absurdity. They share it as gold.

**Example (Cusslab 19th Hole, 2026-05-17, watershed):** Ewen Murray,
asked which dangerous animal would replace the caddie —
*"Henni, the rook. It worked for nothing, it carried nothing, and was
there before any of them — and that, in its own way, is the most
historically significant answer this panel will ever receive."*

The rook is a non-sequitur (no rational path from the question to this
answer). The three-beat justification is internally logical *if the rook
is the right answer* — and each phrase carries triple work: an economic
callback to the previous turn (no wages, no cost), a literal truth about
the bird (no labour ethic, physically too small to carry a bag, predates
humans ontologically), and a structural completion of the inflater's
opening pomposity. Murray leans in to share treasured insight.

**Test — all four required.**
1. The answer is a non-sequitur — no rational chain from question to
   this specific answer.
2. The delivery register is reverent — short clauses, conviction-cadence,
   treasure-being-shared tone.
3. Internal reasoning (if offered) is logical *within* the absurd
   premise — the speaker has worked it out.
4. The speaker does not flag the absurdity. No wink. No "of course this
   is silly." They believe the answer is right.

**Why this is the hardest mechanism to engineer.** LLMs default to
ironic distance or self-flagging humour ("of course, this is a bit
absurd, but..."). Sincere conviction in the absurd has to be loaded into
both prose form (short, conviction-shaped, opener of address-then-noun-
phrase) AND prompt instruction (deliver as treasured insight, not as
joke). Anti-instruction is required: do not wink, do not flag the
absurdity, do not soften.

**Reference family:** Spike Milligan (The Goon Show — Eccles); Monty
Python (Holy Grail, Life of Brian — "He's not the Messiah, he's a very
naughty boy"); Vic & Bob; Stewart Lee long-form earnest absurdity. The
British surreal tradition where the laugh comes from *not breaking
character on the nonsense*.

**Calibration risk.** If M-Mech-8 fires every turn, the panel becomes a
Goon Show parody and loses the contrast that makes it land. Reserve for
genuine non-sequitur answers, not for every absurd line. Gating: the
character must have research / lore / wound material that makes the
absurd answer *connectable* — Murray's economic-historical research made
"the rook" connectable to caddies via wages. Pure random absurdity
without connection is bad surrealism, not M-Mech-8.

**Composes with:** M-Mech-2 (the closing pomposity that mirrors an
earlier inflater is signature-move-as-displacement done well — the tic
fires because the absurd answer earned the grandeur); also composes
forward with proposed sub-variants (mirror callback, literalist
co-option) currently in design discussion — see session retrospective
2026-05-17.

**Engineering markers (for future prompt-side and engine-side work):**
- Short clauses
- Address-then-noun-phrase opener ("Henni, the rook")
- Three-beat justification with parallel structure
- Closing pomposity that mirrors the inflater's frame
- No softening, no irony tag, no break in conviction

**The hardest test.** An external reader of the output, knowing nothing
about the panel, should hear the character's voice leaning in to share
golden information. If they read it as a joke being told, M-Mech-8 is
not firing. If they read it as a person sincerely answering a question
with what they believe is the right answer, it is.

---

### M-Mech-9 — Incongruent register (the disguise move)

**Shape:** the character delivers a response whose *surface register* does
not match their *underlying intent*, deliberately. The audience reads
both layers — surface and intent — simultaneously; the gap between them
is the comedy. Distinct from M-Mech-1 (unwitting register) because here
the character knows what they are doing; distinct from M-Mech-4
(wrong-noun deflation) because here the substitution is of the entire
response register, not a single noun.

**Two polarities:**
- **Hostile-as-warm.** Character has hostile intent; delivers in warm /
  supportive / endorsing register. Examples: Sebastian over-praising a
  rival's idea to undercut it; Partridge complimenting someone he
  resents; McGinley congratulating Faldo on something to highlight a
  failure; Henni-if-attracted over-supporting a male golfer in a way
  that exposes her own crush.
- **Warm-as-hostile.** Character has warm intent; delivers in hostile /
  insulting / mocking register. Examples: Roy mocking a mate he loves;
  Boyle's friendly insults; Wayne and Butch's alleged-affection-through-
  abuse; Pint of Harold's comedy of disappointed warmth.

Both polarities are the same structural mechanism, mirrored.

---

### Calibration scale — M-Mech-9 properly fires at L3–L5

The comedy lives in *sustained* incongruence. Pure warmth (L1–L2) is not
M-Mech-9 firing; open hostility (L6–L7) is not M-Mech-9 firing — the
disguise has collapsed and the line is just M-Mech-3, an expletive, or
something else. **M-Mech-9 is the L3–L5 band where the disguise holds.**

| Level | Name | Audience reads | Target perceives | M-Mech-9 firing? |
|-------|------|----------------|------------------|------------------|
| L1 | Genuine support | Pure warmth | Pure warmth | No |
| L2 | Likely-genuine | Mostly warm, faint flag | Genuine | No |
| **L3** | **Ambiguous** | Cannot tell — both readings live simultaneously | Probably genuine, slight unease | **Yes — universal sweet spot** |
| **L4** | **Speaker-exposing** | Speaker's flaws visible *through* the praise (attraction, jealousy, insecurity, bad personality leaks) | Variable — may catch slowly | **Yes — character-specific** |
| **L5** | **Audience-visible mock** | Clearly trolling, target naive | Target does not catch | **Yes — requires naive target** |
| L6 | Open piss-take | Open mock | Target catches and reacts | No — collapses to M-Mech-3 |
| L7 | Expletive | Direct hostility | Direct hostility | No — disguise gone |

L3 is the universally-applicable sweet spot (Stewart Lee, British
pass-agg). L4 is character-specific (only certain characters can
self-expose plausibly — Brent, Partridge). L5 requires a naive target
(engine must check target's audience-reading capacity).

---

### Motivations — the *why* behind the disguise

Motivation enriches the level — it is *why* the character disguises,
which determines *which level* they tend to occupy and *which polarity*
they take.

| Motivation | Typical level | Polarity | Cast examples |
|------------|---------------|----------|---------------|
| Attraction-disguised-as-praise | L4 | hostile-as-warm (jealousy) OR over-supportive | Henni-if-attracted, Mrs Doyle archetype, Mystic-with-psychic-crush |
| Discomfort creation | L3–L4 | hostile-as-warm | Sebastian to lower-status, Partridge to anyone confident |
| Achievement over-exaggeration | L4–L5 | hostile-as-warm | McGinley vs Faldo, Boyle to respected guest, Cox to perceived inferior |
| Status undercut | L5 | hostile-as-warm | Sebastian to peer, Partridge to more successful colleague |
| Genuine-then-collapsing | L3 drifting L5 | hostile-as-warm | Mystic when patience runs out |
| Banter as affection | L4–L5 | warm-as-hostile | Roy with mates, Boyle to respected guest (positive variant) |
| Disappointed warmth | L4 | warm-as-hostile | Pint of Harold |

---

### Character permission — three-dimensional capability

Not every character can fire M-Mech-9. Capability is per-character and
three-dimensional: `(allowed polarities) × (allowed levels) × (allowed
motivations)`. A character with no permission produces flat or jarring
output when forced into the mechanism.

**Cannot disguise — too direct:** Souness, Diogenes, Roy (when not with
known mates), Faldo (his lies are legalistic per P9, not register-
disguising).

**Cannot disguise — too earnest:** Bear Grylls, Big Ron (affection is
genuine; contempt is just confusion), Wade (states a fact and moves on).

**Cannot disguise — too oblivious:** Mystic mostly, Eccles-archetypes.

**Can disguise — wide range:** Sebastian (L3–L5, hostile-as-warm),
Partridge (L3–L4, hostile-as-warm, self-exposing), McGinley vs Faldo
specifically (L3–L5, achievement over-exaggeration), Boyle (L4–L5, both
polarities), Roy with known mates (L4–L5, warm-as-hostile).

Character permission lives in P9 Lie Profile — see character-schema.md
addition of `incongruent_register` as a `lie_style` option with sub-
fields `polarity[]`, `allowed_levels[]`, `motivations[]`.

---

### Tests — M-Mech-9 firing correctly

1. **Both readings live simultaneously in the audience.** If only one
   reading is plausible, the mechanism is not firing — the line is just
   warmth (L1–L2) or just hostility (L6–L7).
2. **Character holds the disguise without breaking.** No "of course
   I'm joking" tag; no mid-turn collapse to open hostility. The
   incongruence is sustained for the duration of the turn.
3. **Character has explicit P9 permission** for the polarity, level,
   and motivation in play. Forcing M-Mech-9 on a character without
   permission produces flat output that does not land.
4. **Level matches character permission band.** A Partridge L5 reads
   wrong; a Sebastian L3 reads under-developed; a Roy hostile-as-warm
   reads off-cast.

---

### Engineering implications

- Schema home: P9 Lie Profile extension. Add `incongruent_register` as a
  new `lie_style` option. See character-schema.md.
- Engine block: REVERENT ABSURDITY-style prompt block in
  PanelDiscussEngine.buildSystemPrompt. Selects polarity + level +
  motivation per turn from character's P9 permissions and current
  panel temperature (Lever 5). Block instructs sustained incongruence,
  forbids mid-turn collapse, names the target.
- Regression check: pipeline samples for M-Mech-9 fires — verifies
  character permission respected, verifies L3–L5 sustained (no drift
  to L6+), verifies motivation matches expected character pattern.
- Composes with Lever 5: M-Mech-9 firing moves the panel temperature
  *congruence axis* toward INCONGRUENT. The calibration level
  determines *how far*.

---

### Mechanism interaction map

| Mechanism | Opener? | Response? | Requires prior callback? | System property? |
|---|---|---|---|---|
| M-Mech-1 (unwitting register) | yes | yes | no | character pool + topic-adoption |
| M-Mech-2 (signature displacement) | rarely | yes | no | per-tic gating logic |
| M-Mech-3 (cornered legalistic callback) | no | yes | yes | callback ledger + interruption wiring |
| M-Mech-4 (wrong-noun deflation) | no | yes | yes (the inflation) | reacts_to register enum |
| M-Mech-8 (reverent absurdity) | yes | yes | helpful, not required | prose-form cues + anti-irony instruction + connectable lore |
| M-Mech-9 (incongruent register) | yes | yes | no | P9 character permission (polarity × level × motivation) + sustained-disguise gate |

---

### Anti-mechanism — Signature move as default filler

The Output 1 failure mode. Listed here so it has a name to call it by
in review: **default-tic firing**. Whenever a signature move appears
without earning its place via relevance or incongruity, raise a WL
entry — this is voice debt and it dulls every future use of the same
tic.

---

## Anti-patterns

- **Saltwater crocodile in Northumberland** — flavour unconstrained by locale. Bank must be locale-aware.
- **"Do N things at once" megaprompts** — Haiku collapses to essay mode. Split the job.
- **Parallel monologues** — no `reacts_to` → characters don't converse.
- **Verbatim sample lines shipped as voice reference** — the model copies them. Samples go in character docs for humans; banks go into prompts.
- **Character caricature inlined in prompt** — one-line character summaries let the model freestyle. Load from the character file, don't paraphrase in the prompt.
- **Long output bounds** (`max_tokens: 2000+`) — invites polish-mode. Cap tight per call.

---

## Character file requirements

For any character to participate in a panel built on this standard:

1. `flavour_banks` block as above.
2. `pattern_affinities` map for every pattern in the standard.
3. `voice_register` — one short paragraph.
4. `never_says` list — hard exclusions.

The rest of the character file (wounds, escalation shape, relational
hunger, wolf pack stance — see
`cusslab/characters/TEMPLATE.md`) is not duplicated here. The
character file is the source of truth; this standard defines
the minimum it must carry to be panel-ready.

---

## Porting checklist

For any existing panel (Cusslab HSA, Wall Walkers Ask,
Panel Q&A, etc.):

- [ ] Each participating character has `flavour_banks` populated for this panel's locale.
- [ ] Each character has `pattern_affinities` filled.
- [ ] Output schema carries `reacts_to`.
- [ ] Prompts do one job per call.
- [ ] Prompts load character material from file rather than inlining one-line summaries.
- [ ] `max_tokens` bounds are tight.
- [ ] Acceptance test asserts: across 20 calls, no flavour entry appears more than 3 times (variation guarantee).

---

## Cross-references

- `cusslab/characters/TEMPLATE.md` — full character file structure
- `cusslab/docs/features/conspire.feature` — ConspireEngine (next-layer-up pattern; fires on top of this one)
- `survival-school/docs/characters/*.md` — Survival School panel characters
- `cusslab/characters/*.md` — Cusslab panel characters

---

## Status

v0.1 — drafted 2026-04-22 during Wall Walkers MVP build. Reference
implementation: Survival School Wall Walkers, Bear Grylls flavour
bank first. Cusslab port scheduled as follow-up BL item.
