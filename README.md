# skills-prompts

Personal library of skills, prompts, automations, and notes for working with AI systems (Claude, ChatGPT, Cursor, Gemini, etc.).

## Layout

```
skills/       Claude Code skills — one directory per skill, skills/<name>/SKILL.md
              with frontmatter. Install by symlinking or copying into ~/.claude/skills.
prompts/      Reusable prompts as plain markdown, tool-neutral. If a prompt needs
              tool-specific variants, keep them side by side (foo.claude.md, foo.gpt.md).
automations/  Hooks, scripts, scheduled agents, and workflow configs.
knowledge/    Notes, patterns, and references on working with AI systems.
```

## Contents

- `skills/feature-brainstorm` — structured brainstorming session that funnels from product areas to a shortlist of buildable features, written to a markdown file.
- `skills/steve-blog` — voice and style guide for writing "Schrodingers Engineer" blog posts.
- `skills/mockup-redesign` — build a page section from an Illustrator mockup, with a pre-flight checklist (layout, background, photos, icons) and a fixed verification workflow (typecheck, lint, screenshot diff, tests, commit).
- `skills/carefortis-adr` — creates and publishes Architecture Decision Records for CareFortis to Confluence, capturing the constraints, alternatives, and trade-offs behind a decision.

## Conventions

- One file (or skill directory) per thing; the filename is the title.
- Prompts start with a one-line comment saying what the prompt is for and any variables to fill in (`{{like_this}}`).
- Skills follow the Claude Code format so they work as-is:

  ```markdown
  ---
  name: my-skill
  description: One line describing when to use it.
  ---

  Instructions...
  ```

## Installing a skill

```sh
ln -s "$(pwd)/skills/<name>" ~/.claude/skills/<name>
```
