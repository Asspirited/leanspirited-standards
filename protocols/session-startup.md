# LeanSpirited Session Startup Protocol
# Canonical source. Product-specific files extend this.

---

## Mandatory Sequence — Run Before Any Work

### Step 1: Orientation
State the current date and confirm which product we're working on.

### Step 2: Read product claude.md and testing standards
Fetch and read `.claude/claude.md` in full.
Fetch and read `.claude/testing-standards.md` in full.

### Step 3: Shared session state
Read `.claude/shared-session-state.md` — carries what was done last session,
what's open, what the other Claude (ai/code) did. Do not skip.

### Step 4: Backlog review
Fetch both backlog files — **BL** (`docs/backlog.md`) and **WL** (`docs/watchlist.md`).
Both must exist. If either is missing on a new project, create it before proceeding.
Identify:
- Any items marked **SHIP TODAY** or **Critical**
- Any items **In Progress** from last session
- Top 3 open items by priority

### Step 5: HDD hypothesis status [ADAPT PER PROJECT]

State all open HDD hypotheses and their current status.
Format:

```
HDD-NNN: [Hypothesis statement]
Status:   OPEN / CONFIRMED / REFUTED / PIVOTED
Evidence: [What we have so far, or "None yet"]
Next validation action: [Specific next step]
```

If any HDD hypothesis is OPEN, state explicitly:
"Today's work should primarily serve [persona] unless a pivot is agreed
and recorded as an ADR."

### Step 6: SWOT check (at phase transitions or if hypothesis has changed)
If hypothesis has changed or we're at a phase boundary:
- Pull the product SWOT file
- Run delta SWOT
- Update CD3 prioritisation if needed

### Step 7: Confirm session goal
State the one thing that would make this session a success.
Confirm with Rod before starting work.
