# Confluence Publishing Reference — Carefortis ADRs

## Authentication

No credential setup required. The Atlassian MCP server handles authentication automatically. Never prompt for API tokens, environment variables, or credentials.

## Site

- **cloudId:** `carefortis.atlassian.net`
- **Space:** `Carefortis`

## Target location

Default publishing target:
- **Parent Page:** `Architecture Decisions`, a child of `Engineering` (page ID `24608774`).
- If this page doesn't exist yet (first run), create it first with `createConfluencePage`:
  - Title: `Architecture Decisions`
  - Parent ID: `24608774`
  - Body: short index blurb, e.g. "Architecture Decision Records for CareFortis. See individual ADR-XXX pages for the context, alternatives, and trade-offs behind infrastructure and architecture choices."
- Capture the resulting page ID. Search for this page by title before recreating it in future sessions — don't create duplicates.

## Numbering

Query children of the Architecture Decisions page. Parse existing titles matching `ADR-\d+`. Next number = max + 1, zero-padded to 3 digits (ADR-001, ADR-002, ...). If no children exist, start at ADR-001.

## Known architecture pages

For pulling current-state context. Don't edit these without explicit confirmation (see SKILL.md Step 5).

| Page | ID |
|---|---|
| Technical Architecture | 49938461 |
| Carefortis Infrastructure | 13893633 |
| Tech Stack | 2359297 |
| Carefortis Frontend | 52330497 |
| HIPAA Technical Compliance | 103251972 |
| CareFortis AI Platform — Architecture & Strategy Overview | 142049281 |

These IDs are stable but pages can be restructured. If a fetch fails, fall back to `searchConfluenceUsingCql` with `cql: space = Carefortis AND title ~ "<page name>"`.

## Page HTML template

Use `contentFormat: "html"` when calling `createConfluencePage`. Build the body as:

```html
<p><span data-type="status" data-color="yellow">Proposed</span></p>
<p><strong>Date:</strong> {date}</p>
<p><strong>Related:</strong> {links to other ADRs, Jira tickets, architecture pages}</p>

<h2>Context</h2>
<p>{problem that forced this decision}</p>
<p>{constraints at the time: compliance, budget, team size, deadline, tech debt}</p>

<h2>Decision</h2>
<p>{one paragraph, stated plainly}</p>

<h2>Alternatives considered</h2>
<ul>
  <li><strong>{option}:</strong> {why it lost, concretely}</li>
</ul>

<h2>Trade-offs accepted</h2>
<p>{what's given up; "unknown, revisit after production load" is acceptable}</p>

<h2>Reconsideration triggers</h2>
<ul>
  <li>{specific, falsifiable condition}</li>
</ul>

<h2>Consequences</h2>
<p><em>To be filled in after the decision has been live for a while.</em></p>
```

Status macro `data-color` values: green = Accepted, yellow = Proposed, red = Superseded, neutral = Deprecated.

## Title convention

`ADR-XXX: <decision in one line, phrased as a choice>`

Example: `ADR-001: PHI redaction via Philter instead of Adaline`

## Error handling

| Situation | Resolution |
|---|---|
| Architecture Decisions page doesn't exist | Create it under Engineering (24608774) per above, then proceed |
| ADR number collision (concurrent edits) | Re-fetch children, recompute next number, confirm with Steve before publishing |
| Title already exists | Ask Steve: new version, or different title? |
| Cross-link target page fetch fails | Ask Steve for the correct page rather than guessing |
