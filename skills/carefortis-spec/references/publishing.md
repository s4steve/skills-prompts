# Publishing Reference — Carefortis Feature Specs

## Authentication

No credential setup required. The Atlassian MCP server handles authentication automatically. Never prompt for API tokens, environment variables, or credentials.

## Site

- **cloudId:** `carefortis.atlassian.net`
- **Space:** `Carefortis`

## Confluence target location

- **Parent Page:** `Features` (page ID `76152833`).
- Each spec is a child page of `Features`, titled `FS-XXX: <feature name>`.
- Search for this page by title before assuming an ID is stale — don't create duplicates.

## Numbering

Query children of the Features page (`getConfluencePageDescendants` on `76152833`). Parse existing titles matching `FS-\d+`. Next number = max + 1, zero-padded to 3 digits (FS-001, FS-002, ...). If no children exist, start at FS-001.

## Confluence page HTML template

Use `contentFormat: "html"` when calling `createConfluencePage`, parent ID `76152833`. Build the body as:

```html
<p><span data-type="status" data-color="yellow">Proposed</span></p>
<p><strong>Date:</strong> {date}</p>
<p><strong>Related:</strong> {links to ADRs, other specs, Jira Story}</p>

<h2>What it is</h2>
<p>{a sentence or two}</p>

<h2>What it needs to do</h2>
<ul>
  <li>{must-have capability}</li>
</ul>

<h2>Limitations incorporated</h2>
<ul>
  <li><strong>{limitation}:</strong> {why}</li>
</ul>

<h2>Deliberately excluded</h2>
<ul>
  <li><strong>{excluded capability}:</strong> {why}</li>
</ul>

<h2>Consequences</h2>
<p><em>To be filled in after the feature has shipped and been live for a while.</em></p>
```

Status macro `data-color` values: green = Accepted, yellow = Proposed, blue = In Progress, purple = Shipped, neutral = Deprecated.

## Title convention

`FS-XXX: <feature name>`

## Jira target

- **cloudId:** `carefortis.atlassian.net` (same as Confluence — shared Atlassian site)
- **Project:** `CA` (Carefortis-app), project ID `10099`
- **Issue type:** `Story`, issue type ID `10003`

Create with `createJiraIssue`. Keep the description short — the Confluence page is the source of truth:

- **Summary:** `FS-XXX: <feature name>`
- **Description:** 2-4 sentences covering what the feature is and what it needs to do, plus a link to the Confluence spec page (e.g. "Full spec: {Confluence URL}"). Do not duplicate the limitations/exclusions lists in Jira — that's what the link is for.

After creating the issue, add its URL back into the Confluence page's **Related** field (edit the page you just created, before considering the spec fully published).

## Order of operations

1. Create the Confluence page first (under `76152833`).
2. Create the Jira Story, with its description linking to the new Confluence page URL.
3. Update the Confluence page's **Related** field to include the Jira issue URL/key.

## Error handling

| Situation | Resolution |
|---|---|
| Features page (`76152833`) fetch fails | Fall back to `searchConfluenceUsingCql` with `cql: space = Carefortis AND title = "Features"`. If still missing, ask Steve — don't create a new top-level page without confirming location. |
| FS number collision (concurrent edits) | Re-fetch children, recompute next number, confirm with Steve before publishing |
| Title already exists | Ask Steve: new version, or different title? |
| Jira project/issue type unclear for a given feature (e.g. it's really infra, not app) | Ask Steve rather than defaulting silently — CA is the default but not the only project (CI, PROD also exist) |
| Cross-link target page (ADR, other spec) fetch fails | Ask Steve for the correct page rather than guessing |
