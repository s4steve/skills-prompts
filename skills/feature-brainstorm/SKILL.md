---
name: feature-brainstorm
description: Walks through a structured brainstorming session that funnels from product areas to feature ideas to a shortlist of specific, buildable features, then writes the result to a markdown file. Product-agnostic — works for any product, not tied to one codebase. Use when exploring what to build next, generating a feature backlog from scratch, identifying product areas worth exploring, or turning a vague "we should think about X" into a concrete feature list. Triggers on phrases like "brainstorm features", "what should we build next", "help me find product ideas", "let's explore feature ideas", "generate a feature backlog".
---

# Feature Brainstorm

This skill runs a structured, convergent brainstorming session: Context → Areas → Ideas → Features → Write. The goal is a concrete deliverable — a shortlist of specific features written to a markdown file, ready to hand to a separate spec/build process. This is not open-ended ideation. Every step narrows toward the shortlist.

**Always run this as an interactive session, one step at a time.** Do not skip ahead or answer for the user. After each step, summarize what was captured and confirm before moving on.

---

## Step 0: Context

Establish what product and space you're brainstorming for before generating anything. Ask:

- "What product or product area are we brainstorming for?"
- "Who are the users, and what do they use it for today?"
- "What prompted this session — a gap you've noticed, a strategic push, a competitive move, or open exploration?"
- "Anything already ruled out or out of scope for this round?"

Keep this tight, 2-4 questions. If the user already stated the product and context in their opening message, don't re-ask what they told you — confirm and move on.

---

## Step 1: Identify Product Areas

Generate a divergent list of product areas: distinct zones of the product where opportunity might exist (e.g. onboarding, collaboration, reporting, mobile, integrations, admin/ops). Aim for 6-10 areas. Cast wide, don't self-censor for feasibility yet.

Present the list. Ask the user to narrow:

> "Which of these do you want to dig into this session? Pick 1-3 — we'll go deep rather than wide."

If the user has an area in mind that wasn't on the list, add it and proceed with that.

---

## Step 2: Generate Ideas Within Each Chosen Area

For each selected area, generate ideas divergently. Quantity over quality here, no evaluation yet.

- Generate 5-8 distinct ideas per area
- Vary along dimensions: scope (quick win vs. big bet), user segment (power user vs. new user vs. admin), mechanism (new capability vs. removing friction vs. automation)
- Use a technique when it helps unlock a stuck moment. Don't force all of them:
  - **Jobs-to-be-done**: "When [situation], the user wants to [motivation] so they can [outcome]." What's currently being hired to do that job badly?
  - **SCAMPER**: substitute, combine, adapt, modify, put to other use, eliminate, or reverse an existing part of the area
  - **Inversion**: "How would we make this area actively worse?" Then flip each answer.
- Present ideas grouped by area. Don't evaluate yet, just lay them out.

---

## Step 3: Converge to a Feature Shortlist

Narrow. Ask the user to react to what's on the table:

> "Which of these are you excited about, skeptical of, or want to combine?"

Then converge together:

- Evaluate against user impact, rough feasibility, strategic fit, and how well-defined the idea already is
- Combine overlapping ideas into a single feature where it makes sense
- Push back if the user wants to keep everything. A shortlist of 15 isn't a shortlist. Aim for 3-8 features genuinely worth specifying next.
- Get each shortlisted feature to a name and a one-sentence description before moving on

---

## Step 4: Structure and Confirm

For each shortlisted feature, capture:

- **Feature name**
- **Product area** (from Step 1)
- **Problem / job statement** — one sentence: "helps [user] do [job] by [mechanism]"
- **Rationale** — why this, why now, 1-2 sentences
- **Rough scope** — S / M / L, gut call, not an estimate
- **Open question** — the biggest unknown, if any (leave blank if none)

Present the full shortlist back to the user in this structure and ask:

> "Does this look right? Anything to cut, merge, or rename before I write it out?"

Make any requested edits before proceeding.

---

## Step 5: Write the Markdown File

Default path: `./brainstorms/{product-slug}-{YYYY-MM-DD}.md`, relative to the current working directory, where `{product-slug}` is the product name from Step 0, lowercased and hyphenated. Confirm before writing:

> "I'll save this to `./brainstorms/{product-slug}-{date}.md` — good, or a different path?"

**Template:**

```markdown
# Feature Brainstorm: [Product Name]
Date: [YYYY-MM-DD]

## Context
[2-3 sentences from Step 0: product, users, what prompted this session]

## Shortlisted Features

### [Feature Name]
- **Area:** [area]
- **Problem:** [problem/job statement]
- **Rationale:** [why this, why now]
- **Rough scope:** S | M | L
- **Open question:** [unknown, or "none"]

[repeat per feature]

## Areas Considered
[list of all areas from Step 1, noting which were explored vs. set aside]

## Ideas Explored But Not Shortlisted
[ideas from Step 2 that didn't make the cut, grouped by area — kept for reference, not lost]
```

After writing, confirm:

> "✅ Saved to [path]. [N] features shortlisted, ready to spec whenever you want to move one forward."

---

## Handling Incomplete Information

If the user doesn't know an answer (rough scope, rationale), don't block on it. Write "TBD" and move on. A shortlist with honest gaps beats one with invented confidence.

If the user wants to stay broad without narrowing to a product area first, let them, but flag it:

> "We can stay broad through Step 2, but we'll need to narrow to specific areas before Step 4 can produce actual features."

## Do Not

- Do not generate the shortlist yourself without the user's input at each narrowing point. The convergence decisions are the user's, not yours.
- Do not skip Step 0. Generic brainstorming without product context produces generic features.
- Do not let the shortlist grow past ~8 without pushing back.
