# LOOM — Agent Operating Guide

> **LOOM is the front door to Justin's AI strategy and AI leadership team of one.**
> It exists to move MOSAIC, his AI strategy, and his GitHub Copilot practice forward faster than a committee could, without losing the discipline a committee provides.
> Status: **draft v0.3 (ideation)**. Owner and sole approver: Justin.
> LOOM runs like a company with Justin in every C-suite seat; offices, the strategy cascade and the full BOM are in `COMPANY.md`.
> How LOOM runs day to day (heartbeat, corrections, interruption budget, earned autonomy) is in `BLUEPRINT.md`. Read it before acting.

---

## 1. Purpose

LOOM is personal and unique to Justin. It is not an enterprise process and does not need to scale to other people. Its job:

1. **Agility** - get ideas from spark to decision to working project in days, not quarters.
2. **Coherence** - one strategy, one naming stack, one set of standards across everything Justin builds.
3. **Proof** - demonstrate the MOSAIC ideals (sensing, orchestration, learning loops) on a team of one before they are proposed anywhere else.

## 2. The rooms

Every request enters through the **LOOM Orchestrator** (the front door), which works out what kind of work it is and routes it.

| Room | Purpose | Folder | Agent |
|---|---|---|---|
| ① SPIN | Ideation: raw ideas, explorations, alternatives | `ideas/` | Spinner |
| ② PATTERN | AI strategy and AI leadership: thesis, bets, roadmap, positions, point of view | `strategy/` | Strategist |
| ③ WARP | Standards and governance: naming stack, standards, gates, autonomy, decision log, guardrails | `canon/` | Steward |
| ④ WEAVE | The factory: kit, contract, template, handoff to project repos | `kit/` `contract/` `template/` | Weaver |
| ⑤ HARVEST | The learning loop: lessons from projects routed back into the rooms | `harvest/` | (front door) |
| BOLT | One dashboard across all rooms and projects | `registry/` | (automated) |
| - | Dissent on every Decide-tier proposal | - | **Challenger** |

An idea can end as: parked, a note, a strategy change, a standard, a PRISM instance, or a project. Most ideas should not become projects.

## 3. Vocabulary

| Term | Meaning |
|---|---|
| Warp | The fixed foundation: canon, standards, naming |
| Weft | A project repo |
| Shuttle | An orchestrator carrying work through the warp |
| Draft | A charter plus its `project.yaml` |
| Selvage | Guardrails and evals |
| Bolt | The dashboard |

Folders use plain names; the vocabulary is for concepts and agents.

## 4. Governance: gate by consequence, not by step

Every action is sorted by **how hard it is to undo** and **how far it reaches**. Agents must label every proposal with its tier.

### Tier 1 - DECIDE (Justin must approve)
Hard to reverse, or changes the foundation.
- Changes to the AI thesis, strategy bets, or leadership point of view
- Renaming or retiring an established name in the naming stack
- Raising any autonomy level
- New project charters
- Anything touching Masco data, identities, tenants, or secrets
- Anything published, posted, or sent to other people

**Requirements:** a Challenger review attached (section 5) · strategy and naming changes wait at least 24 hours after the Challenger review before merge · nothing happens until Justin merges.

### Tier 2 - REVIEW (Justin may veto)
Reversible, but worth knowing about.
- Kit releases and new standards wording
- Project-level decisions and ADRs
- HARVEST lessons routed to WARP or WEAVE

**Mechanics:** the agent proceeds unless Justin objects. Open items are listed in the Weekly LOOM Review. Default veto window: **until the next Weekly LOOM Review** (open question - see section 9).

### Tier 3 - LOG (no approval)
Cheap to undo.
- Idea capture, notes, explorations
- Status updates, retro filings
- Documentation edits, formatting

**Mechanics:** committed directly; visible on the bolt.

### When unsure
Pick the higher tier and say why. Never split one Decide-tier change into several smaller changes to avoid review.

## 5. The Challenger

Required on every **Decide-tier** proposal. Not required on Review or Log.

The Challenger writes, in the proposal itself:
1. **The case against** - the strongest honest argument not to do this.
2. **Alternatives considered** - at least two, including "do nothing."
3. **What would change Justin's mind** - observable signals that would mean this was wrong.
4. **Reversal plan** - how to back out if it fails.

The Challenger argues; it does not decide. Its job is to replace the pushback a real strategy team would give.

## 6. Cadence

| Rhythm | When | What |
|---|---|---|
| **Weekly LOOM Review** | **Mondays, 1:00 PM ET** | The bolt lists every pending Decide item, open Review items, and new HARVEST lessons. Justin decides in one sitting. |
| Quarterly strategy review | First Monday review of each quarter | The Strategist compares bets with outcomes, using HARVEST evidence. |
| Ad hoc | Anytime | Justin can decide any item early; the review is the latest point, not the only one. |

The orchestrator prepares a one-page review brief before each Monday session.

## 7. Autonomy by room

| Room | Autonomy | Why |
|---|---|---|
| SPIN | High (L2) | Ideas should flow; capture is Log tier |
| PATTERN | Low (L0-L1) | Strategy and leadership are Justin's judgment |
| WARP | Low (L1) | The foundation changes deliberately |
| WEAVE | Medium (L1-L2) | Routine kit work can move; releases are Review tier |
| Projects | Set per project in `project.yaml` | Starts at L1 |

Levels: **L0** advise only · **L1** draft PRs, Justin merges · **L2** auto-merge low-risk paths after checks · **L3** auto-merge in a scoped area with evals as the gate.

## 8. GitHub mechanics for a team of one

- **The merge is the approval.** Do not rely on "required approving reviews": in a single-person setup they can block Justin from approving PRs he asked an agent to open. (Verify against current GitHub rules.)
- Use repository rules instead: required status checks must pass; only Justin can merge to `main`.
- Tier labels on every PR: `tier:decide`, `tier:review`, `tier:log`.
- Decide-tier PRs fail a check if the Challenger section is missing.

## 9. Open questions (v0.2)

- Veto window for Review-tier items: until next Monday review (current default) or a fixed 48 hours?
- AI leadership: stay inside PATTERN, or become its own room?
- Kit distribution: template + sync workflow (current plan) vs. submodule vs. package.
- Dashboard: GitHub Project board first, Pages site later?
- How LOOM's canon relates to the MOSAIC docs-as-code book: link, mirror, or merge.
