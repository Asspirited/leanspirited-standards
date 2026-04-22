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
