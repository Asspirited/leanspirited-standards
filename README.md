# LeanSpirited Standards

Shared orchestration standards, session protocols, and delivery framework documentation for all LeanSpirited products.

**Owner:** LeanSpirited (Tom Roden / Rod)  
**Applies to:** All repos under github.com/Asspirited

---

## Repos using these standards

| Repo | Product | Status |
|------|---------|--------|
| Asspirited/cusslab | Cusslab / Heckler and Cox | Active |
| Asspirited/your-green-gardening-wizard | Your Green Gardening Wizard | Active |
| Asspirited/risk-and-impact-assessor | RIA | Active |

---

## Contents

### Delivery Framework
- [`/framework/four-loops.md`](./framework/four-loops.md) — TDD-BDD-DDD-HDD framework
- [`/framework/cd3-swot.md`](./framework/cd3-swot.md) — CD3 prioritisation + SWOT integration

### Session Protocols
- [`/protocols/session-startup.md`](./protocols/session-startup.md) — Mandatory session start sequence
- [`/protocols/session-insession.md`](./protocols/session-insession.md) — Mid-session trigger map
- [`/protocols/session-closedown.md`](./protocols/session-closedown.md) — Mandatory session end sequence

### Claude Orchestration
- [`/claude/claude.md`](./claude/claude.md) — Master Claude orchestration instructions

### Backlog Standards
- [`/standards/backlog-format.md`](./standards/backlog-format.md) — Backlog item format, Gherkin conventions, prefix registry

### Architecture Patterns
- [`/architecture/patterns.md`](./architecture/patterns.md) — Shared architecture decisions (ACL, per-agent state, etc.)

---

## How to use in a product repo

Each product repo contains a `.claude/claude.md` that begins:

```
# [Product Name] — Claude Orchestration
# Standards reference: github.com/Asspirited/leanspirited-standards
# Local overrides and product-specific context below.
```

Session protocol files in `.claude/` reference the standards repo for shared sequences and add product-specific triggers.

---

## Updating standards

1. Raise a backlog item in the relevant product repo with prefix `STD-`
2. PR to `leanspirited-standards` main
3. Update the `CHANGELOG.md` with date and summary
4. Notify affected repos — update their `.claude/` reference comments
