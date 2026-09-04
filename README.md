# SEO / AEO / GEO Agent

An end-to-end content agent for [Claude Code](https://claude.com/claude-code) that takes a topic
from research to a publish-ready article optimised for three things at once:

- **SEO** — ranking in Google.
- **AEO** — showing up in AI Overviews and featured snippets.
- **GEO** — getting cited inside answers from ChatGPT, Perplexity, Gemini and Claude.

The agent orchestrates a six-skill pipeline. It handles sequencing, state and the approval
gates between stages; each skill holds its own method in full.

| Stage | Skill | Produces |
|---|---|---|
| Frame | `seo-aeo-geo-workflow` | Programme view: technical health, architecture, distribution, measurement |
| 1 | `query-fan-out` | The demand landscape, scored and tiered (`.md` + `.csv`) |
| 2 | `semantic-outline` | The article blueprint |
| 3 | `source-collection` | A mapped source pack plus a gap list |
| 4 | `article-draft` | The first draft |
| 5 | `seo-article-audit` | A verdict plus prioritised, copy-paste fixes |
| 6 | `featured-image` | A production-ready image prompt, alt text and filename |

## What it's good for

- **Write a new post** — run the full pipeline (stages 1–6) with approval gates at the outline and draft.
- **Audit an existing article** — run stage 5 alone for a prioritised list of fixes.
- **Plan a content programme** — run the `seo-aeo-geo-workflow` frame.
- **A single stage** — ask for just an outline, just sources, or just an image.

You don't need to say "SEO" or "AEO". Prompts like *"write a post about X"*, *"why isn't AI citing us"*,
*"get cited by ChatGPT"* or *"audit this article"* all route correctly.

## Install

These are personal (user-level) Claude Code skills and an agent. Copy them into your Claude config:

```bash
# Agent
mkdir -p ~/.claude/agents
cp agents/seo-aeo-geo.md ~/.claude/agents/

# Skills
mkdir -p ~/.claude/skills
cp -R skills/* ~/.claude/skills/
```

Then start (or restart) Claude Code. The agent appears as `seo-aeo-geo`, and each skill can also be
invoked on its own by its bare name (e.g. `query-fan-out`, `featured-image`).

## Structure

```
agents/
  seo-aeo-geo.md            # the orchestrator
skills/
  seo-aeo-geo-workflow/     # programme-level frame
  query-fan-out/            # stage 1
  semantic-outline/         # stage 2
  source-collection/        # stage 3
  article-draft/            # stage 4
  seo-article-audit/        # stage 5
  featured-image/           # stage 6
```

## Notes on customising

This pack is written to be industry-neutral. A few things are worth setting for your own use:

- **Brand system** — `featured-image` ships with a neutral placeholder palette. Point it at your own
  brand guidelines, or replace the palette in its Step 3 with your colours, typeface and shape language.
- **Research tooling** — several stages can use a search-data connector (Ubersuggest / Ahrefs-style)
  when one is authorised, and fall back to web search and reasoning when it isn't. The skills label
  every figure as measured or estimated accordingly.
- **Worked examples** — some skills use an illustrative seed (e.g. "fractional CMO") to demonstrate a
  method. These are just examples; swap in your own topic when you run the skill.

## Provenance

The `seo-aeo-geo` agent and the `featured-image` skill are original work. The five pipeline skills
(`seo-aeo-geo-workflow`, `query-fan-out`, `semantic-outline`, `source-collection`, `article-draft`,
`seo-article-audit`) are adapted from Anthropic's bundled Claude skills, generalised here for reuse.
