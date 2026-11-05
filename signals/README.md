# Signals

One file per signal: `signals/YYYY/YYYY-MM-DD-short-slug.md`. Any PRISM instance (or Justin) can write one. The BOLT reads the header; humans read the body.

```yaml
---
id: S-2026-001
source: "PRISM: Industry"        # any PRISM instance, or "Justin"
observed: 2026-11-02
title: "[What changed, in one line]"
type: vendor                     # vendor | platform | model | regulatory | industry | business
link: "[public URL, if any]"
classification: public           # public | sanitised   (never internal)
affects:
  - { bet: B1, effect: supports }        # supports | threatens | new-option | watch
confidence: medium               # low | medium | high
recommended_action: "[What LOOM suggests: none, watch, propose bet change, open idea]"
response: open                   # open | answered (link to decision/idea) | dismissed
---
Two or three sentences in our own words: what happened and why it matters to the bet.
No copied articles, no Masco data.
```

**Rules**
- A signal with `effect: threatens` and `response: open` for more than two Monday reviews becomes a gap on the BOLT.
- `classification: sanitised` is only allowed for phase-2 MOSAIC digests that Justin has approved (Decide tier).
- Signals are evidence, not decisions: changing a bet is still a PATTERN proposal through the Challenger.
