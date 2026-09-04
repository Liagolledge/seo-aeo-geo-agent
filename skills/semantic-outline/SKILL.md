---
name: "semantic-outline"
description: "Build a semantic outline — the meaning-first blueprint for a blog post or article, optimized for SEO, AEO (featured snippets, AI Overviews) and GEO (getting cited by ChatGPT, Perplexity, Gemini, Claude). Use whenever the user asks for an outline, a content brief, a blog post structure, \"what should this article cover\", \"plan a post about X\", \"brief for a writer\", \"help me structure this article\", or wants an existing post restructured before rewriting. Also trigger when the user names a keyword or topic and asks what to write. Produces the blueprint only — entities, questions, headings, answer targets, schema and internal links — as a markdown file, not the finished draft."
---

# Semantic Outline

Builds the blueprint for an article **before** any drafting happens: what the piece must mean, not just what keywords it must contain.

A keyword outline lists headings. A semantic outline maps the topic the way a search engine or an AI model does — as a network of entities, relationships and questions — then arranges that map into a structure where every section is independently liftable as an answer.

**This skill stops at the blueprint.** Do not write the article.

## Where this sits

The content pipeline, in order:

1. `query-fan-out` — what people actually ask
2. **`semantic-outline`** ← this skill — what the piece must say and in what order
3. `source-collection` — what backs each claim
4. `article-draft` — the first full draft
5. `seo-article-audit` — what to fix before publishing

Each step can run alone, but the outline is much stronger with a fan-out behind it. `seo-aeo-geo-workflow` covers the wider programme — technical health, content architecture, distribution, measurement — and is the right skill when the user is planning a content strategy rather than a single piece.

---

## Before starting

Ask only what you genuinely can't infer. In one round, confirm:

1. **The target query and the audience** — the exact thing someone types or asks, and who they are.
2. **Whose site it's for** — the user's own site, one of their sub-brands, or a client's. This determines voice, credibility angle and internal linking.
3. **What the user already has** — original data, client results, personal experience, screenshots, a transcript. This is the single biggest lever on whether the piece gets cited, so ask for it explicitly.

If a project folder has a context folder, read it first — audience, brand voice and prior posts come from there, not from guesses.

---

## Step 1 — Lock the intent

Write one sentence: *"Someone searching this wants ___, at the ___ stage, and will be satisfied when they know ___."*

Then name the stage, because it dictates the whole structure:

- **Awareness** — "how do I…", problem-aware only. Structure: explain, then widen.
- **Consideration** — "best ways/tools to…". Structure: options with honest trade-offs.
- **Evaluation** — "X vs Y", "alternatives to X". Structure: comparison table up top.
- **Decision** — "does X do Y", "how much does X cost". Structure: the answer in the first line, then the caveats.

Mixed intent is a warning sign. If the query serves two stages, say so and recommend splitting into two pieces rather than writing one that half-serves both.

## Step 2 — Build the entity map

This is the part that makes the outline *semantic* rather than a keyword list. An entity is a real thing with a name — a person, company, tool, place, method, concept. Models understand topics as entities connected to other entities, so an article that names the right ones is legible in a way a keyword-stuffed one isn't.

Produce four groups:

- **Primary entity** — the one thing the article is about. Pick the name and use it identically everywhere, in the article and across the site. Inconsistent naming quietly wrecks citation trust.
- **Supporting entities** — the things that must appear for the topic to be complete. If someone knowledgeable would notice one missing, it's required, not optional.
- **Attributes** — the properties of the primary entity a reader needs: cost, timeline, requirements, limitations, who it's not for.
- **Adjacent entities** — near neighbours worth a mention and an internal link, but not worth a section. These prevent the piece from sprawling.

For each supporting entity, note in one line *why it belongs*. If there's no answer, cut it.

## Step 3 — Fan out the questions

**Run the `query-fan-out` skill on the target query.** It produces the full sub-query landscape — the eight patent-based variant types, scored and tiered, with a coverage check — and its question inventory is exactly what this step needs. Don't duplicate that work here.

If the user has already run a fan-out for this topic, reuse the CSV rather than regenerating.

Only if `query-fan-out` isn't available or the user wants a faster pass, do the lightweight version inline:

1. **Real phrasing** — Reddit, niche forums, comment sections, the user's own client conversations and DMs. Always beats invented phrasing.
2. **Live search data** — if an SEO connector (Ubersuggest/Ahrefs-style) is authorised, pull keyword suggestions, related questions and search volume. If it isn't connected, say so once and move on; don't block on it.
3. **Web search** — check what's actually ranking and what the People Also Ask box holds.
4. **The follow-up test** — "what would someone ask immediately after reading the answer to this?" Two levels deep.

Either way, end with every question sorted into three buckets:

- **Must answer** — the piece fails without it.
- **Should answer** — adds depth, keeps the reader on-page.
- **Adjacent** — becomes a separate post; note it as a backlog idea rather than cramming it in.

## Step 4 — Benchmark what already exists

Two checks, both quick:

**In Google** — look at the top 3–5 results. Note their heading structures, what they all cover (table stakes), and what none of them cover (the opening). Note the snippet format Google currently favours for the query — paragraph, list, or table — because matching that format is how the piece gets pulled into the snippet.

**In AI answers** — run the query through ChatGPT, Perplexity, Gemini and Claude if possible, or at minimum reason about what a model would currently say. Note who gets cited and what claim they get cited *for*. That specific claim is the thing to beat with something more specific, more original, or more current.

Finish this step with one line: **the information gain statement** — what this article will contain that no result on page one currently does. If that line is weak, the outline isn't ready. Go back to the user and ask what the user knows that the existing results don't.

## Step 5 — Build the structure

Now assemble the outline. Rules that matter more than they sound:

- **H1** — plain, matches the query language, no cleverness.
- **The answer paragraph comes first**, before any section. 40–60 words, directly answering the title question, written so it could be quoted verbatim with nothing else around it. No throat-clearing, no "in today's landscape".
- **Every H2 is a question or a plain statement of what it delivers.** Not "Background" or "Getting started" — those are invisible to both readers and models.
- **Every section opens with its own direct answer**, then explains. A model should be able to lift any single section as a complete answer without needing the rest of the article.
- **Logical order beats keyword order.** Sequence sections the way understanding actually builds.
- **One H3 level maximum.** Deeper nesting fragments meaning.
- **FAQ block at the end** — 4–6 questions phrased exactly as someone would type them, each answered in 2–3 sentences. Pull these from the Tier 2 queries in the fan-out. This pairs with FAQ schema and is one of the highest-leverage additions for both snippets and AI citations.

For each section in the outline, specify:

| Field | What goes in it |
|---|---|
| Heading | The H2/H3 as it will appear |
| Question answered | The reader question this closes |
| Direct answer | The one-sentence answer the section must open with |
| Entities to name | From the Step 2 map |
| Evidence needed | Data, example, screenshot, quote — and whether the user has it or needs to get it |
| Format | Paragraph / numbered list / bullets / table / example |
| Word budget | Rough, so the piece stays balanced |

The **Evidence needed** column is what `source-collection` works from next, so be specific: "the % of B2B buyers in the target market who research on mobile, 2024" is actionable; "some data" isn't.

## Step 6 — The machine-readable layer

Close the outline with:

- **Title tag** (≤60 characters) and **meta description** (≤155), both written, not described.
- **URL slug** — short, matches the primary entity.
- **Schema to apply** — Article always; FAQPage where there's an FAQ block; HowTo for step-based content; Product/Review for comparisons.
- **Internal links** — which existing pages this should link to, and which should link back to it. Name actual pages where known.
- **External citations** — 2–3 authoritative sources to reference. Being adjacent to trusted sources helps; being the only source on the page for every claim reads as unsupported.
- **Image plan** — what images are needed and the alt text for each, since alt text is how vision models read them.

## Step 7 — Check before handing over

Run these and report honestly:

- Can each section be read alone and still make sense? If not, restructure.
- Does the information gain statement survive scrutiny, or is it a rewording of what page one already says?
- Is every "must answer" question assigned to a section?
- Is the primary entity named identically throughout?
- Is there at least one specific, verifiable number — a real result, not a recycled industry stat?
- Is there a single natural tie to the user's (or the client's) credibility on this topic — once, not in every paragraph?
- Would a writer who knows nothing about the topic be able to draft from this without asking follow-up questions?

Flag any check that fails rather than quietly fixing it — a failed check usually means the user needs to supply something only the user has.

---

## Output

Save as a markdown file named `semantic-outline-[topic-slug].md` in the outputs folder, and present it. Structure it in this order:

1. Target query, intent, audience, stage
2. Information gain statement
3. Entity map
4. Question inventory (must / should / adjacent), noting whether it came from a full fan-out or the quick pass
5. Competitive + AI citation benchmark
6. The outline — section table as specified in Step 5
7. Metadata, schema, links, images
8. Checks: what passed, what the user still needs to supply

Keep the file itself in plain English. It's a working document the user or a writer will use, not an SEO report — no jargon that isn't doing a job, no acronym without its meaning on first use.

## After the output

Offer the next step in one line: gathering sources for the claims in this outline (`source-collection`), which is what the draft will need before it can be written.

