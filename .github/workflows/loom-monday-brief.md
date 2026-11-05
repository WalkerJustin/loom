---
# LOOM Monday Brief – GitHub Agentic Workflow (compile with `gh aw compile`)
# Runs Mondays at 11 AM ET (15:00 UTC), ahead of the 1 PM exec review.
on:
  schedule:
    - cron: "0 15 * * 1"        # Mondays 11 AM ET (15 UTC)
  workflow_dispatch:             # run on demand
permissions:
  contents: read
  issues: read
  pull-requests: read
  actions: read
tools:
  github:
    mode: remote
    read-only: true
    toolsets: [repos, issues, pull_requests, actions]
    github-token: ${{ secrets.LOOM_READ_TOKEN }}
safe-outputs:
  create-issue:
    title-prefix: "[monday-brief] "
    labels: [loom, "tier:log", brief]
    max: 1
  send-email:
    to: ${{ github.repository_owner }}@github.com
    subject-prefix: "[LOOM] Monday Brief"
---

# LOOM Monday Brief

You are preparing the Monday executive review brief for Justin. Read [`AGENTS.md`](../../AGENTS.md) (section 6), [`BLUEPRINT.md`](../../BLUEPRINT.md) sections 3-4, and [`COMPANY.md`](../../COMPANY.md) section 5 first.

## Your job
Prepare a **one-page executive brief** that makes the 1 PM review productive. This is your only output for this workflow.

## What to include in the brief

1. **Pending Decide items** (must appear before 1 PM ET)
   - List every open PR labeled `tier:decide` (no Challenger review yet, or waiting for merge)
   - Link, title, one-line summary, and "status: [waiting for Challenger review | ready to decide | blocked on]"
   
2. **Open Review items from last week** (veto window: until 1 PM ET this Monday)
   - List every PR labeled `tier:review` that was opened more than 24 hours ago
   - If Justin hasn't objected by 1 PM, these auto-merge
   - Link, title, summary, default action: "→ auto-merge at 1:01 PM unless Justin objects"

3. **New HARVEST lessons** (routed for decision)
   - Any new items tagged `room:harvest` since last Monday
   - One-line summary of each lesson + which project it came from
   - Proposed routing: "send to WARP" (canon change), "send to WEAVE" (kit change), "parked for next cycle"

4. **Top 3 risks or blocks**
   - Any project or bet with status: amber or red
   - One-line summary + what Justin decides about it

5. **Autonomy review** (if quarterly)
   - Quarterly only: proposed autonomy level changes for each agent/room
   - Evidence: track record in the past quarter

6. **Calendar & next moves**
   - What's due this week?
   - What decisions unlock next work?

## Format

```markdown
# Monday Brief – Nov 4, 2026

**Status:** X Decide items pending · Y Review items awaiting decision · Z HARVEST lessons routed

---

## 🔴 Decide items awaiting your merge (1)
- [ ] [PR title here](#link) – [one-line] – Status: ready to merge
- [ ] [PR title here](#link) – [one-line] – Status: waiting for Challenger review (ETA: EOD today)

## 🟡 Review items (auto-merge unless you object) (2)
- [PR title](#link) – [one-line] – Opened: Fri 3pm – auto-merge at 1:01 PM Mon unless vetoed
- [PR title](#link) – [one-line] – Opened: Sun 6pm – auto-merge at 1:01 PM Mon unless vetoed

## 📚 New HARVEST lessons (2)
- Lesson 1: [from project X] – Proposed: send to WARP (canon update)
- Lesson 2: [from project Y] – Proposed: parked for next cycle (needs more evidence)

## ⚠️ Top risks (1)
- **Project P1 – AMBER** – [reason] – Decision needed: [option A | option B | option C]

## 📅 This week
- Mon 1 PM ET: This review (you are here)
- Wed 9 AM ET: [Any decision deadlines?]
- Fri 5 PM ET: [Any check-ins?]

---

**Generated:** [timestamp]
**Workflow:** `.github/workflows/loom-monday-brief.md`
```

## Before you run

Check:
- [ ] At least one Decide item open (or say "no pending decisions this week")
- [ ] All Review-tier PRs from last week are listed
- [ ] Any new HARVEST lessons are routed with clear recommendations
- [ ] Risks are accurate (check project briefs, GitHub status)
- [ ] Links are correct (broken links = wasted Monday time)

## Safety guardrails

- Never include Masco data or secrets
- If a PR has no tier label, flag it: "Missing tier label: [PR link]"
- If a Review PR is older than 1 week, ask: "Should this auto-merge or be closed?"
- If a Decide PR is missing the Challenger review, flag it: "Waiting for Challenger review"

## After 1 PM ET

- Decide PRs that Justin merges → close
- Review PRs that aren't vetoed → auto-merge at 1:01 PM (Steward handles this via status check)
- HARVEST lessons routed → open Review PRs in WARP or WEAVE by end of day

