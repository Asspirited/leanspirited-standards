# Backlog Format, Gherkin Conventions & Prefix Registry

**Owner:** LeanSpirited  
**Version:** 1.0

---

## Backlog Item Format

```markdown
## BL-[PREFIX]-[NNN] — [Short title]

**Status:** Open | In Progress | Done | Blocked | Deferred
**Priority:** Critical | High | Medium | Low
**Loop:** HDD | DDD | BDD | TDD (primary loop this item lives in)
**Raised:** YYYY-MM-DD

### User Story
As a [role],
I want [capability],
So that [outcome].

### Acceptance Criteria

```gherkin
Feature: [Feature name]

  Scenario: [Scenario name]
    Given [context]
    When [action]
    Then [outcome]
```

### Notes
- Dependencies, links, open questions
```

---

## Gherkin Conventions

- **Feature** names are noun phrases: "Garden profile capture", not "Capture garden profile"
- **Scenario** names describe the situation, not the test: "User provides incomplete profile", not "Test incomplete profile"
- **Given** sets context — never includes actions
- **When** is a single action — if you need two, split the scenario
- **Then** asserts observable outcomes — never implementation details
- Use **And** freely to keep steps readable
- Background blocks for shared Given context across scenarios in a feature

---

## Prefix Registry

| Prefix | Product / Scope | Repo |
|--------|----------------|------|
| `YGW-` | Your Green Gardening Wizard | Asspirited/your-green-gardening-wizard |
| `RIA-` | Risk and Impact Assessor | Asspirited/risk-and-impact-assessor |
| `CL-` | Cusslab / Heckler and Cox | Asspirited/cusslab |
| `STD-` | LeanSpirited Standards (cross-cutting) | Asspirited/leanspirited-standards |
| `BL-ORACLE-` | House Name Oracle (Cusslab panel) | Asspirited/cusslab |
| `TBT-` | Through the Biscuit Tin | Asspirited/cusslab (branch: through-the-biscuit-tin) |
| `UH-` | Universal Harmonix (UAP investigation app) | Asspirited/Universal-Harmonix |

### Registering a new prefix
Add a row to this table via PR to `leanspirited-standards` before raising the first item.

---

## Status Definitions

| Status | Meaning |
|--------|---------|
| Open | In backlog, not started |
| In Progress | Active in current or recent session |
| Done | Acceptance criteria met, pipeline green |
| Blocked | Cannot proceed — dependency noted in item |
| Deferred | Deliberately parked — reason noted |
