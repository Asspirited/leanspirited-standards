# CD3 + SWOT Prioritisation

**Owner:** LeanSpirited  
**Version:** 1.1 (SWOT layer added, 2026-03-19)

---

## CD3 Axes (baseline)

| Axis | Question | Score |
|------|----------|-------|
| **C**ustomer value | How much does this matter to the user? | 1–5 |
| **D**ependencies | What is blocked until this is done? | 1–5 |
| **D**elivery complexity | How hard is this to build well? | 1–5 (inverted — lower is better) |

Items are sequenced by: `(Customer value + Dependencies) - Complexity`

---

## SWOT Strategic Weight Layer

Before sequencing, each item is assessed against four SWOT vectors:

| Vector | Question | Applies if... |
|--------|----------|---------------|
| **S** — Strength | Does this build on something we already do well? | Yes → +1 |
| **W** — Weakness | Does this address a weakness before it becomes a blocker? | Yes → +1 |
| **O** — Opportunity | Does this capture a time-sensitive opportunity? | Yes → +1 |
| **T** — Threat | Does this mitigate a threat that blocks other items? | Yes → +1 |

**Strategic weight** = sum of applicable SWOT vectors (0–4)

Items scoring 2+ on SWOT vectors are **promoted** in the sequence — even if CD3 alone would rank them lower.

---

## Combined Scoring

```
Priority score = (Customer value + Dependencies - Complexity) + (SWOT weight × 1.5)
```

The 1.5 multiplier reflects that strategic alignment should meaningfully influence sequencing but not completely override delivery logic.

---

## Full Prioritisation Protocol

1. List candidate backlog items
2. Score each on CD3 (1–5 per axis)
3. Score each on SWOT vectors (0–4 total)
4. Calculate combined priority score
5. Review top items for dependency conflicts
6. Confirm sequence with team
7. Record scores in backlog item or session notes

---

## Phase Transition Protocol

Before re-sequencing at a phase transition:

1. Review existing SWOT — has anything changed?
2. Run delta SWOT (what's new in each quadrant since last assessment)
3. Re-score affected backlog items with updated SWOT weights
4. Confirm next phase sequence
5. Store updated SWOT at `/docs/swot/swot-[product-slug]-phase[N]-[date].md`

---

## SWOT Storage Convention

All SWOTs are stored in the relevant product repo under `/docs/swot/`:

```
/docs/swot/
  swot-[product-slug]-inception-[date].md
  swot-[product-slug]-phase2-[date].md
  swot-[product-slug]-[decision-topic]-[date].md
```

First SWOT for Your Green Gardening Wizard:
`/docs/swot/swot-ygw-inception-2026-03-19.md`
(Source: Jerry Maynard's five-model analysis, WhatsApp thread 19/03/2026)
