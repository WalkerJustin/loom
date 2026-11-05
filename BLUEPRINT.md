# LOOM Blueprint — Operating Model v0.3

> **The deal:** Justin acts as the transformational, strategic AI CIO/CTO. He sets intent, makes the calls, and applies taste.
> LOOM does the rest: it senses, frames, proposes, challenges, corrects, executes within its autonomy, and learns. Justin should rarely need to prompt it.
> Status: draft v0.3 (ideation). Companion to `AGENTS.md` (how agents behave) - this file explains *how LOOM runs*.

---

## 1. Roles: the CIO/CTO and the team

| Justin gives | LOOM gives back |
|---|---|
| **Intent** - where we're going and why | **Options** - two or three ways to get there, with a recommendation |
| **Decisions** - on Decide-tier items only | **Execution** - everything below Decide tier, within autonomy levels |
| **Taste** - "that's not us", "more of this" | **Corrections** - drift, conflicts, stale work, and pushback on Justin himself |
| **Attention** - Monday 1 PM, plus rare interrupts | **A brief** - one page that makes the Monday hour count |

LOOM's standing posture: **suggest first, correct openly, never wait to be asked.** It treats Justin's notes and canon as a living draft and offers alternatives rather than enforcing rules blindly.

## 2. How Justin talks to LOOM (the intent protocol)

Justin should be able to drop a one-liner anywhere and walk away. LOOM expands it.

**Accepted inputs:** a GitHub issue in LOOM (any length), a comment on any LOOM/project issue starting with `@loom`, or a note dropped in `ideas/inbox/`. (Later: email-to-self or Teams, via the M365 side.)

**LOOM turns every input into an Intent Card:**

```
INTENT CARD  #123
Said:        "PRISM should cover Azure changes too"
Purpose:     why this matters (inferred, flagged if unsure)
End state:   what "done" looks like
Constraints: canon, guardrails, data boundary that apply
Room:        SPIN | PATTERN | WARP | WEAVE
Tier:        Decide | Review | Log
Next move:   what LOOM will do now, and by when
Assumptions: what LOOM guessed - correct me if wrong
```

**Rule:** LOOM asks Justin **at most one question** per intent. If anything else is unclear, it makes an assumption, states it in the card, and proceeds. Justin corrects by exception.

## 3. The operating loop

Every piece of work moves through the same seven steps. These are the MOSAIC ideals (sense, decide, act, learn) running at a scale of one person.

| Step | What happens | Who |
|---|---|---|
| **1. Sense** | Notice something: Justin's intent, a project signal, an external change, drift | Heartbeat workflows, Orchestrator |
| **2. Frame** | Write the Intent Card; route to a room; assign a tier | Orchestrator |
| **3. Propose** | Options plus a recommendation, as an issue or PR | Room agent (Spinner, Strategist, Steward, Weaver) |
| **4. Challenge** | Case against, alternatives, reversal plan (Decide tier only) | Challenger |
| **5. Decide** | Merge, veto, or let it pass by default | Justin (Decide/Review); none (Log) |
| **6. Act** | Do the work, hand off to a project, release kit | Room agent, project orchestrators |
| **7. Harvest** | What did we learn? Route lessons back to step 1 | Project orchestrators, Orchestrator |

## 4. The heartbeat (what runs without prompts)

Without a heartbeat, agents only act when prompted, so this is the part that makes "rarely prompting" possible. Each beat is a scheduled GitHub Agentic Workflow (natural-language workflow in `.github/workflows/*.md`) with **safe outputs**: agents are read-only and can only write through declared outputs such as "open issue" or "open PR". Tiers map onto safe outputs.

| Beat | When (ET) | Does | Allowed outputs |
|---|---|---|---|
| **Inbox triage** | Daily 6 AM | Turns new inputs into Intent Cards, routes them | Comment, label (Log) |
| **Project pulse** | Nightly | Collects `status.json` from every project, updates the bolt | Commit to `registry/` (Log) |
| **Drift audit** (Steward) | Weekly, Sun night | Checks repos against standards, naming, kit version; finds stale ideas and decisions | Issues (Review) |
| **AI landscape scan** ("PRISM: Industry") | Weekly, Sun night | Scans GitHub Copilot changelog, model and platform releases against current bets | Issue per relevant change (Review) |
| **Monday brief** | Mondays 11 AM | One-page brief for the 1 PM review | Issue + optional email (Log) |
| **Harvest sweep** | Mondays 11 AM | Collects retros and lessons, proposes routing | Issues / PRs (Review) |
| **Quarterly review** | First Monday of quarter | Bets vs. outcomes, autonomy review, canon pruning | PR (Decide) |

Requires a GitHub Copilot plan and a `COPILOT_GITHUB_TOKEN` repository secret for a personal repo. Agentic workflows are early-stage: start with **two beats** (Monday brief, inbox triage) and add one at a time.

## 5. What LOOM corrects (without being asked)

**Drift in the work:**
- **Strategy drift** - a project no longer serves any current bet
- **Standards drift** - a repo deviates from kit standards, or pins a kit 2+ versions behind
- **Naming drift** - names that break the naming stack (e.g., `Prism` vs. `PRISM: <Domain>`)
- **Decision debt** - Decide items waiting more than two Monday reviews
- **Stale work** - ideas untouched for 60 days (propose park), bets without evidence for a quarter

**Drift in Justin** (the part a real team would say out loud):
- **Over-commitment** - more than **3 active projects** (WIP limit); LOOM proposes what to pause
- **Contradiction** - a new intent conflicts with canon or a prior decision; LOOM names the conflict and asks which wins
- **Meta-work trap** - more than **20%** of recent effort spent improving LOOM itself instead of the projects it exists to serve
- **Boundary risk** - intent that would pull Masco data into personal repos (see section 8)

**Correction etiquette:** every correction states *observation → evidence → suggested fix → tier*. No silent fixes to canon or strategy, ever.

## 6. Interruption budget

The Monday 1 PM review is the default channel. LOOM may interrupt outside it **only** for:

1. A guardrail or security breach (secrets, Masco data, unexpected permissions)
2. An external change that breaks a current bet or an active project
3. A Decide item that is blocking active work, after the Challenger review is done

Everything else waits for Monday. If LOOM interrupts more than **twice a week**, the Steward must raise that as a Review-tier issue about LOOM itself.

## 7. What LOOM always knows (context)

Agents load a small, stable context before acting. Keep it short; stale context is worse than none.

| File | Holds |
|---|---|
| `canon/justin.md` | Operating profile: role, how he likes options framed, plain-language style, "alternatives not edicts", sign-off conventions |
| `canon/naming.md` | The naming stack registry: MOSAIC, PRISM: <Domain>, CITADEL and its rooms, LOOM - with rules for new names |
| `strategy/thesis.md` | The AI thesis in one page |
| `strategy/bets.md` | Current bets: now / next / later, each with a success signal |
| `canon/decisions/` | ADR log; agents check it before proposing |
| `registry/projects.yaml` | Every project, its stage, autonomy level, kit version |

The Steward reviews this context quarterly and prunes it.

## 8. Boundaries and safety

**Personal vs. Masco - the most important boundary.** LOOM lives on a personal GitHub account.
- LOOM holds **patterns, strategy, standards and charters** - things that are Justin's thinking.
- LOOM **never** holds Masco data, tenant or app IDs, identities, credentials, internal documents, or code destined for Masco systems.
- Masco implementations (for example, PRISM: Microsoft's Azure build) live in Masco-approved environments. LOOM can hold a sanitized pattern and charter that points to them.
- Before putting any Masco-related work product in a personal repo, confirm it is allowed under Masco policy. This is a Decide-tier gate.

**Kill switch:** adding the label `loom:pause` to the LOOM repo's control issue (or a `PAUSE` file at the root) stops every heartbeat workflow at its first step.

**Budgets:** monthly caps on Actions minutes and Copilot premium requests, tracked on the bolt. A beat that exceeds its budget pauses itself and raises an issue.

**Reversibility:** everything LOOM does is a commit, issue, or PR. Nothing happens outside Git.

## 9. Earned autonomy

Autonomy is earned with evidence, and lost faster than it is gained.

- **Promote:** when a category of Review-tier items passes **10 times in a row without a veto**, the Steward may propose moving it to Log tier. The proposal itself is Decide tier.
- **Demote:** any revert, guardrail breach, or Justin saying "that's not us" on an item drops that category back one level immediately (a Log-tier change, no approval needed to become *safer*).
- **Never auto-promoted:** strategy, naming, and anything touching the Masco boundary.

## 10. LOOM's scorecard (shown on the bolt)

| Measure | What it tells Justin |
|---|---|
| Idea → decision time | Is LOOM making Justin faster? |
| Decisions per Monday review | Is the review the right size? (Target 3-5) |
| Veto rate on Review-tier items | Is LOOM's judgment aligned with his? |
| Corrections accepted | Are LOOM's corrections useful or noise? |
| Lessons harvested → adopted | Is the learning loop real? |
| Interrupts per week | Is LOOM respecting his attention? |
| LOOM-on-LOOM effort share | Is LOOM serving projects, or itself? |

## 11. Failure modes to design against

| Risk | Mitigation |
|---|---|
| Rubber-stamping (approving everything because it's Monday) | Challenger on Decide items; veto rate tracked; quarterly review of passed items |
| Agent spam (too many issues and PRs) | Interruption budget; Monday brief caps itself at one page; Steward audits LOOM's own noise |
| Canon bloat (rules pile up) | Quarterly pruning; every rule must cite the lesson or decision behind it |
| Sycophancy (agents agree with Justin) | Challenger argues even for good proposals; correction etiquette includes Justin |
| Meta-work trap (LOOM becomes the hobby) | 20% cap tracked on the scorecard |
| Boundary leak (Masco data in personal repos) | Section 8 rules; secret scanning; Decide-tier gate |
| Fragile automation | Start with two beats; add one at a time; kill switch |

## 12. Bootstrap plan

| Phase | Weeks | Done when |
|---|---|---|
| **0. Skeleton** | 1 | Repo created; `AGENTS.md`, `BLUEPRINT.md`, Orchestrator and Challenger agents in place; repo rules set (only Justin merges) |
| **1. Seed the warp** | 1-2 | `canon/justin.md`, `canon/naming.md`, `strategy/thesis.md`, `strategy/bets.md` drafted from existing material (naming stack, PRISM decisions, MOSAIC docs plan, Leadership OS) and approved |
| **2. First heartbeat** | 2 | Monday brief and inbox triage running; first Monday 1 PM review held |
| **3. First weft** | 3-4 | mosaic-book chartered and handed off through the contract; first status in the bolt |
| **4. Close the loop** | 4-6 | First harvest lesson routed and adopted; drift audit and landscape scan added |
| **5. Earned autonomy** | Ongoing | First promotion proposal based on evidence |

## 13. Repo shape (v0.3)

```
loom/
├── AGENTS.md                 how agents behave
├── BLUEPRINT.md              how LOOM runs (this file)
├── ideas/                    SPIN: inbox/, exploring/, parked/
├── strategy/                 PATTERN: thesis.md, bets.md, leadership/, positions/
├── canon/                    WARP: justin.md, naming.md, principles.md, standards/, decisions/
├── kit/                      WEAVE: instructions/, prompts/, agents/, skills/, mcp/, workflows/
├── contract/                 project.yaml, charter template, definition of done
├── template/                 new-project repo template
├── harvest/                  lessons in, routing decisions out
├── registry/                 projects.yaml, scorecard, bolt (dashboard) source
├── evals/                    eval suites, guardrail policies
└── .github/
    ├── agents/               loom-orchestrator, spinner, strategist, steward, weaver, challenger
    ├── workflows/            heartbeat beats (*.md agentic workflows) + standard CI
    └── copilot-instructions.md
```

## 14. Open questions

1. Where do intents come from besides GitHub - should the M365 side (email-to-self, Teams) feed the LOOM inbox?
2. Does the Monday brief arrive by email, as an issue, or both?
3. WIP limit of 3 active projects - right number?
4. How LOOM's canon relates to the MOSAIC docs-as-code book: link, mirror, or merge?
5. Confirm "PRISM: Industry" as the formal name for the landscape scan (a PRISM instance in the naming stack).

---

## 15. Existing repos (brownfield)

LOOM must see everything Justin already has, not only repos it creates. Existing repos are **observed first and changed last**.

### How LOOM collects their information: pull, via MCP

LOOM reads repos through the **remote GitHub MCP server** (`https://api.githubcopilot.com/mcp/`), in **read-only** mode, with only the toolsets it needs: repos, issues, pull requests, actions, code security, Dependabot, secret protection. Nothing has to be installed in the existing repos for this to work.

Two paths use the same server:
- **In VS Code** (Justin chatting with the LOOM Orchestrator): remote server with OAuth, configured by `kit/mcp/mcp.json`.
- **Unattended** (the heartbeat): the weekly **LOOM Census** agentic workflow (`.github/workflows/loom-census.md`) uses the same server with a read-only token.

### The adoption ladder

| Level | What it means | What changes in the repo | Tier to move up |
|---|---|---|---|
| **0 Observed** | Census sees it and reads health, activity, security counts, AI readiness | Nothing | Automatic |
| **1 Registered** | In `registry/repos.yaml` with room, family, bet and owner confirmed | Nothing (optional `loom` topic) | Review |
| **2 Adopted** | LOOM opens an adoption PR adding `.loom/project.yaml`, `AGENTS.md` pointer to the kit, `.vscode/mcp.json`, and a status step | Metadata files only, no product code | Review (Decide if Masco-related) |
| **3 Native** | Fully on the kit, receives kit sync PRs, sends harvest lessons | As for new projects | Review |

Not every repo should climb the ladder. Old experiments can stay Observed forever; the census just keeps them visible and proposes archiving after 180 idle days.

LOOM still never merges in a project repo. Adoption and sync are proposals; Justin's merge is the approval.

### What the census collects per repo

Identity · activity · CI health · security alert counts (never contents) · AI readiness (AGENTS.md, Copilot instructions, custom agents, MCP config, LOOM manifest, kit version) · adoption level · alignment guess with confidence.

### What Justin does once to make collection work

1. **Create one fine-grained personal access token** owned by his personal account, with **All repositories** (so new repos are included automatically) and **read-only** permissions: Metadata, Contents, Issues, Pull requests, Actions, Dependabot alerts, Code scanning alerts, Secret scanning alerts. Save it in the LOOM repo as the secret `LOOM_READ_TOKEN`. The Steward tracks its expiry date and raises an issue 30 days before.
2. **Connect the remote GitHub MCP server in VS Code** with OAuth, using `kit/mcp/mcp.json`.
3. **Tag anything LOOM should ignore** with the repo topic `loom-exclude`. Optionally tag repos he wants prioritised with `loom`.
4. **Run the census once by hand** and confirm the first registry PR.

### Boundary by construction

The token's resource owner is Justin's personal account, so it cannot read repos in Masco's GitHub organisation even by mistake. If Masco repos should ever be represented, add a hand-written, sanitised entry to the registry (name, purpose, link) - a Decide-tier change.

---

## 16. The BOLT: an always-current CIO dashboard

### Two feeds, because facts and intent come from different places

| Feed | Direction | Carries | Source of truth |
|---|---|---|---|
| **Census** (section 15) | LOOM pulls via MCP | Facts GitHub already knows: activity, CI health, security counts, AI readiness | GitHub itself |
| **Project brief** | Each repo pushes | What only the project knows: plan, dev→prod path, milestones, risks, asks, value, cost, lessons, which bets it serves | `.loom/brief.md` in each repo |

The census can't know a project's plan; the brief can't be trusted for facts. Together they cross-check: a brief that says "green" next to failing CI is flagged.

### How the brief stays current
1. **Repo-level instruction** - `kit/instructions/loom-brief.instructions.md` (applies to every Copilot agent in the repo) requires updating `.loom/brief.md` *in the same PR* as any change to plan, scope, milestones, risk, value or cost.
2. **Project Orchestrator** refreshes it at least weekly and after every milestone.
3. **`loom-pulse` workflow** in every project validates the brief on each PR, warns when it is older than 14 days, and on every merge to `main` pings LOOM.
4. **`bolt-build`** in LOOM rebuilds the dashboard on every ping, on any strategy or registry change, and nightly as a safety net. "Always updated" means **minutes after any merge**.

### What the BOLT shows

| View | Answers | Built from |
|---|---|---|
| **1. Strategy** | What is my AI thesis and which bets are live? | `strategy/thesis.md`, `strategy/bets.md` |
| **2. Implementation** | Which projects serve which bets, and how are they doing? | Briefs' `serves_bets` + health + phase |
| **3. Gaps** | Where are strategy and execution out of line? | Computed (below) |
| **4. Signals** | What is changing in the world that supports or threatens a bet? | `signals/` from the landscape scan and Justin |
| **5. Projects** | One card per project: phase, dev→prod plan, next 3, risks, asks | Each `.loom/brief.md` |
| **6. Decisions** | What needs me on Monday? | Briefs' `decisions_needed` + LOOM Decide items |
| **7. Factory health** | Is the machine working? | Census, kit versions, adoption ladder, scorecard (section 10) |

### Gap detection (computed every build)
- **Bet with no project** - strategy without execution
- **Project with no bet** - execution without strategy
- **Bet with no success evidence** for a quarter
- **Signal threatening a bet** with no response
- **Brief vs. facts mismatch** - says green, CI red; says active, no commits in 30 days
- **Value unmeasured** - project in pilot/prod with no value measure
- **Capacity** - more than 3 active projects, or cost trending over budget

### The threads, checked against the CIO/CTO role

| Thread | Covered by |
|---|---|
| Strategy | PATTERN, view 1 |
| Execution | Briefs, census, views 2 and 5 |
| Gaps | View 3 |
| Signals | View 4 |
| Decisions | View 6, Monday review |
| **Value** | Brief `value` field; gap rule "value unmeasured" |
| **Capacity and cost** | Brief `cost` field; WIP limit; budgets |
| **Risk and boundary** | Brief `risks`; guardrails; census security counts |
| **Leadership and communication** | PATTERN leadership; proposed: a monthly "what to tell leadership" draft from the bolt |
| Learning | HARVEST |

### Signals: built on PRISM, phased in

Signals are the input to strategy, so LOOM does not invent its own sensing: it **consumes PRISM instances**. Every source emits the same signal format (`signals/README.md`), so new sources plug in without changing the dashboard.

| Phase | Sources | Lives where |
|---|---|---|
| **1. Industry (now)** | Public industry signals: vendor and platform changes, model releases, analyst and peer moves. Run as the weekly landscape scan, proposed name **PRISM: Industry** (replaces the working name "PRISM: LOOM") | LOOM `signals/` |
| **2. MOSAIC planned signals (later)** | The PRISM instances already planned under MOSAIC (PRISM: Microsoft first, then others such as business-unit news) | Masco environment |

Phase 1 also proves the PRISM pattern on public data before it carries Masco data, which is itself a MOSAIC proof point.

**The Masco boundary for phase 2** (a Decide-tier choice when the time comes):
1. LOOM receives only a **sanitised digest** of MOSAIC signals (theme, affected bet, effect, no Masco data), written in Justin's words or produced by a Masco-side summariser and approved before it crosses.
2. Or LOOM's signals view **links** to the MOSAIC signal view in its Masco-approved home and copies nothing.

Either way, the signal format is the same, so the strategy and gap views work unchanged.
