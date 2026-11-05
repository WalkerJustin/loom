# LOOM Production Deployment Checklist

**Status:** Ready for go-live  
**Generated:** 2026-11-04  
**Owner:** GitHub Copilot Agent  
**Approval required:** Justin Walker  

---

## Executive Summary

LOOM v0.3 is production-ready. All components are scaffolded, documented, and waiting for GitHub repository configuration and Justin's customization choices. Go-live is a 2-3 hour process: GitHub setup → configure secrets → customize strategy/naming → run first test Intent Card.

**Blockers:** None  
**Risks:** Agentic workflows are early-stage; monitor first two weeks closely  
**Next step:** Justin approves this checklist; Copilot executes deployment  

---

## Pre-Deployment Checklist (for Justin)

- [ ] **Read the key docs** – [`README.md`](README.md), [`AGENTS.md`](AGENTS.md), [`BLUEPRINT.md`](BLUEPRINT.md) (sections 1-3)
- [ ] **Understand the governance model** – Review [`AGENTS.md` section 4](AGENTS.md#4-governance-gate-by-consequence-not-by-step) (tier system)
- [ ] **Confirm data boundary** – You will keep Masco data out of personal repos
- [ ] **Check your PAT** – You have a fine-grained GitHub PAT with access to your personal account
- [ ] **Copilot setup** – GitHub Copilot CLI is installed locally (needed for agentic workflow testing)

**Time to review:** ~30 minutes

---

## Deployment Phase 1: GitHub Repository Setup (Copilot executes)

### 1a. Repository Creation
- [ ] Create GitHub repository `WalkerJustin/loom` (public)
- [ ] Description: "LOOM – Justin's Agent Operating System for AI strategy"
- [ ] Topics: `loom`, `agent-os`, `personal`, `ai-strategy`
- [ ] Initialize with this production repo contents

### 1b. Branch Protection Rules
- [ ] Create rule for `main` branch:
  - [ ] Dismiss stale reviews when new commits pushed
  - [ ] Require code review from me (Justin) before merge? **No** (team of one)
  - [ ] Require status checks to pass? **Yes** (validate all checks)
  - [ ] Require branches to be up to date? **No** (unnecessary for one person)
  - [ ] Include administrators? **No** (Justin is admin, can override if needed)
  - [ ] Restrict who can push to this branch? **Yes** (only Justin)

### 1c. Secrets & Environment Variables
- [ ] Add repository secret: `LOOM_READ_TOKEN`
  - Type: Fine-grained GitHub PAT
  - Scopes: `read:repos`, `read:issues`, `read:pull_requests`, `read:actions`, `read:code_security`
  - Applies to: public repos only (safer than full account access)
- [ ] Add repository secret: `COPILOT_GITHUB_TOKEN` (required for agentic workflows to run)
  - Type: GitHub Copilot token (special token provided by GitHub for CLI agents)
  - Where to get: `gh auth token` if you have Copilot CLI + personal token

### 1d. Pages Setup (optional, for BOLT dashboard later)
- [ ] Enable GitHub Pages
  - Source: Deploy from branch
  - Branch: `main`
  - Folder: `_site/` (or `/` root, depending on build)
- [ ] Leave disabled for now if BOLT dashboard is MVP later

### 1e. Security Settings
- [ ] Enable secret scanning (prevent credential leaks)
- [ ] Enable dependabot security updates (if dependencies in kit)
- [ ] Enable code scanning (if applicable; LOOM is docs/config mostly)

**Time:** ~15 minutes

---

## Deployment Phase 2: LOOM Initial Configuration (Justin + Copilot)

### 2a. Customize Strategy & Naming (Justin required)

These files need personalization before go-live:

| File | What to customize | Time |
|---|---|---|
| [`canon/justin.md`](canon/justin.md) | Your communication style, preferences, decision-making patterns | 15 min |
| [`canon/naming.md`](canon/naming.md) | Naming stack for your projects (domains, tiers, conventions) | 15 min |
| [`strategy/vision.md`](strategy/vision.md) | Annual AI vision for LOOM | 20 min |
| [`strategy/bets.md`](strategy/bets.md) | Replace template with your 3-5 active bets (B1, B2, B3, ...) | 20 min |
| [`strategy/okrs/2026-Q4.md`](strategy/okrs/2026-Q4.md) | Current quarter OKRs (if none yet, mark TBD) | 10 min |

**What's ready (no customization needed):**
- All agent profiles (Orchestrator, Strategist, Steward, Weaver, Challenger, Spinner)
- All governance definitions (tier system, guardrails)
- All templates (charter, brief, project.yaml)
- All documentation (README, AGENTS, BLUEPRINT, COMPANY)

**Time:** ~90 minutes (can defer some to after go-live and iterate)

### 2b. Enable Heartbeat Workflows (Copilot executes, Justin approves)

Two workflows are ready to compile and enable:

1. **Inbox triage** (daily 6 AM ET) – Turn new ideas into Intent Cards
   - [ ] Workflow: [`.github/workflows/loom-inbox-triage.md`](.github/workflows/loom-inbox-triage.md)
   - [ ] Compile: `gh aw compile .github/workflows/loom-inbox-triage.md`
   - [ ] Test dry-run: `gh aw run loom-inbox-triage --dry-run`
   - [ ] Enable: Push compiled workflow to `main`

2. **Monday brief** (Mondays 11 AM ET) – Prepare executive review
   - [ ] Workflow: [`.github/workflows/loom-monday-brief.md`](.github/workflows/loom-monday-brief.md)
   - [ ] Compile: `gh aw compile .github/workflows/loom-monday-brief.md`
   - [ ] Test dry-run: `gh aw run loom-monday-brief --dry-run`
   - [ ] Enable: Push compiled workflow to `main`

**Note:** Agentic workflows require GitHub Copilot CLI and `COPILOT_GITHUB_TOKEN` secret. Test locally before enabling in the repo.

**Time:** ~30 minutes (compile + test + push)

---

## Deployment Phase 3: Test Intent Card Flow (End-to-end verification)

Once the repo is live, run a test Intent Card through the full system:

### Test scenario: "LOOM v0.3 Go-Live" (already prepared)

The file [`ideas/inbox/001-loom-v03-go-live.md`](ideas/inbox/001-loom-v03-go-live.md) contains a complete example Intent Card with:
- Intent statement
- Challenger review
- Routing to room, tier, and next move

### Steps to test

1. **Run inbox triage workflow** (or simulate manually)
   - Expect: Intent Card is triaged, labeled `room:warp`, `tier:decide`, assigned to orchestrator
   
2. **Challenger provides review** (or role-play)
   - Input: Read the pre-written Challenger review in the Intent Card
   - Output: Case against, alternatives, reversal plan all present
   
3. **Justin approves the Decide item** (manual)
   - Justin: Merge the PR or approve the issue (or simulate approval)
   
4. **Orchestrator routes the work** (or simulate)
   - Expected: Open issues in relevant rooms (WARP for standards, WEAVE for kit setup)

5. **LOOM runs** (or note what you'd expect)
   - Expected: Brief in Monday review; decision made; work routed to appropriate agents

**Success criteria:**
- [ ] Intent Card is properly triaged (room + tier + assumptions all correct)
- [ ] Challenger review is complete and persuasive
- [ ] Justin can easily approve or reject
- [ ] Work flows to the right room

**Time:** ~30 minutes (manual simulation) or immediate if workflows are running

---

## Deployment Phase 4: Go-Live (Copilot coordinates)

Once Phase 1-3 are complete:

1. **Push all files to GitHub** – Deploy production repo to WalkerJustin/loom
2. **Verify branch protection** – Main branch is protected, only Justin can merge
3. **Verify secrets** – LOOM_READ_TOKEN and COPILOT_GITHUB_TOKEN are set
4. **Enable Pages** (optional) – BOLT dashboard can be built later
5. **Create first issue** – Open the test Intent Card (#1) in the repo to seed activity
6. **Run first workflows** (optional) – Test inbox triage and Monday brief dry-runs

**Status:** LOOM is live and ready for Justin's first real Intent Card

**Time:** ~30 minutes

---

## Post-Deployment (First 2 weeks)

### Week 1: Prove reliability
- [ ] Run inbox triage daily (observe for errors)
- [ ] Run Monday brief (first brief should land Monday 11 AM ET)
- [ ] File 2-3 real Intent Cards (test different rooms and tiers)
- [ ] Observe agent decisions (are they routing correctly?)
- [ ] Log issues if workflows fail or agents misroute

### Week 2: Optimize & iterate
- [ ] Adjust agent instructions if needed (e.g., if Spinner is over-generating alternatives)
- [ ] Fix naming or strategy if the test run revealed confusion
- [ ] Enable more workflows (drift audit, harvest sweep) if you want them
- [ ] Gather feedback from Justin: "Does this feel right?"

### By end of Q4
- [ ] LOOM running smoothly (no weekly fires)
- [ ] First project launched (LOOM managing a real charter)
- [ ] BOLT dashboard operational (if dashboard is part of strategy)
- [ ] Quarterly review completed (score bets against outcomes)

---

## Customization Checklist (Justin's to-do list)

Before LOOM feels like "yours", personalize these:

- [ ] **Tone & style** – Edit [`canon/justin.md`](canon/justin.md)
- [ ] **Naming conventions** – Edit [`canon/naming.md`](canon/naming.md)
- [ ] **Your vision** – Write [`strategy/vision.md`](strategy/vision.md)
- [ ] **Your bets** – Update [`strategy/bets.md`](strategy/bets.md)
- [ ] **This quarter's OKRs** – Fill [`strategy/okrs/2026-Q4.md`](strategy/okrs/2026-Q4.md)
- [ ] **Copilot scope** – Customize [`.github/copilot-instructions.md`](.github/copilot-instructions.md) if needed (optional)

**Time to personalize:** ~90 minutes; can defer some to after go-live

---

## Known Limitations & Workarounds

| Limitation | Impact | Workaround |
|---|---|---|
| Agentic workflows are v0.1 | May fail or be slow | Monitor closely; escalate via GitHub support; fall back to manual if needed |
| BOLT dashboard is MVP | Registry-only for now | Can ship without Pages; add dashboard UI later when needed |
| No external integrations yet | Can't email/Slack alerts | Manual check of Monday brief; add integrations in Q1 2027 if valuable |
| Single-person team | No external review | Challenger review compensates; otherwise, all decisions rest with Justin |

---

## Rollback Plan

If LOOM isn't working after 2 weeks:

1. **Disable all workflows** – Set schedules to `on: workflow_dispatch` only (manual trigger)
2. **Keep the registry** – Strategy, bets, and project tracking are still valuable
3. **Revert to simpler tool** – Use GitHub Project Board or a spreadsheet
4. **Document lessons** – What didn't work? Why? Feed back into BLUEPRINT

**Recovery time:** < 1 hour (workflows are stateless; no data loss)

---

## Success Metrics (2-week checkpoint)

By end of week 2, LOOM is successful if:

- [ ] Both workflows (inbox triage, Monday brief) run without errors
- [ ] Intent Cards are properly triaged (room + tier assignments are accurate)
- [ ] Zero Masco data boundary violations detected
- [ ] Justin has approved at least one real Decide item
- [ ] At least one project or idea has moved from SPIN to a charter

---

## Questions & Support

- **Workflow not running?** Check `COPILOT_GITHUB_TOKEN` is set; re-run `gh aw compile`
- **Challenger review seems harsh?** That's the point! If you disagree, propose a change; Challenger sections are not laws, they're arguments
- **Registry missing projects?** Census workflow populates it; can add manually if needed
- **Confused about autonomy?** See [`.github/copilot-instructions.md`](.github/copilot-instructions.md#autonomy-levels--gate-requirements)
- **Need to change tiers or governance?** File a Review-tier PR; Steward updates canon/instructions

---

## Sign-Off

**LOOM Production Deployment Checklist v0.3**

| Role | Status | Approval |
|---|---|---|
| **Build & scaffolding** | ✅ Complete | Copilot |
| **Documentation** | ✅ Complete | Copilot |
| **Governance** | ✅ Defined | Awaiting Justin |
| **Customization** | ⏳ Awaiting Justin | Justin |
| **Go-live authorization** | ⏳ Awaiting Justin | Justin |

**Next step:** Justin reviews this checklist and the README; if approved, Copilot executes Phases 1-4.

---

**Generated:** 2026-11-04  
**For:** Justin Walker  
**From:** GitHub Copilot Agent
