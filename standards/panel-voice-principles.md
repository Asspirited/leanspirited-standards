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

### Mechanism interaction map

| Mechanism | Opener? | Response? | Requires prior callback? | System property? |
|---|---|---|---|---|
| M-Mech-1 (unwitting register) | yes | yes | no | character pool + topic-adoption |
| M-Mech-2 (signature displacement) | rarely | yes | no | per-tic gating logic |
| M-Mech-3 (cornered legalistic callback) | no | yes | yes | callback ledger + interruption wiring |
| M-Mech-4 (wrong-noun deflation) | no | yes | yes (the inflation) | reacts_to register enum |

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
