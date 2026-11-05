---
# .loom/brief.md - the project's PM handoff to LOOM. Machine-readable header, human body.
# Maintained by the Project Orchestrator. Updated in the same PR as any change to plan, scope or milestones.
project: mosaic-book
updated: 2026-11-02            # LOOM flags the project stale after 14 days
phase: dev                     # idea | charter | dev | pilot | prod | sunset
health: green                  # green | amber | red (with reason below)
serves_bets: [B1]              # IDs from LOOM strategy/bets.md - this is how strategy traces to execution
autonomy_level: L1
kit_version: v0.1.0
milestones:
  - { id: M1, name: "[TBD]", target: "[TBD]", status: done }
  - { id: M2, name: "[TBD]", target: "[TBD]", status: in-progress }
  - { id: M3, name: "Production", target: "[TBD]", status: planned }
next_3: ["[TBD]", "[TBD]", "[TBD]"]
risks:
  - { risk: "[TBD]", impact: medium, mitigation: "[TBD]" }
decisions_needed:              # surfaces in the Monday brief
  - { ask: "[TBD]", tier: decide, by: "[TBD]" }
value:                         # outcomes, not activity
  measure: "[TBD: what value this delivers]"
  current: "[TBD]"
cost:
  monthly_estimate: "[TBD]"    # Copilot requests, Actions minutes, cloud
product:                       # L5
  portfolio_id: P2
  objective: "[O1.x]"          # quarterly OKR this serves (golden thread)
bom:                           # component IDs from LOOM stack/catalog.yaml, by layer
  L0: [cmp.github-actions]
  L1: []
  L2: [mdl.copilot-default]
  L3: [mcp.github-remote]
  L4: []
  L6: [ops.pages]
  L7: [gov.masco-boundary]
go_to_market:                  # L8 - required before phase: pilot
  audience: "[TBD]"
  value_proposition: "[TBD]"
  channel: "[TBD]"
sales_review:                  # L9 - required before phase: prod
  adoption: "[TBD]"
  value_realised: "[TBD]"
  feedback: "[TBD]"
lessons: []                    # harvest candidates - LOOM routes these
---

# mosaic-book - project brief

## Where we are
One paragraph: what changed since the last brief and why it matters.

## Dev → prod plan
How this gets from where it is to production: remaining milestones, the gate for each, what "prod" means here.

## What I need from Justin
Only items that need him. Everything else is handled.
