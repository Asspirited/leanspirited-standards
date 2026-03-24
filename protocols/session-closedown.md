# LeanSpirited Session Closedown Protocol
# Canonical source. Product-specific files extend this.

---

## Mandatory Sequence — Run Before Ending Any Session

### Step 1: Pipeline check
Is the pipeline green? If not, do not close. Fix or explicitly park with a blocked backlog item.

### Step 2: Backlog and Waste Log update
For every BL item touched this session:
- Update status (Open → In Progress → Done / Blocked / Deferred)
- Add any new items surfaced during the session
- Note any acceptance criteria changes

For the WL (`docs/waste-log.md`):
- Close any WL items resolved this session
- Add any new waste observations made during the session (defects, waits, risks surfaced)

### Step 3: ADR session summary
List every ADR written this session: title, ID, one-line status.
Flag any decisions made verbally but not yet written as ADRs.
Confirm `/docs/decisions/` index is current.

### Step 4: HDD advancement check [ADAPT PER PROJECT]

Answer every session before closing:

1. Did today's session advance the open HDD hypothesis? Yes / No / Partial
2. If yes — what specifically moved forward?
3. If no — what was the reason?
   (valid reasons: explicit pivot, scaffolding work, consumer feature agreed as intentional)
4. What is the next concrete action that would advance the hypothesis?
5. Who owns that action and by when?

### Step 5: Decisions log
List every significant decision made this session not captured in an ADR or backlog item.
Format: `DECISION [date]: [what was decided] — [why]`

### Step 6: SWOT update (if applicable)
If the session produced strategic learning (user feedback, commercial input, technical discovery):
- Note which SWOT quadrant(s) are affected
- Update the product SWOT file or create a new delta SWOT
- Re-run CD3+SWOT prioritisation if priorities have shifted

### Step 7: Next session setup
State the top 3 items for next session, in priority order.
State the session goal in one sentence.
Note any blockers that need resolving before next session.

### Step 8: Shared session state
Write `.claude/shared-session-state.md` with what was done, decisions made,
HDD status, and top 3 for next session. This is read by the other Claude at next start.

### Step 9: Commit reminder
List files that need committing:
- New/changed source files
- Updated backlog
- New/updated SWOT documents
- Updated session protocol files (if changed)
- New ADRs
