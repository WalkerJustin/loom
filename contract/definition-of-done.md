# Definition of Done for LOOM Work

This checklist applies to all work flowing through LOOM: PRs in the LOOM repo itself, PRs in projects, and deployments.

## All PRs (minimum)

- [ ] **Tier label applied** – `tier:decide`, `tier:review`, or `tier:log`
- [ ] **Description explains what and why** – one paragraph
- [ ] **Links to related work** – charter issue (if project), HARVEST lesson (if WARP/WEAVE), strategy/bet (if PATTERN)
- [ ] **Status checks pass** – no red X (required; all checks must pass)
- [ ] **No merge conflicts** – merge to main is clean

## If Decide tier (required before merge)

- [ ] **Challenger review section included** – four parts:
  - Case against
  - Alternatives considered (≥2, including "do nothing")
  - What would change your mind
  - Reversal plan
- [ ] **At least 24 hours since review posted** – wait period for strategy/naming changes
- [ ] **Justin has merged the PR** – only Justin merges to main

## If Review tier (required before merge)

- [ ] **Description is clear** – Justin can understand the change without asking
- [ ] **No objection from Justin by Monday 1 PM ET** – auto-merge at 1:01 PM unless veto posted

## If Log tier (required before commit)

- [ ] **Brief description in commit message** – one line
- [ ] **No sensitive data** – no secrets, Masco data, or credentials
- [ ] **Status checks pass** – all green

---

## For PRs that change code (all tiers)

- [ ] **Tests written or updated** – every code change has a test
- [ ] **All tests pass locally** – you ran them
- [ ] **No breaking changes** without Review tier discussion
- [ ] **No unused imports or dead code** – clean slate
- [ ] **Code style matches the project** – run linter if one exists

## For PRs that change scope/plan (all projects)

- [ ] **`.loom/brief.md` updated in the same PR** – never separate
- [ ] **`updated` date set to today** – LOOM uses this to detect staleness
- [ ] **`serves_bets` accurate** – does this still serve the bet(s) listed?
- [ ] **`decisions_needed` updated** – only genuine Decide/Review items

## For PRs that change strategy/bets/naming (Decide tier)

- [ ] **Challenger review complete** – four parts filled in
- [ ] **Evidence cited** – HARVEST lessons, project briefs, external signals
- [ ] **Reversibility clear** – how do we back out if this is wrong?
- [ ] **Impact understood** – how many projects does this change affect?

## For PRs to kit releases (Review tier, Steward + Weaver)

- [ ] **Changelog written** – what's new, breaking changes, deprecations
- [ ] **Migration guide** – for projects using the old version
- [ ] **Evals updated or added** – new or changed functionality has eval baselines
- [ ] **Auto-sync PRs prepared** – ready to open in all affected projects after merge

## For PRs that route HARVEST into WARP/WEAVE (Review tier)

- [ ] **Source cited** – which project/lesson is this from?
- [ ] **Change is reversible** – it's a canon/kit addition or clarification, not a rewrite
- [ ] **Timing is right** – wait for pattern (don't over-generalize from one project)

---

## For project repositories (in addition to above)

### `.loom/project.yaml` and `.loom/brief.md`

- [ ] **`kit_version` pinned** – not floating; specified down to patch
- [ ] **`autonomy_level` set** – L0, L1, L2, or L3 (defaults to L1)
- [ ] **`serves_bets` filled in** – which bets does this project serve? (at least one)
- [ ] **`data_classification` set** – personal | internal | confidential
- [ ] **`stage` is current** – idea | charter | active | paused | done | archived
- [ ] **`definition_of_done` points to this file** or project-specific override

### Before marking a project as **done**

- [ ] **Retro completed** – team reflected on what was learned
- [ ] **Lessons filed** – what should feed back into WARP/WEAVE?
- [ ] **Handoff clear** – if maintenance is needed, who owns it?
- [ ] **Brief set to `stage: done`** – LOOM knows this work is complete

---

## Special: Security & Data Boundary

- [ ] **No secrets in code** – use GitHub Secrets instead
- [ ] **No Masco data** – not even filenames, tenant IDs, or internal references
- [ ] **No credentials in PR description** – use private notes if needed
- [ ] **Secret scanning enabled** – if in a project repo
- [ ] **If boundary violation detected** – file Decide-tier issue immediately; escalate to Justin

---

## Questions?

- **Is my work done enough to merge?** Run through this checklist. If you check all boxes for your tier, merge.
- **Do I need all of these?** Yes, for your tier. If a section doesn't apply, mark N/A.
- **What if I can't pass a check?** File an issue explaining the blocker. Don't merge incomplete work.

---

**Definition of Done v0.3 – active, applies to all LOOM work**  
**Last updated:** 2026-11-04  
**Owner:** LOOM Steward, LOOM Weaver
