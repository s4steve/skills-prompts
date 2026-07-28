---
name: carefortis-adr
description: Creates and publishes Architecture Decision Records (ADRs) for CareFortis to Confluence. Use this whenever Steve is making, documenting, or revisiting an architecture-level or infrastructure-level decision — comparing technical alternatives, choosing a vendor or library, deciding on a data storage or compliance approach, or explicitly saying "document this decision," "let's write an ADR," "why did we choose X," "should we revisit Y," or "should we switch from X to Y." Also trigger when Steve references a past technical choice and asks for the reasoning behind it — check Confluence for an existing ADR before assuming none exists. Do not use this for feature or bug specs (see carefortis-spec for those) — this skill is specifically for capturing the reasoning behind infrastructure, architecture, and technical trade-off decisions.
---

# Carefortis ADR Builder

This skill captures Architecture Decision Records (ADRs) for CareFortis: not just what was decided, but the constraints, alternatives, and trade-offs behind it, so the reasoning survives past the person who made the call.

**Always run this as an interactive session for new ADRs.** Don't fabricate alternatives or constraints the user hasn't stated. An honest gap ("only one option was considered") is more useful than an invented one. See `assets/adr-template.md` for the field-by-field philosophy behind this template.

---

## Step 0: Determine the mode

1. **New decision** — being made now or was recently made and needs to be captured.
2. **Revisit / lookup** — Steve is asking why a past decision was made. Search Confluence first (Step 1) before assuming nothing exists.
3. **Supersede** — a previous ADR's decision is being reversed or changed. Find the original, mark it Superseded, link forward.

Ask if it's ambiguous:
> "Is this a new decision to document, or are you asking about one that's already been made?"

---

## Step 1: Pull existing context

Before drafting anything, check what's already documented so the ADR doesn't contradict or duplicate it.

1. Search for an existing "Architecture Decisions" index page under Engineering (page ID `24608774`) using `searchConfluenceUsingCql` with `cql: space = Carefortis AND title ~ "Architecture Decisions"`.
2. If found, list its children with `getConfluencePageDescendants` to see existing ADR numbers and titles. This gives you the next ADR number and surfaces directly related prior decisions.
3. If it doesn't exist yet, this is the first ADR — create the index page in Step 4.
4. Pull whichever current-state architecture page is relevant (see `references/confluence.md` for known page IDs: Technical Architecture, Infrastructure, Tech Stack, HIPAA Technical Compliance, AI Platform Overview). Use it as ground truth for current state. Don't let the ADR draft conflict with it.

---

## Step 2: Interview

Work through these one at a time, not all at once. Don't move to drafting until each section has an answer or an explicit "unknown."

**Context**
- "What problem forced this decision? What was happening that made it unavoidable right now?"
- "What constraints were you under? Compliance surface area, budget, team size, deadline, existing tech debt — be specific."

**Decision**
- "State the decision in one sentence."

**Alternatives**
- "What else did you seriously consider? For each one, why did it lose, concretely, not just 'more complex.'"
- If only one option was considered: "That's fine. Just say so. Don't invent alternatives to look thorough."

**Trade-offs**
- "What are you giving up by choosing this? If you don't know yet, say so. That's a real answer."

**Reconsideration triggers**
- "What specific, concrete condition would make you revisit this? Not 'if it stops working,' a number, an event, a threshold."

If Steve doesn't know an answer, don't block. Mark it explicitly as unknown/TBD in the draft rather than inventing something plausible.

---

## Step 3: Draft and confirm

Assemble the draft using the structure in `assets/adr-template.md`. Assign the next ADR number from Step 1, or ADR-001 if this is the first.

Present the full draft in chat and ask:
> "Does this look right? Anything to change before I publish it to Confluence?"

Make requested edits. Do not publish without explicit confirmation. This becomes a durable team record, not a scratch note.

---

## Step 4: Publish to Confluence

See `references/confluence.md` for the full publishing workflow: target space and parent page, HTML template, numbering, and known page IDs for cross-linking.

After publishing, confirm:
> "✅ ADR-XXX published: [page URL]"

---

## Step 5: Offer to cross-link

Ask, don't do this automatically:
> "Want me to add a line linking back to this ADR from [the relevant architecture page]? I won't edit it without your OK."

If yes, use `updateConfluencePage` to append a short reference, not a rewrite, to the existing page, e.g. "See ADR-XXX for the reasoning behind this." Show the exact addition before writing it.

---

## Handling supersession

If this ADR replaces an earlier one:
1. Update the old ADR's Status to `Superseded by ADR-YYY` (new page version, don't delete history).
2. Set the new ADR's Related field to reference the old one.
3. Confirm both edits with Steve before publishing, same as any existing-page edit.

---

## Reference Files

- `assets/adr-template.md` — the ADR field structure and the reasoning behind each field
- `references/confluence.md` — space and page IDs, HTML body template, numbering convention, publishing steps
