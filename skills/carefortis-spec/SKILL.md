---
name: carefortis-spec
description: Creates and publishes short, concise feature specs for CareFortis, then creates the linked Jira Story. Use whenever Steve is defining, documenting, or scoping a new feature — explicitly saying "document this feature," "let's write a spec," "create a Jira story for X," or describing a feature's purpose, requirements, and scope. Captures what the feature is, what it needs to do, what limitations are deliberately built in and why, and what capabilities were deliberately left out and why. Do not use this for architecture or infrastructure trade-off decisions (see carefortis-adr for those) — this skill is specifically for scoping a feature's requirements and boundaries, not the reasoning behind a technical choice.
---

# Carefortis Feature Spec Builder

This skill captures feature specs for CareFortis in a short, consistent format: not just what the feature does, but the limitations deliberately built into it and the capabilities deliberately left out — so scope decisions survive past the person who made the call, the same way `carefortis-adr` preserves architecture reasoning.

**Always run this as an interactive session for new specs.** Don't invent requirements, limitations, or exclusions Steve hasn't stated. An honest gap ("we haven't decided what's out of scope yet") is more useful than a fabricated one. See `assets/spec-template.md` for the field-by-field philosophy.

The full spec lives on a Confluence page; the Jira Story stays short and links to it — mirrors the pattern in `carefortis-adr`.

---

## Step 0: Determine the mode

1. **New feature** — being scoped now, needs a spec and a Jira Story created.
2. **Revisit / lookup** — Steve is asking what a feature was scoped to do, or why something is limited/excluded. Search Confluence first (Step 1) before assuming nothing exists.
3. **Update existing spec** — scope is changing for a feature that already has a spec. Find the original, update it (new page version, don't delete history), note what changed.

Ask if it's ambiguous:
> "Is this a new feature to spec out, or are you asking about one that's already been scoped?"

---

## Step 1: Pull existing context

Before drafting anything, check what's already documented so the spec doesn't contradict or duplicate it.

1. Search for the "Features" index page using `searchConfluenceUsingCql` with `cql: space = Carefortis AND title = "Features"` (known page ID `76152833` — see `references/publishing.md`).
2. List its children with `getConfluencePageDescendants` to see existing FS numbers and titles. This gives you the next spec number and surfaces directly related prior specs.
3. If the feature depends on or touches a prior architecture decision (e.g. it streams AI responses, touches PHI redaction), check the Architecture Decisions index (page `146472961`) for a relevant ADR to link — don't re-litigate a decision an ADR already made, just reference it.

---

## Step 2: Interview

Work through these one at a time, not all at once. Don't move to drafting until each section has an answer or an explicit "unknown."

**What the feature is**
- "In a sentence or two, what is this feature?"

**What it needs to do**
- "What does this feature need to do? What are the must-have capabilities?"

**Limitations incorporated**
- "What limitations are you deliberately building into this feature, and why?" (e.g. a cap, a rate limit, a narrowed scope for v1)
- These are constraints *within* the feature's scope — the feature does the thing, but bounded.

**Deliberately excluded**
- "What capabilities did you deliberately decide *not* to build, and why?"
- This is different from limitations: these are things the feature does not do at all, not things it does in a bounded way. Keep the two sections separate — conflating them is how specs get skimmed past instead of read.
- If nothing has been explicitly excluded yet: "That's fine. Just say so, don't invent exclusions to look thorough."

If Steve doesn't know an answer, don't block. Mark it explicitly as unknown/TBD in the draft rather than inventing something plausible.

---

## Step 3: Draft and confirm

Assemble the draft using the structure in `assets/spec-template.md`. Assign the next FS number from Step 1, or FS-001 if this is the first.

Present the full draft in chat and ask:
> "Does this look right? Anything to change before I publish it to Confluence and create the Jira Story?"

Make requested edits. Do not publish or create the Jira issue without explicit confirmation.

---

## Step 4: Publish to Confluence, then create the Jira Story

See `references/publishing.md` for the full workflow: Confluence parent page and HTML template, numbering, and the Jira project/issue type to create the Story in, with its description linking back to the Confluence page.

After both are created, confirm:
> "✅ FS-XXX published: [Confluence page URL]
> ✅ Jira Story created: [issue URL]"

---

## Step 5: Offer to cross-link

Ask, don't do this automatically:
> "Want me to add a line linking back to this spec from [the relevant ADR or architecture page]? I won't edit it without your OK."

If yes, use `updateConfluencePage` to append a short reference, not a rewrite, to the existing page. Show the exact addition before writing it.

---

## Reference Files

- `assets/spec-template.md` — the spec field structure and the reasoning behind each field
- `references/publishing.md` — Confluence parent page and HTML template, numbering convention, Jira project/issue type, and publishing steps
