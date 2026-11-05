# LOOM as a Company — the Executive Operating System (v0.4 draft)

> **Premise:** Justin holds every C-suite seat: CEO, CIO, CTO and Chief AI Officer. He leads top-down.
> LOOM staffs every office beneath him, and the strategy covers the **entire bill of materials (BOM)**, from the ground (compute, data, models) up to product, go-to-market and the sales and value review.
> `BLUEPRINT.md` explains how LOOM runs; this file explains **how LOOM runs like a company**.

---

## 1. You hold every title. LOOM staffs every office.

| Office | Seat Justin holds | LOOM agent (the staff) | Accountable for | BOM layers |
|---|---|---|---|---|
| **Office of the CEO** | CEO | **Chief of Staff** (the LOOM Orchestrator) | Vision, priorities, cadence, the Monday brief, cross-office conflicts | All |
| **Strategy** | CEO / CAIO | **Strategist** | Thesis, bets, objectives, portfolio choices, signals | Strategy cascade |
| **Technology** | CTO | **Architect** | The ground-up stack: platforms, data, models, tools, agents; reuse and technical debt | L0–L4 |
| **Information & Governance** | CIO | **Steward** | Standards, naming, security, responsible AI, data boundary, compliance | L7 (cross-cutting) |
| **Product** | CEO / CPO | **Product Lead** (+ each project's orchestrator) | Portfolio roadmap, problems worth solving, users, value propositions | L5 |
| **Delivery & Operations** | COO / CTO | **Weaver** (build) + **Operator** (run) | Shipping, reliability, support, kit and factory health | L6 |
| **Finance** | CFO | **Treasurer** | Cost by layer and product, budgets, value and ROI | Cost and value of every layer |
| **Market** | CMO / CRO | **Market Lead** | Positioning, audiences, adoption, pricing or value model, sales and value review | L8–L9 |
| **The Board** | (independent) | **Challenger** | Dissent on Decide items; quarterly board review of strategy and results | All |

**Rules for the staff**
- Every office proposes; only the CEO decides Decide-tier items.
- Offices may disagree in writing. The Chief of Staff surfaces disagreements; it does not resolve them for Justin.
- Each office owns a section of the BOLT and two or three KPIs (section 6).

## 2. Top-down: the strategy cascade (the golden thread)

Every piece of work traces up to the vision. Every result traces back down.

```
VISION          why LOOM / Justin's AI practice exists                    strategy/vision.md        (annual)
  └ STRATEGY    thesis + bets (B1, B2 …)                                  strategy/bets.md          (annual, reviewed quarterly)
     └ OBJECTIVES  quarterly OKRs per bet (O1.1, O1.2 …)                 strategy/okrs/2026-Q4.md  (quarterly)
        └ PORTFOLIO   products and platforms that deliver the OKRs (P1…)  portfolio/portfolio.yaml  (quarterly)
           └ PRODUCT     roadmap per product                              each repo: .loom/brief.md (monthly)
              └ RELEASE     milestones / releases                         each repo: milestones     (weekly)
                 └ WORK        issues and PRs                             each repo: issues         (daily)
```

**Traceability rules**
- An issue without a release, a release without a product, a product without an objective, or an objective without a bet is an **orphan**, and orphans show as gaps on the BOLT.
- A bet with no objective this quarter is **dormant**: either revive it or retire it at the quarterly review.

## 3. The full BOM: from ground to sales review

Each layer has an owning office, a catalog of approved components in `stack/catalog.yaml`, standards, and measures. Every product declares its own BOM in its brief, using component IDs from the catalog.

| Layer | What it covers | Owner | Example components (catalog IDs) | Measures |
|---|---|---|---|---|
| **L0 Ground** | Compute, cloud, runners, identity and access, environments, cost centers | Architect | `cmp.github-actions`, `cmp.azure-sub-personal`, `idn.fine-grained-pat` | Uptime, cost per month |
| **L1 Data** | Sources, pipelines, storage, quality, classification, lineage | Architect + Steward | `dat.fabric-lakehouse`, `dat.public-feeds` | Freshness, quality, classification coverage |
| **L2 Models** | Foundation models, model routing, fine-tunes, evals | Architect | `mdl.copilot-default`, `mdl.foundry-<model>` | Eval scores, cost per call |
| **L3 Tools & Context** | MCP servers, connectors, skills, knowledge, prompts | Architect | `mcp.github-remote`, `skl.mosaic-book` | Reuse count, tool error rate |
| **L4 Agents & Orchestration** | Agents, agentic workflows, handoffs, autonomy levels | Architect + Weaver | `agt.loom-orchestrator`, `wf.loom-census` | Task success, veto rate |
| **L5 Product** | The product: problem, users, experience, roadmap | Product Lead | `P1 PRISM: Microsoft`, `P2 mosaic-book` | Problem fit, roadmap delivery |
| **L6 Delivery & Ops** | CI/CD, releases, monitoring, incidents, support | Weaver + Operator | `ops.loom-pulse`, `ops.pages` | Lead time, change failure, incidents |
| **L7 Governance & Risk** *(cross-cutting)* | Security, responsible AI, data boundary, compliance, IP | Steward | `gov.secret-scanning`, `gov.masco-boundary` | Open risks, policy exceptions |
| **L8 Go-to-market** | Audiences, positioning, value proposition, channels, enablement, adoption plan | Market Lead | `gtm.mpe-team`, `gtm.leadership-brief` | Reach, activation |
| **L9 Sales & Value review** | Pipeline or demand, adoption, retention, revenue or value realised, feedback into strategy | Market Lead + Treasurer | `rev.monthly-review` | Adoption, value realised, retention, ROI |

**What the BOM gives the CEO**
- **Roll-up cost and value** by layer, product and bet (Treasurer).
- **Reuse and concentration risk**: which components carry many products; a single point of failure is visible (Architect).
- **Layer gaps**: a product with no L8 plan is a project, not a product; a bet whose products have no L9 measure is unproven.
- **Change impact**: when a signal hits a component (say a model is retired), the BOLT shows every product and bet affected.

The per-product BOM follows the emerging AI-BOM idea (an inventory of the models, data, tools and dependencies in an AI system). LOOM keeps it in YAML so agents and the BOLT can read it.

## 4. "Customers" and "sales" for a company of one

LOOM's products can have two kinds of market. The Market Lead tracks both with the same review.

| Market | Customers | "Sales" means |
|---|---|---|
| **Internal adoption** | Teams, leaders and peers who use what Justin builds | Commitments, active users, adoption, time or cost saved, sponsorship won |
| **External** (only if and when cleared) | Outside buyers or communities | Pipeline, revenue, retention |

**Boundary note (Decide tier):** Any product built in a personal capacity and offered externally, or built from Masco work, must be checked against Justin's Masco employment, IP and outside-activity terms before any external go-to-market. Until then, L8–L9 track internal adoption and personal-brand value only.

## 5. Operating cadence (the company calendar)

| Rhythm | When | Chaired by | What gets decided | Inputs |
|---|---|---|---|---|
| **Weekly exec review** | Mondays 1:00 PM ET | Justin (CEO) | Decide items, escalations, priorities for the week | Monday brief, BOLT |
| **Monthly business review (MBR)** | First Monday review of each month, extended | Justin | Per-product: roadmap, BOM changes, cost vs. value, sales/adoption review | Briefs, Treasurer roll-up, Market review |
| **Quarterly business review + board** | First Monday of each quarter | Justin, Challenger as board | OKRs set and scored, portfolio changes (start / stop / scale), bet changes, autonomy changes | Strategist and Treasurer packs, Challenger review |
| **Annual strategy refresh** | Once a year | Justin | Vision, thesis, bets for the year | Everything above, a year of HARVEST |

Each office prepares its own one-page section; the Chief of Staff assembles the pack. Justin should never need to ask for a report.

## 6. Office KPIs (shown on the BOLT's executive view)

| Office | KPIs |
|---|---|
| Chief of Staff | Idea → decision time · decisions per review · interrupts per week |
| Strategy | % of bets with an active objective · % of OKRs on track · signals answered |
| Technology | Component reuse rate · eval pass rate · tech-debt items open |
| Governance | Open risks by severity · boundary exceptions · secrets/alerts open |
| Product | Roadmap delivery vs. plan · products with a clear problem and user |
| Delivery & Ops | Lead time · change failure rate · stale briefs |
| Finance | Cost per product per month · value realised · ROI by bet |
| Market | Adoption / active users · stakeholder commitments · value stories told |
| Board | Decide items challenged · Challenger calls later proven right |

## 7. Portfolio management

`portfolio/portfolio.yaml` lists every product and platform with: bet and objective served, stage, BOM summary, monthly cost, value measure, and a quarterly **start / stop / scale / sustain** recommendation from the Strategist and Treasurer, challenged by the Board.

WIP limit stays at **3 active products** unless the quarterly review raises it.

## 8. Open questions (v0.4)

1. External products: is selling (now or ever) in scope, or is "sales" strictly internal adoption for now?
2. Should the monthly business review be its own slot, or an extended first-Monday review (current default)?
3. Fiscal calendar: calendar quarters (current default) or Masco's fiscal quarters?
4. Who are the first "customers" for each current product?
