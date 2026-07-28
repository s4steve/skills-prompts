# ADR-XXX: [Decision in one line, phrased as a choice]

**Status:** Proposed | Accepted | Superseded by ADR-YYY | Deprecated
**Date:** YYYY-MM-DD
**Related:** [links to Confluence architecture pages, Jira tickets, other ADRs]

## Context

What problem forced this decision. What was happening in the product or business that made this unavoidable right now, not theoretical.

Constraints at the time. Be specific: compliance surface area, budget ceiling, team size, deadline pressure, existing tech debt. If you had two engineers and a HIPAA audit in six weeks, say that. This is the part that goes stale fastest and matters most later, because it explains why a decision that looks wrong in hindsight was right given what you knew.

## Decision

State it plainly. One paragraph. No hedging.

## Alternatives considered

For each one you seriously evaluated, not a straw man:

- **Option A:** Why it lost. Be concrete. "Slower" or "more complex" is not a reason. "Would have required a second BAA and added 3 weeks to the compliance review" is a reason.
- **Option B:** Same.

If you only considered one option, say so and say why. That's a real answer and it's more honest than inventing alternatives after the fact.

## Trade-offs accepted

What you're giving up. Every decision costs something. Name it. If you don't know yet, say "unknown, revisit after production load" rather than leaving it blank.

## Reconsideration triggers

Specific, falsifiable conditions that mean revisit this decision. Not "if it stops working." Examples: "if PHI-touching data volume exceeds 50GB/month," "if Philter's maintainer goes dark for 6 months," "if we hire a third backend engineer and this becomes a bottleneck."

If you can't write a concrete trigger, that's a signal the decision needs more thought, not that this section is optional.

## Consequences (fill in later, not at decision time)

What actually happened after this shipped. Update this when you learn you were wrong, or right for the wrong reason. This is the field that makes ADR-XXX worth reading in a year instead of just another doc nobody opens.
