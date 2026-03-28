# Backlog Display Standard — Session Closedown Report
# Canonical source. All Asspirited projects use this format at closedown.
# Last updated: 2026-03-28

---

## When to Display

At session closedown (Step 2 of the closedown protocol), display the full backlog
in the format below. This is mandatory for every session, every project.

---

## Format

Three tables, in this order:

### 1. Open (N items)

| ID | Title | Description | CD3 |
|----|-------|-------------|-----|
| SS-NNN | Short title | Brief description | score |

Sorted by CD3 descending. Include items with status: Open, In Progress, Blocked.
Row count displayed in section header as "(N items)".

### 2. Closed Today (N items)

"Today" = current 24-hour period in UK time (midnight to midnight GMT/BST).

| ID | Title | Description | CD3 | Pushed |
|----|-------|-------------|-----|--------|
| SS-NNN | Short title | Brief description | score | HH:MM |

Sorted by push time (earliest first). Push time = the `git log` timestamp of the
commit that closed the item (format: HH:MM UK time). If multiple commits touched
the item, use the final one.

Row count displayed in section header as "(N items)".

### 3. Closed Prior to Today (N items)

| ID | Title | Description | CD3 | Closed |
|----|-------|-------------|-----|--------|
| SS-NNN | Short title | Brief description | score | YYYY-MM-DD |

Sorted by closed date descending, then CD3 descending within same date.
Closed date = the date noted in the backlog status field (not git time).

Row count displayed in section header as "(N items)".

### Summary Line

After all three tables, display:

```
Totals: N open | N closed today | N closed prior | N total items
```

---

## How to Get Push Times

Run from the project root:

```bash
git log --format="%H %ai %s" --since="midnight" | grep -i "SS-\|BL-\|CL-\|YGW-\|UH-\|FF-"
```

Replace the grep pattern with the project's prefix. The `%ai` field gives
author date in ISO format — convert to UK time (GMT/BST) and display as HH:MM.

If no git commit references the item ID directly, use the commit that changed
the backlog file to mark it DONE.

---

## Column Definitions

| Column | Source | Notes |
|--------|--------|-------|
| ID | Backlog item prefix + number | e.g. SS-040 |
| Title | Backlog item title | Short, imperative |
| Description | One-line summary of what it is | Not the full spec |
| CD3 | CD3 score from backlog | Number or "—" if unscored |
| Pushed | Git push time (HH:MM UK) | Closed Today table only |
| Closed | Date from backlog status field | Closed Prior table only |

---

## Cross-Project Use

This standard applies to all Asspirited projects:
- Survival School (SS-)
- Cusslab (CL- / BL-)
- Fallacy Finder (FF- / V-)
- Your Green Gardening Wizard (YGW-)
- Universal Harmonix (UH-)
- Risk & Impact Assessor (RIA-)

Each project's `session-closedown.md` references this standard at Step 2.
The prefix in the grep pattern and table headers changes per project.
