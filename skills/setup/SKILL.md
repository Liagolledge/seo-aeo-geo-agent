---
name: "setup"
description: "First-run setup for the SEO/AEO/GEO pipeline — interview the user and write their context pack (seo-context.md) so every other skill writes in their voice, for their market, sources and brand. Use when the user says set up, set me up, onboard, get started, configure, first run, 'create my context pack', or when any pipeline skill or the seo-aeo-geo agent finds no seo-context.md and needs one. Also use when the user wants to update or change their existing context (voice, sites, market, sources, brand, tools)."
---

# Setup — build the context pack

Creates or updates `seo-context.md`, the file every skill in this pipeline reads before it runs.
Without it, the pipeline has to guess voice, market, sources and brand, or stop and ask mid-task.
This skill front-loads all of that once.

## When this runs

- On first use of the pipeline, before any content work.
- Whenever a skill or the `seo-aeo-geo` agent reports there's no `seo-context.md`.
- When the user wants to change something in their existing context.

If a `seo-context.md` already exists, read it first and treat this as an edit — confirm what's
there, change only what the user asks, and don't re-interview from scratch.

## How to run the interview

Work from `context.template.md` in the plugin — it lists every field. Don't ask the fields as a
dry form. Ask in plain language, grouped, and **infer what you can** so the user answers less:

- If the project has a website, brand doc, existing posts, or an "about" page, read them first and
  propose draft answers the user just confirms or corrects. Inference the user approves beats a
  blank they have to fill.
- Ask the high-leverage fields properly, and don't let them be skipped with a shrug:
  - **Voice** — get a real writing sample (3–5 sentences they wrote, or a link). This is the single
    strongest signal for sounding like them. A description of the voice is a weak substitute for an
    example of it.
  - **Original material** — what data only they have (client results, numbers, transcripts). This is
    what makes their content citable, so name examples and make it easy to say what they've got.
  - **Market** — because it changes spelling, phrasing, competitors and search volumes.
- Let the low-stakes fields default. Say what the default is rather than forcing a choice: "I'll use
  a neutral placeholder palette for images unless you have brand colours" is better than an
  interrogation.

Keep it to a couple of rounds, not twenty questions. The user can always refine `seo-context.md`
later, and this skill can be re-run to update it.

## Writing the file

Write the completed pack to **`seo-context.md`** in the project root (the skills also check
`.claude/seo-context.md` — use that only if the user keeps their config there). Use the same
headings as `context.template.md` so the other skills find each field.

- Fill every field the interview answered.
- For anything left blank, write the neutral default explicitly and note it's a default, so the
  user can see what the pipeline will assume — e.g. `Colour palette: (none set — neutral placeholder
  palette will be used)`.
- Never invent a value the user didn't give. A labelled default is honest; a fabricated preference
  quietly wrong-foots every later stage.

## After writing

Show the user where the file is and a one-line summary of what's set versus defaulted. Then offer,
in one line, the natural first job: writing a post (the full pipeline via the `seo-aeo-geo` agent),
or a single stage like an outline or an audit.

If setup was triggered because another skill needed the context, hand back to that skill once the
pack is written.
