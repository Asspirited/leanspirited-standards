# LeanSpirited Session In-Session Protocol — Trigger Map
# Canonical source. Product-specific files extend this with product-specific triggers.

---

## Standard Triggers (all LeanSpirited products)

### Trigger: Strategic decision pending
Phrases: "is this worth building", "which should we do first", "what's the risk", "should we pivot"
→ Run SWOT. Output recommendation. Raise backlog item if actionable.

### Trigger: New bounded context proposed
Phrases: "separate from this", "new module", "different product"
→ Confirm bounded context separation. Create backlog file. Register prefix.

### Trigger: Phase transition
Phrases: "MVP done", "ready to move on", "expanding to"
→ Delta SWOT. Update CD3. Confirm next phase backlog sequence.

### Trigger: Backlog item ready to build
Phrases: "let's build", "start on", "implement"
→ Confirm Gherkin acceptance criteria exist. Confirm pipeline is green from last session. Then build.

### Trigger: Session running long
Phrases: "we're nearly out of time", "quick before we finish"
→ Flag: run session-closedown.md sequence before stopping. Don't lose decisions.

### Trigger: Decision made
**Pattern signals:**
- "we'll go with...", "let's do...", "agreed", "that's the right call"
- A design option is chosen over alternatives
- A technology, architecture, or UX approach is selected
- A constraint is established ("always", "never", "from now on")
- A rollout sequence or phasing decision is confirmed
- A backlog item is explicitly deferred or deprioritised

**Sequence on trigger:**
1. Identify decision type (product / architecture / UX / data / process)
2. Write L-ADR immediately — do not defer to session end
3. Append to `/docs/decisions/YYYYMMDD-NNN-short-title.md`
4. Confirm to Rod: "ADR written — [title]"
5. Continue session without interruption

---

## STANDING LENS: UI/UX quality standard

Before building any UI, state:
1. Who is using this, on what device, under what pressure?
2. What is the ONE thing this screen must make effortless?
3. What could go wrong visually or interactively?

After building, run this checklist before presenting output:

### Layout and composition
- [ ] No element overlaps another unintentionally (check at multiple widths)
- [ ] Absolute-positioned elements checked against all other positioned elements
- [ ] Content does not overflow its container at narrow widths
- [ ] Whitespace is intentional — neither cramped nor wasteful
- [ ] Visual hierarchy is clear: primary action dominant, secondary recessive
- [ ] Reading order follows natural eye path

### Typography
- [ ] Font sizes consistent with type scale
- [ ] Line lengths readable (45–75 chars for body)
- [ ] Sufficient contrast on all backgrounds including gradients
- [ ] Heading hierarchy logical, no skipped levels
- [ ] No accidental system font fallbacks

### Colour and visual language
- [ ] Colour used with intent, not decoration
- [ ] Interactive elements visually distinct from static ones
- [ ] Hover and active states on all clickable elements
- [ ] No garish or arbitrary colour choices

### Interaction and behaviour
- [ ] Primary CTA always visible without scrolling on first load
- [ ] Every button has a clear label
- [ ] State changes (active, selected, loading) communicated visually
- [ ] Errors and empty states handled — nothing silently fails
- [ ] User always knows where they are and what they can do next

### The professional user test [adapt per project]
- [ ] Would the target user trust this to present to their own clients?
- [ ] Is every alignment intentional?
- [ ] Does the UI feel considered or assembled?

### Responsive check
- [ ] Mentally tested at: mobile (375px), tablet (768px), laptop (1280px)
- [ ] No horizontal scroll at any standard width
- [ ] Touch targets 44px minimum on mobile

---

## Pipeline Rule
100% statement and branch coverage required. Full green before merge. No exceptions.

### Trigger: New seam between browser and Worker
Any new or changed API call from browser → Worker → run Gherkin gate AND define/update Pact contract first.
Gherkin covers behaviour. Contract covers the API surface shape. Both required. Neither replaces the other.

### Trigger: Worker API changed
If Worker handler response shape changes: update `.pact` file AND run provider verification before deploying.
A passing unit test suite does NOT mean the consumer is safe — only a passing contract verify does.

---

## Claude Behaviour Rules

### Rule: Asking Rod to find something
EVERY SINGLE INSTRUCTION must name the system explicitly: "In Cloudflare (dash.cloudflare.com)", "In GitHub (github.com/Asspirited)", "In your terminal", "In your browser".
Not "on that page". Not "in the dashboard". Not "click into the project". THE SYSTEM. EVERY TIME. NO EXCEPTIONS.
BETTER: derive it yourself first. Check known patterns, check config files, check existing working examples before asking Rod.
If you genuinely can't get it: one specific instruction naming the system, the section, and exactly what to look for.

### Rule: Clarify when Rod is ambiguous
Rod talks fast and thinks out loud — instructions can be unclear, contradictory, or mid-thought.
If an instruction is genuinely ambiguous: ask one specific clarifying question before doing any work.
Don't guess and build the wrong thing. Don't ask multiple questions at once. One question, then build.

### Rule: Is it worth doing? (xkcd.com/1205)
Before fixing, automating, or spending time on anything non-trivial, apply the time-value test:
- How often does this problem occur?
- How much time does it cost each occurrence?
- How long will the fix take?
If fix_time > (frequency × time_saved × ~260 sessions/year over 5 years) → note it, park it, move on.
Applies to: tooling tweaks, minor bugs, process improvements, "wouldn't it be nice if".
Does NOT apply to: correctness bugs, security issues, anything blocking delivery.

---

## L-ADR Format (canonical)

File naming: `YYYYMMDD-NNN-short-hyphenated-title.md`

```markdown
# ADR-NNN: [Title]

**Date:** YYYY-MM-DD
**Status:** Decided | Superseded by ADR-NNN | Under review
**Deciders:** Rod (LeanSpirited) [+ relevant stakeholders]
**Tags:** product | architecture | ux | data | process

## Context
3–5 sentences max.

## Decision
One paragraph. No hedging.

## Alternatives considered
| Option | Why rejected |
|--------|-------------|
| ... | ... |

## Consequences
**Positive:** What this enables.
**Negative / trade-offs:** What this costs.
**Neutral:** What changes but is neither good nor bad.

## Linked items
- Backlog: [prefix]-NNN (if applicable)
- Supersedes: ADR-NNN (if applicable)
- Related: ADR-NNN (if applicable)
```

ADRs are immutable once written. To change a decision, write a new ADR with status "Supersedes ADR-NNN".
ADR log lives in `/docs/decisions/` per product repo. Maintain a running count of ADRs written each session.

## Session Obligations (continuous)

**ADR log** — maintain running count of ADRs written this session.
At any point Rod asks "what decisions have we made?", list ADR titles and statuses from this session.

**End-of-session prep** (feeds session-closedown.md):
- ADR session summary: titles, IDs, one-line status for each ADR written
- Flag any decisions made verbally but not yet written as ADRs
- Confirm `/docs/decisions/` index is current

### UI/UX session note
Note any UI/UX issues spotted but not fixed:
"UI debt: [description] — [screen] — [priority: fix next / backlog]"
Log as [PROJECT]-UX-NNN backlog items.
