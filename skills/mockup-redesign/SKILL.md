---
name: mockup-redesign
description: >
  Use when redesigning or rebuilding a page section of the website from an Adobe
  Illustrator export or mockup screenshot (e.g. Care Compass, Organizations, or any
  future page/section). Reuses existing Storybook components, keeps copy in
  src/content, and runs a fixed pre-flight checklist plus verification workflow
  (typecheck, lint, dev server + Playwright screenshots, vitest, commit) before
  declaring the section done. Encodes lessons learned from repeated correction
  rounds on prior mockup handoffs. Triggers on "redesign this section from the
  mockup", "match this to designs/...", "build this page section from the
  screenshot/Illustrator export", or handing over a new section of a
  mockup-driven redesign.
---

# Mockup-Driven Page Redesign

Converts an Adobe Illustrator export / mockup screenshot into a page section, reusing
this codebase's existing component library. Most correction rounds on past sections
came from the same handful of mistakes — the Checks below exist to catch them before
reporting the section done, not after.

## Step 1: Gather inputs

Confirm before starting, if not already given:

- **Section name** and which page it belongs to.
- **Path to the reference mockup** (e.g. `designs/CareFortis_Contact Us_v2_Folder`).
- Any known constraints (e.g. must reuse a specific existing component).

## Step 2: Build

- Reuse existing Storybook components wherever possible
  (`src/components/landing/*`, `src/components/ui/*`). If no existing component
  fits, ask for approval before creating a new one — check first whether extending
  an existing component's props solves it instead of a new component.
- Content copy goes in `src/content/[file].ts`, not hardcoded in the section
  component.

## Step 3: Run the checks below before declaring the section done

Report which ones were actually confirmed — not "looks right."

**1. Layout structure, column by column.**
Don't infer the layout from what similar sections elsewhere in the codebase look
like. Look at the reference and identify: is it stacked or side-by-side? What are
the actual column proportions (e.g. `0.35fr/0.65fr`, not a plain `grid-cols-2`)? Is
text left-aligned or centered? Match the reference's structure directly, section by
section — a plausible-looking layout that doesn't match the mockup still needs
fixing.

**2. Section background.**
Check the actual background color/tint of the section against the reference, not
just the content inside it. It's easy to reuse a nearby section's warm/tint
background token out of habit when the mockup actually wants plain white (or vice
versa).

**3. Photo assignment — open every image, don't go by filename.**
If a section assigns photos to cards/slots, use the `Read` tool to actually view
each candidate image before assigning it. Filenames (`providers.jpg`,
`families.jpg`) are not reliable indicators of what's actually in the photo —
verify the visual content matches the card's audience/topic.

**4. Icon-to-label matching — render and look, don't trust names or order.**
When a set of icons maps to a set of labels (steps, features, etc.), convert each
SVG to PNG (`sips -s format png file.svg --out /tmp/file.png`) and view it before
assuming the Nth icon belongs to the Nth label. Icon filenames can be misleading (a
file named `connect.svg` may actually depict the concept that belongs under a
different label). Confirm the semantic match visually.

**5. Icon treatment — check if the SVG is already fully styled.**
Before wrapping an icon in a colored circle, applying a CSS filter (invert,
brightness), or any other container styling, render the raw SVG first. Some icon
assets are already self-contained two-tone/circle designs — wrapping them again
doubles up the circle or destroys the two-tone detail via a filter. Also check
whether a styling treatment actually applies uniformly across all items in a set,
or only to a subset (the reference may deliberately mix plain icons with
circled/badged icons within the same row).

**6. Zoom in on the reference screenshot, not just the full page.**
When the user attaches a screenshot of one section, treat every visual detail in
it as significant — icon shapes, badge colors, number colors, divider styles — not
just the overall layout. Crop your own verification screenshot to the same region
and compare side by side before reporting back.

## Step 4: Verification workflow

1. `npx tsc -b --noEmit` — typecheck.
2. `npx eslint <changed files>` — lint.
3. Start the dev server in the background and poll until it's up:
   ```
   npm run dev -- --port 5183
   curl -sf http://localhost:5183/<route> -o /dev/null
   ```
4. Run the Playwright screenshot script (desktop 1440×900 + mobile 390×844). It
   must scroll through the full page in increments first to trigger `Reveal`'s
   `whileInView` animation before taking the final screenshot — a screenshot taken
   immediately after `goto()` will show blank gaps where Reveal-wrapped content
   hasn't faded in yet. Check for console errors.
5. `Read` the resulting screenshot(s) and compare directly against the reference,
   section by section (see Checks above). Crop to zoom into a specific row/section
   if the detail matters (icon shapes, number colors).
6. `npx vitest run` — confirm the full Storybook/vitest suite still passes.
7. Kill the dev server: `pkill -f "vite --port 5183"`.
8. Commit locally with a descriptive message. **Do not push** unless explicitly
   told to — confirm this standing instruction is still in effect before pushing
   anything to the PR.
