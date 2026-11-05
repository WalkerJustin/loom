# LOOM — Justin's Agent Operating System

> **LOOM is the front door to Justin's AI strategy and AI leadership team of one.**
> 
> It exists to move MOSAIC, his AI strategy, and his GitHub Copilot practice forward faster than a committee could, without losing the discipline a committee provides.

**Status:** Production v0.3 (active)  
**Owner:** Justin Walker  
**Repository:** https://github.com/WalkerJustin/loom

---

## Quick Start

### First time here?
1. Read [`AGENTS.md`](AGENTS.md) – understand the five rooms and how they work
2. Read [`BLUEPRINT.md`](BLUEPRINT.md) – how LOOM operates day-to-day (heartbeat, corrections, decisions)
3. Read [`COMPANY.md`](COMPANY.md) – the full organizational operating model
4. See [`canon/principles.md`](canon/principles.md) – ten principles that guide the whole system

### Contributing an idea?
- Drop it in [`ideas/inbox/`](ideas/inbox/) or create a GitHub issue
- Tag it with a room guess: `room:spin`, `room:pattern`, `room:warp`, `room:weave`, or `room:harvest`
- The **LOOM Orchestrator** triages it daily and turns it into an Intent Card

### Merging changes?
- Label every PR with its tier: `tier:decide`, `tier:review`, or `tier:log`
- **Decide-tier** PRs require a Challenger review (red-team section with case against, alternatives, reversal plan)
- **Review-tier** PRs proceed unless Justin objects by the next Monday review
- **Log-tier** PRs merge directly
- Only Justin merges to `main`

---

## The Five Rooms

| Room | Purpose | Folder | Tier | Agent |
|---|---|---|---|---|
| **① SPIN** | Ideation: raw ideas, explorations, alternatives | [`ideas/`](ideas/) | L2 | Spinner |
| **② PATTERN** | AI strategy: thesis, bets, leadership POV, roadmap | [`strategy/`](strategy/) | L0-L1 | Strategist |
| **③ WARP** | Standards & governance: naming stack, gates, canon | [`canon/`](canon/) | L1 | Steward |
| **④ WEAVE** | The factory: kit, contracts, templates, handoffs | [`kit/`](kit/) [`contract/`](contract/) [`template/`](template/) | L1-L2 | Weaver |
| **⑤ HARVEST** | Learning loop: lessons from projects routed back | [`harvest/`](harvest/) | L1 | (Orchestrator) |

---

## Key Files

### Core
- **[`AGENTS.md`](AGENTS.md)** – Every agent's role and rules (6 agent profiles + governance)
- **[`BLUEPRINT.md`](BLUEPRINT.md)** – Operating model, heartbeats, cadence, autonomy levels
- **[`COMPANY.md`](COMPANY.md)** – Full organizational structure, BOM, KPIs, cadence

### Strategy (PATTERN room)
- **[`strategy/bets.md`](strategy/bets.md)** – Active bets, horizons, success signals
- **[`strategy/vision.md`](strategy/vision.md)** – Annual vision (TBD - customize)
- **[`strategy/okrs/`](strategy/okrs/)** – Quarterly OKRs

### Governance (WARP room)
- **[`canon/principles.md`](canon/principles.md)** – 10 principles that guide LOOM
- **[`canon/naming.md`](canon/naming.md)** – Naming stack and conventions (TBD - customize)
- **[`canon/justin.md`](canon/justin.md)** – Justin's preferences and style (TBD - customize)

### Factory (WEAVE room)
- **[`contract/project.yaml`](contract/project.yaml)** – Project manifest template (every project repo uses this)
- **[`contract/brief.template.md`](contract/brief.template.md)** – Project brief template
- **[`contract/charter.template.md`](contract/charter.template.md)** – Charter template (TBD - create)
- **[`kit/`](kit/)** – Shared templates, instructions, MCP config, evaluation baselines

### Agents (.github)
- **[`.github/agents/`](.github/agents/)** – Agent profiles (orchestrator, challenger, specialists)
- **[`.github/workflows/`](.github/workflows/)** – Heartbeat workflows and automations

### Registry & Dashboard (BOLT)
- **[`registry/projects.yaml`](registry/projects.yaml)** – All tracked projects (TBD - auto-generated)
- **[`registry/repos.yaml`](registry/repos.yaml)** – Census of all repos (TBD - auto-generated)
- **[`registry/census-latest.md`](registry/census-latest.md)** – Latest census summary (TBD - auto-generated)

---

## Governance & Gates

### Tier System (gate by consequence, not by step)

| Tier | Approval | Visibility | Examples |
|---|---|---|---|
| **DECIDE** | Justin only (after Challenger review) | All Monday reviews; 24h wait | Strategy changes, new charters, Masco data, published content |
| **REVIEW** | Justin may veto; default is proceed | Weekly review agenda | Kit releases, project ADRs, HARVEST routing |
| **LOG** | None | Commit + BOLT | Idea capture, status updates, docs |

### The Challenger (required for Decide tier)

Every Decide-tier PR must include a **Challenger review** section with:
1. **Case against** – strongest honest argument not to do this
2. **Alternatives considered** – at least two options (including "do nothing")
3. **What would change your mind** – observable signals proving wrong
4. **Reversal plan** – how to back out

---

## Operating Cadence

| Rhythm | When | Chair | What |
|---|---|---|---|
| **Weekly exec review** | Mondays 1:00 PM ET | Justin | Decide items, escalations, priorities |
| **Monday brief** | Mondays 11:00 AM ET | Orchestrator | One-page summary of pending decisions |
| **Inbox triage** | Daily 6:00 AM ET | Orchestrator | New ideas → Intent Cards |
| **Project pulse** | Nightly | Automated | Collect `.loom/brief.md` from all projects |
| **Drift audit** | Sundays | Steward | Standards, naming, kit version checks |
| **Quarterly review** | Q1/Q2/Q3/Q4 kickoff | Justin + Challenger | OKRs, bets, autonomy levels |

---

## Safety & Boundaries

### Data Classification

Every piece of work declares its data level in its charter/brief:
- **personal** – Justin's personal AI practice, can be public
- **internal** – organizational strategy, visibility limited to Justin
- **confidential** – anything from Masco: data, code, identities, tenants

**Hard rule:** No Masco data, identities, tenants, or credentials ever in personal repos. Boundary violations trigger an immediate Decide-tier veto.

### Guardrails

- **Secret scanning** – enabled on main branch
- **Copilot instructions** – defined in `.github/copilot-instructions.md`
- **BOLT secrets check** – census flags any Masco data exposure
- **Autonomy gates** – agents cannot raise their own autonomy level

---

## How to Contribute (different roles)

### If you're a project building in LOOM

1. Create a `charter.md` and `.loom/project.yaml` in your repo (use templates from [`contract/`](contract/))
2. Pin your LOOM kit version in `project.yaml`
3. Keep `.loom/brief.md` current (updated weekly, same PR as any scope/plan change)
4. In your retro, flag lessons for [`harvest/`](harvest/) routing back to canon/kit

### If you're an agent orchestrator (for new projects)

1. See the handoff checklist in the latest Monday brief
2. Run the Project Orchestrator agent to prepare repository setup
3. Create the repo from the template; populate the charter and `project.yaml`
4. Open a PR to add the project to `registry/projects.yaml`

### If you're contributing to LOOM itself

1. **Canon changes** – propose in a PR with Decide tier (Challenger review required)
2. **Kit releases** – propose in a PR with Review tier (open until Monday or veto)
3. **Naming stack updates** – Decide tier (naming is foundational)
4. **Agent instructions** – submit as a PR; label `tier:review` if new, `tier:log` if fixing bugs

---

## First Steps for Justin (Customization Checklist)

Before going live, personalize these files:

- [ ] **[`canon/justin.md`](canon/justin.md)** – Add your communication style, tone, preferences
- [ ] **[`canon/naming.md`](canon/naming.md)** – Define the naming stack for your projects (domains, tiers, conventions)
- [ ] **[`strategy/vision.md`](strategy/vision.md)** – Write your annual AI vision
- [ ] **[`strategy/bets.md`](strategy/bets.md)** – Replace template with your 3-5 active bets (B1, B2, B3, ...)
- [ ] **[`strategy/okrs/2026-Q4.md`](strategy/okrs/2026-Q4.md)** – Current quarter OKRs
- [ ] **[`.github/copilot-instructions.md`](.github/copilot-instructions.md)** – Define autonomy boundaries and tool restrictions (TBD - create)
- [ ] **GitHub repository settings:**
  - [ ] Set branch protection: `main` – require status checks, only you can merge
  - [ ] Add team: create `@WalkerJustin/loom-team` if using subagents
  - [ ] Secrets: add `COPILOT_GITHUB_TOKEN` (fine-grained, personal account)
  - [ ] Pages: enable, use `main` branch, `/ (root)` folder for BOLT dashboard
  - [ ] Enable secret scanning, Dependabot security updates
  - [ ] Topics: `loom`, `agent-os`, `personal`, `ai-strategy`

---

## Heartbeat Workflows (GitHub Copilot Agentic)

LOOM's autonomy comes from scheduled workflows that sense, propose and execute within guardrails.

**Currently enabled (MVP):**
- **Inbox triage** – 6 AM daily (via `.github/workflows/loom-inbox.md`)
- **Monday brief** – 11 AM Mondays (via `.github/workflows/loom-brief.md`)

**Ready to enable (when tested):**
- Drift audit (Steward) – Sundays 11 PM
- Project pulse (Orchestrator) – nightly (read-only)
- Harvest sweep (Orchestrator) – Mondays 11 AM

**Compile with:** `gh aw compile loom-inbox.md` (requires `gh` CLI v2.61+)

---

## Architecture & Tech Stack

| Layer | Component | Source |
|---|---|---|
| **L0 Ground** | GitHub Actions, GitHub Copilot, Azure (opt) | `stack/catalog.yaml` |
| **L2 Models** | Copilot (Claude, GPT, etc.), custom fine-tunes | `stack/catalog.yaml` |
| **L3 Tools** | MCP (GitHub, Copilot, Azure, custom) | `kit/mcp/mcp.json` |
| **L4 Agents** | LOOM Orchestrator, room agents, project orchestrators | `.github/agents/` |
| **L6 Delivery** | GitHub Pages (BOLT dashboard), Actions CI/CD | `.github/workflows/` |
| **L7 Governance** | Secret scanning, RBAC, data classification | `.github/copilot-instructions.md` |

---

## What Success Looks Like

✓ Ideas turn into decisions in days, not weeks  
✓ Every project traces back to a current bet  
✓ Standards are enforced, not discussed  
✓ Learning from projects feeds back into strategy  
✓ Justin rarely needs to prompt; LOOM suggests  
✓ Dissent is built in (Challenger); no echo chamber  
✓ MOSAIC ideals (sense, decide, act, learn) run on a team of one  

---

## Open Questions & Future

See [`AGENTS.md` section 9](AGENTS.md#9-open-questions-v02) for open design questions.

Near-term roadmap:
- [ ] BOLT dashboard (GitHub Pages static site from registry + briefs)
- [ ] Azure infrastructure dashboard (if BOLT dashboard runs on Azure)
- [ ] Kit v1.0 release and first project repo using full kit
- [ ] Quarterly strategy review automation
- [ ] Harvest → canon/kit proposal automation

---

## Getting Help

- **Confused about a room?** Start with [`AGENTS.md`](AGENTS.md) (the guide to each room)
- **How do I propose something?** See [`BLUEPRINT.md`](BLUEPRINT.md) section 2 (intent protocol)
- **What tier is my change?** See [`AGENTS.md`](AGENTS.md) section 4 (governance)
- **How are decisions made?** See [`BLUEPRINT.md`](BLUEPRINT.md) (operating loop and cadence)
- **What are the constraints?** See [`COMPANY.md`](COMPANY.md) (BOM, layers, guardrails)

---

**LOOM v0.3 – draft, active, evolving.**  
Owner: Justin Walker  
Questions? File an issue in `ideas/inbox/` or start a GitHub discussion.
