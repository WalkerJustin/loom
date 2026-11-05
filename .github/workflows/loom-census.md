---
# LOOM Census - GitHub Agentic Workflow (draft; compile with `gh aw compile`)
# Verify field names against the current gh-aw reference before first run.
on:
  schedule:
    - cron: "0 3 * * 1"        # Mondays 3 AM UTC (Sunday night ET) - ahead of the 11 AM brief
  workflow_dispatch:            # run on demand
permissions:
  contents: read
  issues: read
  pull-requests: read
  actions: read
tools:
  github:
    mode: remote
    read-only: true
    toolsets: [repos, issues, pull_requests, actions, code_security, dependabot, secret_protection]
    github-token: ${{ secrets.LOOM_READ_TOKEN }}   # fine-grained PAT, read-only, all repos you own
safe-outputs:
  create-pull-request:          # updates registry/ in LOOM only (Log tier)
    title-prefix: "[census] "
    labels: [loom, "tier:log"]
  create-issue:                 # findings that need a decision (Review tier)
    title-prefix: "[census] "
    labels: [loom, "tier:review"]
    max: 5
---

# LOOM Census

You are LOOM's census taker. Read `AGENTS.md`, `BLUEPRINT.md` (section 15) and `canon/naming.md` first.

## Scope
Every repository owned by the account that owns this repo, **except** repos with the topic `loom-exclude`, archived repos, and forks you have not changed.

## For each repo, collect
1. **Identity** - name, description, visibility, default branch, topics, created date.
2. **Activity** - last push, open issues, open PRs, latest release.
3. **Health** - result of the latest workflow run on the default branch.
4. **Security** - counts of open Dependabot, code scanning and secret scanning alerts, where available. Counts only; never copy alert contents.
5. **AI readiness** - presence of `AGENTS.md`, `.github/copilot-instructions.md`, `.github/agents/`, `.vscode/mcp.json`, `.loom/project.yaml`, and the pinned LOOM kit version if any.
6. **Adoption level** - Observed, Registered, Adopted or Native (BLUEPRINT section 15).
7. **Alignment guess** - which room, family (MOSAIC / PRISM / CITADEL / standalone) and current bet it likely serves, with a confidence of high, medium or low.

## Outputs
- One PR updating `registry/repos.yaml` and `registry/census-latest.md` with the table above.
- An issue (Review tier) only for: a repo never seen before, a repo whose alignment confidence is low, a repo idle for 90+ days, a naming-stack violation, or any open critical/high security alert.
- If nothing changed since last week, update the date in `census-latest.md` and stop.

## Never
- Write to any repo other than LOOM.
- Copy source code, secrets, alert details, or anything that looks like Masco data into LOOM. If you see Masco data in a personal repo, open a Review issue titled "Boundary check" naming the repo only.
