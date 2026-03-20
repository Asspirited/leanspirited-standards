# L-ADR Format — LeanSpirited Standard

Lightweight Architecture Decision Records per Thoughtworks guidance.
One file per decision. Immutable once status is Decided.
To change a decision: write a new ADR superseding the old one.

---

## File naming

```
YYYYMMDD-NNN-short-hyphenated-title.md
```

Example: `20260320-001-archetype-first-suggestion-model.md`

---

## Template

```markdown
# ADR-NNN: [Title]

**Date:** YYYY-MM-DD
**Status:** Decided | Superseded by ADR-NNN | Under review
**Deciders:** [Names]
**Tags:** product | architecture | ux | data | process

## Context
What situation or problem prompted this decision?
What were the forces at play?
3–5 sentences maximum.

## Decision
What was decided, stated plainly. One paragraph. No hedging.

## Alternatives considered
| Option | Why rejected |
|--------|-------------|
| ...    | ...         |

## Consequences
**Positive:** What this enables or improves.
**Negative / trade-offs:** What this costs or constrains.
**Neutral:** What changes but is neither good nor bad.

## Linked items
- Backlog: [PROJECT]-NNN (if applicable)
- Supersedes: ADR-NNN (if applicable)
- Related: ADR-NNN (if applicable)
```

---

## Conventions

- ADRs are immutable — never edit a decided ADR
- Supersede with a new ADR if a decision changes
- Product AND technical decisions both get ADRs
- ADR log is the primary artifact shared with stakeholders
- Written to be readable by non-technical stakeholders
- Tags: product | architecture | ux | data | process
- Index maintained in `docs/decisions/README.md` per product repo
- ADR trigger and session obligations: see `protocols/session-insession.md`
