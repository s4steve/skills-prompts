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

- `skills/steve-blog` — voice and style guide for writing "Schrodingers Engineer" blog posts.

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
