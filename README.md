# SEO / AEO / GEO Agent

An end-to-end content agent for [Claude Code](https://claude.com/claude-code) that takes a topic
from research to a publish-ready article optimised for three things at once:

- **SEO** — ranking in Google.
- **AEO** — showing up in AI Overviews and featured snippets.
- **GEO** — getting cited inside answers from ChatGPT, Perplexity, Gemini and Claude.

The agent orchestrates a six-stage pipeline. It handles sequencing, state and the approval gates
between stages; each skill holds its own method in full. It reads a per-user **context pack** so the
output is written in your voice, for your market, sources and brand, not generic filler.

| Stage | Skill | Produces |
|---|---|---|
| 0 | `setup` | `seo-context.md` — your context pack (voice, market, sources, brand). Run once, first. |
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

This is a Claude Code plugin. Add the marketplace, then install:

```bash
claude plugin marketplace add Liagolledge/seo-aeo-geo-agent
```
```bash
claude plugin install seo-aeo-geo@liagolledge
```

Restart Claude Code. The agent appears as `seo-aeo-geo`, and each skill is invocable as
`seo-aeo-geo:<skill>` (e.g. `seo-aeo-geo:query-fan-out`, `seo-aeo-geo:featured-image`).

## First run: build your context pack

Before writing anything, set up your context pack — it's what makes the output sound like you
instead of generic content. Just say:

> set up the SEO agent

The `setup` skill interviews you (voice, sites, market, preferred sources, brand, any search-data
tool you've connected) and writes a `seo-context.md` into your project. Every other skill reads it.
You can edit that file by hand any time, or re-run setup to change it. Prefer to fill it in yourself?
Copy [`context.template.md`](context.template.md) to your project root as `seo-context.md`.

If you skip setup, the pipeline falls back to neutral defaults and tells you where it's guessing —
but a filled-in pack is the difference between "on brand" and "generic".

## Structure

```
.claude-plugin/
  plugin.json               # plugin manifest
  marketplace.json          # marketplace entry (install source)
context.template.md         # the context-pack template you fill in
agents/
  seo-aeo-geo.md            # the orchestrator
skills/
  setup/                    # stage 0 — builds your context pack
  seo-aeo-geo-workflow/     # programme-level frame
  query-fan-out/            # stage 1
  semantic-outline/         # stage 2
  source-collection/        # stage 3
  article-draft/            # stage 4
  seo-article-audit/        # stage 5
  featured-image/           # stage 6
```

## Customising

Everything specific to you lives in `seo-context.md`, not in the skills — so you configure once and
never edit skill files:

- **Voice & market** — spelling, point of view, tone, target market. Drives every stage.
- **Sources** — the publishers you want cited first. Blank uses broadly-trusted defaults.
- **Brand system** — colour palette (hex), typography and shape language for `featured-image`. Blank
  uses a neutral placeholder palette.
- **Research tooling** — if you've connected a search-data MCP (Ubersuggest has a free tier; Ahrefs
  and similar also work), record it and any usage cap. The pipeline uses real data when it's there
  and falls back to web search and reasoning, labelling figures as measured or estimated, when it isn't.

## Provenance

The `seo-aeo-geo` agent and the `setup` and `featured-image` skills are original work. The six
pipeline skills (`seo-aeo-geo-workflow`, `query-fan-out`, `semantic-outline`, `source-collection`,
`article-draft`, `seo-article-audit`) are adapted from Anthropic's bundled Claude skills, generalised
here for reuse.
