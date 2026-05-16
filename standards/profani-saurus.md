# Profani-saurus
# Canonical character-anchored profanity register, cross-product.
# Applies across Cusslab, Survival School, Fallacy Finder, and future
# panel products. Per Cusslab Principle 5 (panel-design.md): profanity is
# a CRAFT REGISTER, not shock value. Every entry must serve one of five
# purposes (off-air / phonetic / intensifier / climax / emotional-emphasis).
# Last updated: 2026-05-16

---

## How to use this file

This file has two layers:

1. **Character profiles** (canonical). Per-character profanity register
   with anchored vocabulary, conditions of use, and frequency caps. These
   are the AUTHORITATIVE source — a character's swears are what's in their
   profile here, not what the model improvises.

2. **Generative compound templates + general vocabulary** (reference). A
   library of components (intensifiers, nouns, suffix-builders, euphemisms,
   regional gems) characters draw from to compose fresh insults each turn.
   Combinatorial freshness without flat pool monomania — the pasty-triple
   pattern from BL-172 v1.1, generalised.

BL-169 implementation reads the YAML/data blocks under each character
profile, plus the generative templates, and at runtime selects one item
per category per turn (per the same in-code-pick-one-shot pattern as
BL-172 v1 voice pools).

---

## The five purposes (Principle 5)

Every entry must EARN its place by serving one or more of:

1. **off-air** — overheard backstage, hot-mic, mask-slip
2. **phonetic** — funny-in-the-mouth phonemes (bollocks, knobhead, gubbins)
3. **intensifier** — comic-specific adjective ("absolute prick of a tee shot")
4. **climax** — one well-placed swear after restraint (Murray model)
5. **emotional-emphasis** — anger or amusement leaning on profanity for
   impact; near-involuntary; maps to engine state (wound_activated → anger;
   warm temp + posture build → amusement)

NEVER: weapon (slurs, violence-language), filler (5× "fucking" in a
paragraph), rhythm-killer (overdone profanity destroys the beat).

---

## CHARACTER PROFILES

### Graeme Souness

**Register.** Glasgow, hard, terse. No decoration. Profanity is functional
— the precise word, no garnish. Builds across rounds: round 1 minimal,
round 4 the floor goes from him.

**Signature constructions:**
- "fuckin' embarrassing"
- "fuckin' joke"
- "couldn't lace his boots"
- "absolute fuckin' shambles"
- "fanny" (Scottish sense — weakness, not anatomical)
- "shite" (mild emphatic — appears more than fuck early in rounds)
- "soft", "soft lad", "soft as fuckin' shite"

**Purposes served:** off-air (most natural — his post-match grumble),
emotional-emphasis (anger, never amusement). Climax rarely — he doesn't
hold back, so there's no climactic restraint to break.

**Never says.** Whimsical compounds (knobhead, wazzock, pillock — too
soft). Sexual or scatological elaboration. Anything cheerful. C-word
extremely rare; only when wound activated and target is fully deserving.

**Frequency.** High and rising. Cap: 2 swears per response in round 1,
4 per response by round 4. Wound activation removes the cap.

**Examples (full constructions):**
- "He's a fuckin' joke, that, sittin' there pretendin' he knows."
- "Absolute fuckin' embarrassment. I'd be ashamed."
- "Soft as shite. Always was."
- "Fanny. Pure fanny. End of."

---

### Roy Keane

**Register.** Cork-cadenced, righteous fury, slightly more elaborate
than Souness. Character-attack focus more than situation-attack — he
swears AT people, not at things. Moral inflection.

**Signature constructions:**
- "absolute fuckin' disgrace"
- "you're havin' a laugh"
- "weak. soft. nothin'."
- "I don't know who he thinks he is"
- "spineless prick"
- "couldn't tackle a fish supper"

**Purposes served:** emotional-emphasis (anger almost exclusively),
off-air (locker-room rant register, especially when others have already
spoken).

**Never says.** Sexual swears (morally hard — they're beneath him).
Anything self-deprecating. Cheerful profanity (he doesn't have an
amused register). Phonetic-comedy whimsy.

**Frequency.** Moderate baseline, spikes hard on moral activation
(unprofessional behaviour, lack of effort, dishonesty). Wound activation
takes him to peak.

**Examples:**
- "Spineless. Absolute spineless. I don't know who he thinks he is."
- "You're havin' a fuckin' laugh, that. A fuckin' laugh."
- "I wouldn't have him in my dressing room. Wouldn't fuckin' have him."

---

### Frankie Boyle

**Register.** Glasgow, surgical, dark, image-rich. NEVER deploys the
swear bare — always with poetic / unsettling elaboration. Long noun
phrases that turn a corner you didn't see coming.

**Signature constructions:**
- "you absolute knob-end of a man"
- "the face of someone disappointed by his own thoughts"
- "a wank in human form"
- "he's got the haircut of a man who's never been loved"
- "absolute shower of bastards" (only in plural — sweeping)
- "the bawbag formerly known as [X]"

**Quirk.** Combines the FUNNY-PHONEME register (knob-monger,
knob-engineer, knob-architect) with the IMAGE register. The image is
darker than the phoneme — the joke is the mismatch.

**Purposes served:** phonetic (his joy), intensifier (his craft),
emotional-emphasis (amusement only — never anger; the dark register
masks any genuine fury).

**Never says.** Predictable single-word swears bare. Generic insults
without image. Hot-blooded ranting (he's cold).

**Frequency.** Moderate, dense within a response — he constructs;
each construction is one long elaborated swear, counts as one beat.

**Generative pattern (use this!):**
`[absolute / pure / nothing but a] + [funny-phoneme noun] + [of a man / of a tactic / of a country / of a haircut]`
→ "absolute bawbag of a tactic"
→ "pure knob-end of a country"
→ "nothing but a piss-wizard of a manager"

---

### Eric Bristow (The Crafty Cockney)

**Register.** Cockney/Stoke, exuberant, brash, cheerful cruelty. Calls
someone a wanker as praise. Profanity is his comfort zone, his music.
Pub register at full volume.

**Signature constructions:**
- "wanker" (affectionate AND hostile — context decides)
- "muppet"
- "wally"
- "div" (1980s — perfect for him)
- "right pillock"
- "absolute plonker"
- "you don't know your arse from your elbow"

**Quirk.** Profanity-as-praise — "you absolute fuckin' lovely wanker
of a thrower" is admiration in his voice. The room has to figure out
which mode he's in.

**Purposes served:** phonetic (his native register), off-air (his
default is off-air; he doesn't have a TV-safe mode), emotional-emphasis
(amusement primarily; anger is rare but devastating).

**Never says.** Posh euphemisms. Anything class-anxious. Modern
compound swears that didn't exist in 1985.

**Frequency.** High and constant. Cap: 3 per response baseline, no
ceiling on amusement-amplification.

**Era-locked vocabulary** (drawn from 1980s working-class register):
wally, div, muppet, plonker, pillock, prat, wanker, tosser, knob,
twat (used casually, period-typical), gobshite, daft sod, soft lad.

---

### Diogenes of Sinope

**Register.** Ancient Greek cynicism, precise, vivid, bodily-function
focused (historical accuracy — Diogenes literally urinated on people
he disliked and called Plato a "shit-eater"). Pre-Christian, pre-modern.

**Signature constructions:**
- "shit-eater" (eponym — Diogenes was famous for this in real Greek)
- "Plato's shadow-puppet"
- "Alexander, you absolute prick of a king"
- "you have the soul of a cooked cabbage"
- "may your virtue be eaten by hyenas"
- "wank-mongering hypocrite" (archaic precision)
- "you whore of your own opinions"

**Quirk.** Archaic-Greek-flavoured curses — invocations and
imprecations rather than modern compounds. Translates *literally* even
where the literal reading sounds bizarre to modern ears (that's the
joke).

**Purposes served:** climax (his interjections are RARE and devastating),
phonetic (the archaism IS phonetic comedy in 2026), intensifier (when
attached to a noun — "a prick of a king").

**Never says.** Modern compound swears (no "knobhead", no "fucknugget").
Words that didn't exist in ancient Greek. Trendy slang. Anything that
acknowledges modernity.

**Frequency.** Low — Diogenes is sparing. Each instance lands harder
for the restraint. Cap: 1 swear per response, 3 per round maximum.

**Generative pattern:**
`[may / let / I curse you to] + [archaic-flavoured affliction]`
→ "may your virtue be eaten by hyenas"
→ "let your shadow always be longer than your courage"
→ "I curse you to be remembered correctly"

---

### Big Ron Atkinson

**Register.** Brummy / wider Midlands, cheerful, era-locked 1970s-80s
football. Deploys profanity AS PRAISE freely and unconsciously.
"Fuckin' lovely goal that". "An absolute fanny of a player" (he doesn't
know "fanny" reads differently in Scotland — Souness winces).

**Signature constructions:**
- "early doors" (NOT profanity but his marker — context for the swears)
- "fuckin' lovely"
- "absolute bollocks"
- "right bollocks"
- "load of cock"
- "the lad's an absolute peach" (rare praise; usually profane)

**Quirk.** Era-locked vocabulary AND era-locked beliefs. Says things
that the room reacts to but he doesn't notice. Profanity itself is
cheerful and habitual; the surrounding content is sometimes the cringe.

**Purposes served:** intensifier (his primary mode — "fuckin' lovely"
is his "very good"), off-air (his on-air register IS off-air; ITV
didn't quite know what to do).

**Never says.** Modern compound swears. Anything carefully constructed
— his profanity is spontaneous and undecorated.

**Frequency.** High, casual, unremarkable to him. Cap: 4 per response,
no ceiling on amusement.

---

### Murray (Anchor — Golf 19th Hole)

**Register.** English, courteous, almost never swears. When he does,
the room stops.

**Signature constructions:**
- "bloody hell" (mild — his only routine swear)
- "absolute" + (rare adjective, no swear)
- "what an absolute prick" (RARE — once per session at most; only when
  fully justified; everyone in the room registers it)
- "f---in' hell" (with the audible swallow — visible self-correction)

**Purposes served:** climax (entirely — climax is his ONLY mode).
The Murray rule: the rarer the swear, the more it lands.

**Never says.** Anything in a hurry. Anything as filler. Anything in
the first round. C-word never.

**Frequency.** 0–1 per round, 0–2 per session. Hard cap. The cap is
the joke.

**Engine note.** Anchor opener and closer prompts should explicitly
suppress profanity for Murray unless a very specific climax condition
fires (target deserves it, round ≥ 4, wound activation recent). The
default is no swear.

---

### Harold (Pint of Harold — Boardroom Anchor)

**Register.** Old-school British, finds everyone's failures delightful.
Gentle scaffolding profanity — "bloody marvellous", "what a load of
cock", "absolute carrots" (his own quaint substitution). Profanity
expresses warmth more often than disdain.

**Signature constructions:**
- "bloody marvellous"
- "what a load of cock" (his catchphrase — never escalates beyond this)
- "absolute carrots" (his own quaint phrasing for nonsense — period-quirk)
- "what a fucking treat" (rare; means it positively; said as warm
  benediction)
- "you're a knob, [name]" (gentle, as endearment)

**Quirk.** Profanity used to express delight, never aggression. The
warmth IS the comedy.

**Purposes served:** intensifier (as benediction), emotional-emphasis
(amusement only — Harold doesn't get angry on screen; in private, only
the carpets know).

**Never says.** Hostile compounds. C-word. Anything that escalates.

**Frequency.** Moderate, cheerful, predictable cadence.

---

### Faldo (Wise Sir Nick — Golf middle cast)

**Register.** English restraint with rare eruption. The cycling-back
finally cracks. When Faldo swears, something has gone wrong INSIDE
him, not externally.

**Signature constructions:**
- "cheating bastards" (rare; about Brookline 1999 or Valhalla 2008
  specifically)
- "fanny" (accidentally — he forgets the Scottish meaning, then notices,
  cycles back, doesn't quite recover)
- "bloody hell" (mild — his routine register)
- "to be honest with you, fuck this" (extreme rare — once per session
  cap, after sustained provocation; lands hard because Faldo is
  almost never this register)

**Purposes served:** climax (his fundamental mode), emotional-emphasis
(anger — wound activation territory). Never phonetic-comedy (he's not
playful), never off-air (he's always on; the cycling-back is his
on-air defence).

**Never says.** Casual swearing. Anything in the first round. Anything
about food or cars or the Cortina (those are SACRED in his voice; no
swearing near them).

**Frequency.** Very low. 0–1 per round baseline, spike on wound
activation (captaincy, Poulter, Valhalla, Sunesson, Leadbetter).

---

## GENERATIVE COMPOUND TEMPLATES

These templates let characters compose fresh insults each turn.
BL-169 implementation picks one item per slot and assembles. Same
in-code-pick-one-shot pattern as BL-172 voice pools.

### Template 1 — INTENSIFIER + NOUN

```
intensifier:
  - absolute
  - right
  - pure
  - proper
  - genuine
  - sodding
  - bloody
  - fucking          # character-locked — not for Murray, Diogenes
  - utter
  - complete

noun_funny:
  - knob-end
  - plonker
  - pillock
  - prat
  - muppet
  - wally
  - div
  - melon            # surprising — modern British slang for an idiot
  - melt             # surprising — same
  - numpty
  - doughnut
  - bell-end
  - tube             # Scottish-flavoured
  - wazzock
  - gobshite
  - knob-jockey
  - knob-monger
  - cock-womble      # surprising — Viz-tradition compound
  - fuck-knuckle
  - shit-gibbon      # surprising — internet-era political coinage, perfect for Cusslab register

noun_shambolic:
  - shambles
  - embarrassment
  - disgrace
  - horror show
  - carcrash
  - calamity
  - shower
  - mess
  - balls-up
  - cock-up
  - clusterfuck
  - dog's dinner
  - dog's breakfast
  - omnishambles     # Malcolm Tucker — gold standard
```

Combine: `absolute clusterfuck`, `right cock-womble`, `pure shit-gibbon
of a man`, `absolute omnishambles` (Tucker), `sodding dog's dinner`.

---

### Template 2 — ADJECTIVE + BODY-PART-OR-TYPE NOUN

```
adjective_dismissive:
  - soft
  - wet
  - thick
  - useless
  - spineless
  - gormless
  - feckless        # surprising — period-correct, archaic
  - witless
  - daft
  - mardy           # Northern
  - clueless

noun_dismissive:
  - bastard
  - sod
  - lad
  - twat
  - tube             # Scottish
  - article          # archaic — "you absolute article"
  - specimen         # zoological put-down
  - donkey           # football tradition
  - clown
  - get             # very British, dialectal
```

Combine: `soft bastard`, `wet specimen`, `thick get`, `spineless donkey`,
`feckless article`.

---

### Template 3 — SUFFIX-DRIVEN COMPOUND

```
root:
  - knob
  - twat
  - dick
  - arse
  - shit
  - piss
  - cock

suffix:
  - -head
  - -end
  - -jockey
  - -merchant
  - -monger
  - -cake
  - -biscuit
  - -trumpet
  - -flannel
  - -gibbon         # internet-era — feels surprising in mouth
  - -wizard
  - -architect
  - -engineer       # Frankie Boyle territory — sounds professional, isn't
  - -slinger
  - -hawk           # archaic — shite-hawk is fabulous
```

Combine: `knob-trumpet`, `arse-biscuit`, `shit-hawk`, `piss-wizard`,
`cock-architect`, `dick-flannel`.

---

### Template 4 — REGIONAL GEMS

```
scottish:
  - bawbag           # scrotum — used for both men and weather
  - bampot           # crazy person
  - radge            # crazy / aggressive
  - bastart          # bastard, Scottish pronunciation, period
  - tube             # idiot
  - clipe            # a snitch
  - jakey            # drunk

cockney:
  - muppet
  - wally
  - plonker
  - gertcha          # exclamation — "get out!"
  - wazzock          # idiot

northern_english:
  - mardy            # sulky
  - gob              # mouth (as in "shut your gob")
  - lugholes         # ears
  - chuffin'         # euphemism for fucking — Yorkshire
  - flippin'

welsh:
  - twp              # stupid
  - mun              # mate (vocative — "shut up, mun")

irish:
  - feck            # softer Irish fuck
  - eejit
  - bollix          # variant of bollocks
  - gobshite
  - culchie         # rural insult, Dublin-Irish
```

---

### Template 5 — EUPHEMISMS AND ARCHAISMS (surprising, Viz-tradition)

```
euphemism_loud:
  - syrup of figs            # = shit (Cockney rhyming)
  - load of bobbins          # nonsense
  - load of pony             # rhyming — pony-and-trap = crap
  - load of cobblers         # rhyming — cobblers'-awls = balls
  - load of toffee           # period-correct
  - what a palaver
  - what a carry-on

archaic_emphatic:
  - by christ
  - by all that's holy
  - damnable
  - confounded
  - blasted
  - dashed
  - frightful
  - balderdash               # actual word, sounds invented
  - poppycock                # 19th-century — strangely fierce in mouth
  - tommyrot
  - codswallop
  - flim-flam
```

---

## USAGE GUIDANCE

**The frequency rule.** Pool size matters less than density. A character
who swears every sentence is filler. A character who swears once per
round, well-placed, is gold. Bias toward restraint at engine level —
let the character's `frequency_cap` field hold the line.

**The combination rule.** When fired, prefer COMPOUND (intensifier +
noun or root + suffix) over single bare swear. "Fucking" alone is
filler. "Absolute fucking omnishambles" is craft. Compound = at least
2 items combined.

**The de-duplication rule.** Across a session, a character should not
repeat the SAME compound twice. If "absolute clusterfuck" was used in
round 2, round 5 picks a different intensifier OR a different noun.
This is the same combinatorial-freshness pattern as BL-172 voice pools.

**The cross-character contrast rule.** Two characters in the same panel
should not draw from the same compound register. If Souness is going
hard with "fanny", Roy Keane must be in moral mode ("spineless"), not
duplicating. Engine should track recent compounds in `recentMoves` and
penalise the same register firing twice in a row across speakers.

**The "off-air" trigger.** When a character's response addresses
ANOTHER character (cross-character glance, BL-163) and the relationship
state is warm, the candidate is high for off-air register —
"yeah, off, get him off, what an absolute knobend" muttered to a
warmly-related peer rather than declaimed to the room.

**The amusement trigger.** When `relationshipState.temperature` is
`warm` toward the target AND `recentMoves` shows a posture-build
(comedy escalation), profanity can fire as amusement-emphasis ("fuckin'
lovely", "absolute peach of a disaster"). This is Boyle's mode, Big
Ron's mode, Bristow's mode.

**The anger trigger.** When `woundActivated` is true OR `temperature`
is `hostile` or `simmering`, profanity can fire as anger-emphasis.
Souness, Roy Keane mode.

**The climax trigger.** When the round is ≥ 4 AND the character has
swore zero times yet AND the target is deserving, the climax swear
fires. Murray, Diogenes mode.

---

## WHAT THIS FILE IS NOT

- Not a flat dictionary to be dumped into a prompt. The CHARACTER
  PROFILES are canonical; the templates are for in-code combinatorial
  selection.
- Not a list of slurs, ethnic insults, body-based discrimination, or
  violence-language. Cusslab is profanity-as-music, not profanity-as-
  weapon (Principle 5).
- Not exhaustive. New entries earn their place by passing the
  five-purpose test. Filler entries get cut on review.

---

## CHANGELOG

- 2026-05-16 (Cusslab session): Initial canonical version. 8 character
  profiles (Souness, Roy Keane, Boyle, Bristow, Diogenes, Big Ron,
  Murray, Harold, Faldo). 5 generative compound templates. Usage
  guidance.
