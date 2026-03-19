# TDD-BDD-DDD-HDD: The Four-Loop Delivery Framework

**Owner:** LeanSpirited  
**Version:** 1.1 (SWOT added to HDD toolkit, 2026-03-19)

---

## Overview

Four nested feedback loops, each operating at a different timescale. The outer loop governs all inner loops — if HDD says "wrong problem", everything else is waste.

```
╔══════════════════════════════════════════╗
║  HDD — Hypothesis-Driven Development     ║  across sessions / months
║  ┌────────────────────────────────────┐  ║
║  │  DDD — Domain-Driven Design        │  ║  ongoing / bounded contexts
║  │  ┌──────────────────────────────┐  │  ║
║  │  │  BDD — Behaviour-Driven Dev  │  │  ║  per session / feature
║  │  │  ┌────────────────────────┐  │  │  ║
║  │  │  │  TDD — Test-Driven Dev │  │  │  ║  seconds / red-green-refactor
║  │  │  └────────────────────────┘  │  │  ║
║  │  └──────────────────────────────┘  │  ║
║  └────────────────────────────────────┘  ║
╚══════════════════════════════════════════╝
```

---

## Loop 1: TDD (innermost)

**Timescale:** Seconds to minutes  
**Question:** Does this code do what I think it does?  
**Rhythm:** Red → Green → Refactor  
**Enforcement:** 100% statement and branch coverage. Pipeline must be full green before merge.

---

## Loop 2: BDD

**Timescale:** Session to session  
**Question:** Are we building the right behaviour?  
**Rhythm:** Gherkin scenario → implementation → passing scenario  
**Enforcement:** All backlog items have Gherkin acceptance criteria before build begins. Session protocols are the mechanical expression of this loop.

---

## Loop 3: DDD

**Timescale:** Ongoing, across sessions  
**Question:** Are we modelling the right domain?  
**Key concepts:** Bounded contexts, ubiquitous language, anti-corruption layers  
**Enforcement:** New bounded contexts require justification. Shared concepts across contexts require explicit ACL design. Session closedown reviews domain integrity.

---

## Loop 4: HDD (outermost)

**Timescale:** Across sessions and months  
**Question:** Are we solving the right problem?  
**Grounding:** Eric Ries Build-Measure-Learn  
**Enforcement:** All inner loop work is meaningless if HDD says wrong problem. Phase transitions require HDD review before re-sequencing backlog.

### HDD Toolkit

| Tool | When to use |
|------|-------------|
| SWOT analysis | Inception, phase transitions, strategic decisions |
| CD3 + SWOT prioritisation | Backlog sequencing |
| Build-Measure-Learn cycle | Validating hypotheses with real users |
| Phase gate review | Before committing to next roadmap phase |

### SWOT in the HDD Loop

SWOT is a first-class HDD tool. See [`/framework/cd3-swot.md`](./cd3-swot.md) for full protocol.

**When to run SWOT:**
- New product inception
- New bounded context proposed
- Phase transition
- Strategic decision with unclear risk/opportunity profile
- CD3 prioritisation of high-uncertainty items

**SWOT outputs are stored in:** `/docs/swot/swot-[product-slug]-[topic]-[date].md` in the relevant product repo.

---

## Session Protocols as Loop Mechanics

Session protocol files are not admin — they are the mechanical expression of loops 3 and 4:

| File | Loop |
|------|------|
| `session-startup.md` | DDD (context recovery) + HDD (hypothesis check) |
| `session-insession.md` | BDD (trigger map) + DDD (domain integrity) |
| `session-closedown.md` | DDD (document decisions) + HDD (measure, update hypothesis) |

**Rule:** Fetch `session-startup.md` in full before any work. Fetch `session-closedown.md` in full at end. No exceptions.
