# User Story Patterns — LeanSpirited Standard

How to shape a backlog item so it delivers discrete value and accepts fast
feedback. Applies across all LeanSpirited products. Read before writing or
splitting any BL item.

**Owner:** LeanSpirited
**Version:** 1.0
**Status:** v1.0 — drafted 2026-05-19. Rod authorisation: *"I prefer an Epic
split into stories that all deliver discrete value for that bigger piece
but allow faster delivery and feedback."*

This standard complements `backlog-format.md` (which defines the syntax of
a BL item). This document defines the **shape and content** — when a thing
is a single story, when it is an Epic that needs splitting, and how to split.

---

## The bedrock principle

**Every BL item must deliver discrete value on its own.**

If a BL is shipped and the product is not measurably better in some way a
real user would notice — that BL was the wrong size. It should have been
split, or absorbed into another item.

This rules out two common anti-patterns:

- **Phased stories (v1 / v2 / v3 within one BL):** the BL stays OPEN for
  ages, each phase ships partial value, and there's no clean "this is
  done" moment. The audit can't tell what's shipped from what's promised.
- **Capability stories ("Build the framework for X"):** no user notices a
  framework. If you can't write the user story sentence ("As a [role], I
  want [capability], so that [outcome]") and have the outcome be
  observable, you're describing infrastructure not a story.

Phasing belongs at the **Epic** level — see "Epic → Story decomposition"
below. Within a single BL, there is no v1/v2.

---

## INVEST — the test for a single story

Bill Wake's INVEST acronym. Each letter is a question you ask the BL item
before raising it. If any answer is "no", the item needs work before it
enters the backlog.

- **I — Independent.** Can this be shipped without first shipping another
  un-shipped story? If no, sequence the dependency first — or merge them.
- **N — Negotiable.** Is the wording open to refinement during ship, or
  is it a frozen contract? Stories invite discussion; specifications close
  it. If you cannot imagine the conversation changing the implementation,
  you've written a specification.
- **V — Valuable.** Will a user notice the change after ship? "User" can
  be the product end-user, an operator, a dependent system, or Rod testing
  in live. Infrastructure that no one notices is not a story — see "Story
  vs Enabler" below.
- **E — Estimable.** Can you guess the CD3 inputs (UBV / TC / RR / Dur)
  without first doing more investigation? If you need a spike, that spike
  is its own story.
- **S — Small.** Could a fresh session ship this end-to-end? Rule of
  thumb: one or two commits, one pipeline run. If it needs three or more
  shipping sessions, it is an Epic and needs splitting.
- **T — Testable.** Can you write the Gherkin scenario(s) for it before
  shipping? If not, the "Then" outcome isn't crisp enough yet — clarify
  the observable change.

The most common INVEST failure in our backlog: **S**. We accept BLs that
take 3-6 sessions to fully ship, ending up with v1/v2/v3 status mires. The
fix is to split into smaller stories before the BL is raised.

---

## Epic → Story decomposition

An **Epic** is a thematic chunk of work that's too big to be a single
story but small enough to remain coherent. Epics are *labels*, not BL
items — see `backlog-format.md`. Stories live inside Epics.

When you have a v1/v2/v3 instinct, ask: **"is this one story I'm
phasing, or is this an Epic with multiple stories?"**

If the v1 ships value standalone (user notices something improves),
v2 ships further value standalone (user notices a second thing improves),
v3 ships yet more — these are three stories in one Epic, not three phases
of one story. Split them.

Example — what we'd previously have raised as one BL with v1/v2/v3:

> **One BL (anti-pattern):**
> BL-XXX: Topic-dismissal moves — peers call out off-topic tangents.
> v1: prompt block. v2: drift detection. v3: per-character flavour profile.

Becomes three stories in an Epic:

> **Epic: Topic-dismissal mechanism**
> - BL-XXX: Panel members may call out off-topic tangents (prompt block).
>   Value: tangents get dismissed in live; the panel feels less monomaniacal.
> - BL-YYY: Engine detects drift automatically and fires dismissal block.
>   Value: dismissals fire on the right turns, not at model discretion.
> - BL-ZZZ: Per-character dismissal flavour profile (polite / cold / piss-take).
>   Value: dismissals sound like the dismisser, not generic.

Each is independently valuable. Each can be CD3-scored separately and
prioritised against unrelated work. The Epic label groups them.

---

## Story splitting patterns

When a BL feels too big, use one of these splits. Patterns are from Mike
Cohn (*User Stories Applied*) and Richard Lawrence's catalogue.

Pick the one that produces the most *valuable* slice first — the first
story shipped is the most important architectural decision in the split.

### 1. Workflow steps
Split a multi-step user workflow into its steps. Ship each step as its
own story, with the first step delivering the most-used path.
*Example: "Sign up" → "Capture email", "Verify email", "Set password".*

### 2. Business rules
The thing operates differently for different inputs/contexts. Split by
which rules apply.
*Example: "Pricing engine" → "Standard pricing", "Discount rules",
"Tier-2 customer rules".*

### 3. Major effort
One specific aspect of the story is significantly more work than the
rest. Ship the simpler version first, the major-effort version second.
*Example: "Payment" → "Card payment", "PayPal", "Bank transfer".*

### 4. Simple → complex
The story has a simple form that delivers value and a complex form that
adds more. Ship simple first.
*Example: "Search" → "Exact-match search", "Fuzzy search with relevance
scoring".*

### 5. Variations in data
The story handles many data types or formats. Split by type.
*Example: "Import" → "Import CSV", "Import JSON", "Import Excel".*

### 6. Methods of input
The story can be triggered by different input methods. Split by method.
*Example: "Submit feedback" → "Submit via form", "Submit via API",
"Submit via email reply".*

### 7. Defer performance
Ship the slow correct version first. Ship the fast version second as a
separate story when performance becomes the binding constraint.
*Example: "Generate report" → "Generate (synchronous, slow)",
"Generate (async, cached, fast)".*

### 8. Operations (CRUD)
Split create / read / update / delete into separate stories. Almost
always create + read first.
*Example: "Manage tournaments" → "Create tournament", "View tournament",
"Edit tournament", "Delete tournament".*

### 9. Break out a spike
The story has an unknown that needs investigation before it can be
estimated. Raise the spike as its own story; do not estimate the story
until the spike returns.
*Example: "Add OAuth" → "Spike: investigate OAuth providers (1-day
timebox)", then "Add Google OAuth", "Add GitHub OAuth".*

### 10. Happy path vs error path
Ship the happy path first. Each error path is its own story.
*Example: "Submit order" → "Submit order (happy path)", "Submit order
with declined payment", "Submit order with out-of-stock item".*

---

## Story vs Enabler

Some work is genuinely infrastructure — no user notices the ship in
isolation, but it unblocks subsequent stories. These are **Enablers**,
not stories.

Examples:
- Schema migrations
- Engine extractions / refactors with no user-facing change
- Pipeline scripts that protect future work without changing current behaviour
- Standards documents (like this one)

Enablers can be raised as BL items but **must be paired with the next
story that builds on them**. The pairing is the answer to "what user-
observable change does this unlock?" Without that pairing, the Enabler
is speculative — defer it until the dependent story is being scoped.

A practical rule: an Enabler with no concrete dependent story shipping
in the next 1-2 sessions is technical debt waiting to happen. Either pair
it or park it.

---

## Anti-patterns to refuse

If a draft BL falls into any of these, rewrite or split before raising:

| Anti-pattern | Why it fails INVEST | Fix |
|---|---|---|
| **v1 / v2 / v3 phasing in one BL** | Not S — needs multiple sessions to fully ship | Split into Epic with three stories |
| **"Build framework for X"** | Not V — no user notices | Split into the first concrete story that uses the framework; build framework as a byproduct |
| **"Refactor X for clarity"** | Not V — no user notices | Pair with the next user-facing change in X; do the refactor as part of that ship |
| **"Add option / config for X"** | Not T — no observable outcome | Add the option *and* the use that surfaces it; refuse options without users |
| **"Investigate X"** | Not E — open-ended | Convert to a spike with a hard timebox; the spike's output is the unblocker for an estimable story |
| **"Improve Y"** | Not T — outcome not observable | Define what "improved" means concretely (a metric? a Gherkin scenario? a user moment?); rewrite |
| **One BL containing multiple unrelated outcomes** | Not I (often) and not S | Split per outcome |

---

## Applying this to the current backlog

When auditing the existing backlog for INVEST compliance:

1. **For each BL with "v1 SHIPPED / v2 OPEN" status:** the v2 is almost
   certainly its own story. Close the original BL as Done (v1 was the
   real story); raise the v2 as a new BL with its own user story sentence
   and acceptance criteria.

2. **For each BL where the title says "X engine" or "X framework":** ask
   what concrete user-observable change it produces. If you can't answer,
   it's an Enabler — pair with a using story or park.

3. **For each BL still OPEN with "needs Three Amigos before ship":** it
   may be Epic-sized. Do the Three Amigos as a splitting exercise — find
   the first story that delivers discrete value, raise that, leave the
   rest in the Epic doc for later raising.

---

## Reference & further reading

- Bill Wake (2003) — *INVEST in Good Stories, and SMART Tasks*.
  Origin of the INVEST mnemonic.
- Mike Cohn (2004) — *User Stories Applied*. The canonical text on
  story-writing including splitting patterns.
- Richard Lawrence — *Patterns for Splitting User Stories*
  (agileforall.com). The 10-pattern catalogue this doc draws on.
- Jeff Patton (2014) — *User Story Mapping*. Epic → Story decomposition
  via the story map / journey backbone technique. Read when an Epic feels
  big enough that splitting isn't obvious.
- Gojko Adzic — *Specification by Example*. How acceptance criteria
  (Gherkin) and user stories work together — covered in our
  `bdd.md` / `tdd.md` practice docs.

---

## Cross-references

- `backlog-format.md` — the syntax of a BL item (User Story sentence,
  AC, status fields). This doc defines the shape and content; that doc
  defines the form.
- `cusslab/.claude/practices/hypothesis-driven.md` — Hypothesis Cards
  for product-bet stories. A Hypothesis Card sits at the *Epic* level —
  the Epic carries the hypothesis; individual stories ship slices that
  test it.
