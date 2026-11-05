---
applyTo: "**"
description: Keep the LOOM project brief current. Applies to every Copilot agent and chat in a LOOM project repo.
---

# Keep `.loom/brief.md` current

This repo reports to LOOM through `.loom/brief.md` (format: LOOM `contract/brief.template.md`). LOOM's dashboard and Justin's Monday review read it.

**In the same pull request**, update `.loom/brief.md` whenever you:
- change scope, plan, milestones, or a target date
- finish or start a milestone
- discover a risk, or a decision only Justin can make
- change what value the project delivers, or its cost
- learn something other projects should know (add it under `lessons`)

Always:
- set `updated` to today's date
- keep `serves_bets` accurate; if the work no longer serves any bet, say so in "Where we are"
- keep `decisions_needed` to genuine Decide/Review items
- write for a CIO: outcomes and asks, not activity logs
- never include secrets, tenant/app IDs, credentials, or Masco data

If a PR changes none of the above, do not touch the brief.
