# LOOM Naming Stack (TBD – customize)

This file defines naming conventions across all LOOM projects, products, and domains. Consistency is governance.

## Core Names (unchanging)

| Name | Category | Use | Example |
|---|---|---|---|
| **LOOM** | System | The operating system itself | `github.com/WalkerJustin/loom` |
| **MOSAIC** | Strategy/Product family | Docs-as-code orchestration; orchestration philosophy | `mosaic-book`, `MOSAIC: Ethics` |
| **PRISM** | Product family | Research, analysis, and positioning on AI topics | `PRISM: Microsoft`, `PRISM: Agents` |
| **CITADEL** | Project family | [TBD – or remove if not used] | [TBD] |
| **BOLT** | Dashboard | LOOM's central dashboard; shows strategy → execution → outcomes | Part of `loom` repo; deployed to GitHub Pages |

## Domain Convention (for products and tools)

**Pattern:** `<FAMILY>: <Domain>`

- **MOSAIC:** applied to building/architecture
  - `MOSAIC: Platform` – platform orchestration
  - `MOSAIC: Ethics` – responsible AI orchestration
  - `MOSAIC: Book` – docs-as-code

- **PRISM:** applied to analysis/intelligence
  - `PRISM: Microsoft` – analysis of Microsoft AI direction
  - `PRISM: Agents` – analysis of agent patterns in AI
  - `PRISM: Industry` – broad industry signals (models, platforms, regulations)

- **CITADEL:** [TBD – for what domain? or retire if unused?]

## Project IDs (kebab-case, lowercase)

Repository names are lowercase, kebab-cased. Use domain suffix if part of a family.

**Examples:**
- `mosaic-book` – the MOSAIC book repo
- `prism-microsoft` – PRISM: Microsoft project repo
- `loom` – the LOOM system itself
- `loom-agents` – shared agent library (if needed)

**Never:**
- Use CamelCase in repo names (`mosaic-book`, not `MosaicBook`)
- Use abbreviations without context (`p-01`, not helpful)
- Mix naming styles in the same family

## Strategy/Bet IDs

**Pattern:** `B[number]` – B1, B2, B3, etc.

- B1, B2, B3 are active bets (see `strategy/bets.md`)
- Referenced in `.loom/brief.md#serves_bets` to trace projects to strategy
- Used in portfolio view to show which products serve which bets

## Product/Portfolio IDs

**Pattern:** `P[number]` – P1, P2, P3, etc.

- P1, P2, P3 are active products in the portfolio (see `portfolio/portfolio.yaml`)
- Referenced in `.loom/brief.md#portfolio_id`
- Products are tracked separately from projects; a project (short-term work) may feed a product (long-term offering)

## OKR IDs

**Pattern:** `O[bet-number].[objective-number]` – O1.1, O1.2, O2.1, etc.

- O1.1, O1.2 are objectives under bet B1
- See `strategy/okrs/2026-Q*.md` for current OKRs
- Referenced in `.loom/brief.md#objective`

## Agent Names

**Pattern:** Descriptive role; use in agent handoff labels and tooling

| Agent | ID | Shorthand | Example handoff |
|---|---|---|---|
| LOOM Orchestrator | `loom-orchestrator` | `@loom` | "Draft charter" |
| Spinner | `spinner` | `@spinner` | "Brainstorm alternatives" |
| Strategist | `strategist` | `@strategist` | "Quarterly bet review" |
| Steward | `steward` | `@steward` | "Audit standards drift" |
| Weaver | `weaver` | `@weaver` | "Prepare project handoff" |
| Challenger | `challenger` | `@challenger` | (auto-required on Decide PRs) |

## Tier Labels (GitHub labels)

**Pattern:** `tier:<level>`

| Tier | Label | Approval | Examples |
|---|---|---|---|
| Decide | `tier:decide` | Justin (after Challenger) | Strategy, bets, charters, Masco data |
| Review | `tier:review` | Proceed by default | Kit releases, standards, project ADRs |
| Log | `tier:log` | None | Idea capture, status notes, docs |

## Room Labels (GitHub labels)

**Pattern:** `room:<name>`

| Room | Label | Purpose |
|---|---|---|---|
| SPIN | `room:spin` | Ideation; routed to Spinner |
| PATTERN | `room:pattern` | Strategy; routed to Strategist |
| WARP | `room:warp` | Standards & governance; routed to Steward |
| WEAVE | `room:weave` | Factory & kit; routed to Weaver |
| HARVEST | `room:harvest` | Learning loop; routed to Orchestrator |

## Autonomy Levels

**Pattern:** `L[0-3]` – L0, L1, L2, L3

- **L0** – Advise only (read-only)
- **L1** – Draft and propose (Justin merges)
- **L2** – Routine auto-merge (after checks)
- **L3** – Delegated (full autonomy in scoped area)

Used in `project.yaml#autonomy_level` and `.github/copilot-instructions.md`.

## Data Classification

**Pattern:** `classification:<level>`

| Level | Visibility | Where it can exist | Examples |
|---|---|---|---|
| **personal** | Public (default) | `WalkerJustin/*` repos | Justin's AI strategy, LOOM, learnings, public positions |
| **internal** | Private / org only | `WalkerJustin/*` repos | Strategy, bets, business plans |
| **confidential** | Locked down | Masco org only | Masco code, customers, IP, financials |

Used in `project.yaml#data_classification`.

---

## How to extend the naming stack

If you need a new family, domain, or convention:

1. **Document it here** – add to this file with pattern and examples
2. **Get Challenger review** – this is Decide tier (naming is foundational)
3. **Update canon/principles.md** if the principle changes
4. **Notify all projects** – reference the change in the Monday brief and any existing repos
5. **Audit compliance** – Steward's drift audit checks for violations

---

**Naming stack v0.3 – awaiting customization**  
**Last updated:** 2026-11-04  
**Owner:** Justin Walker, Steward
