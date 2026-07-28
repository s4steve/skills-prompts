# FS-XXX: [Feature name]

**Status:** Proposed | Accepted | In Progress | Shipped | Deprecated
**Date:** YYYY-MM-DD
**Related:** [links to ADRs, other specs, Jira Story]

## What it is

A sentence or two. What the feature is, in plain language — not the implementation, the thing itself.

## What it needs to do

The must-have capabilities. Short, concrete bullets, not a design doc. If it doesn't do this, the feature has failed at its purpose.

- Capability one
- Capability two

## Limitations incorporated

Constraints deliberately built *into* the feature's scope — bounded, not absent. The feature does the thing, but with a cap, a narrowed scope, a rate limit, a v1 restriction. Name the limitation and why it's there.

- **Limitation:** why.

If there are none yet, say so — don't invent a limitation to look thorough.

## Deliberately excluded

Capabilities that were considered and explicitly decided *against* — not a limited version of the thing, the absence of it entirely. This is different from Limitations above: a limitation bounds what the feature does; an exclusion is something it doesn't do at all. Keep them separate so future readers can tell "capped" from "not built."

- **Excluded capability:** why.

If nothing has been explicitly excluded, say so.

## Consequences (fill in later, not at spec time)

What actually happened after this shipped. Did the limitation turn out to be too tight? Did an excluded capability turn out to be needed after all? Update this when you learn something — it's what makes this worth reading in a year instead of just another doc nobody opens.
