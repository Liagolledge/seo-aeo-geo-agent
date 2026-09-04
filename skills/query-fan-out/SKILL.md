---
name: "query-fan-out"
description: "Research query fan-out — expand one seed keyword or prompt into the full set of sub-queries an AI search engine generates from it, using the eight variant types from Google's query-variant patent, then score and tier them. Use whenever the user asks about query fan-out, sub-queries, \"what else would someone search\", \"what questions should this cover\", keyword expansion, \"what is AI actually searching for\", semantic variations, long-tail research, or wants to know the full demand landscape around a topic before writing. Also use as the research step feeding a semantic outline or content brief. Outputs a markdown brief plus a CSV of every query with type, intent, tier and score."
---

# Query Fan-Out Research

Expands one seed keyword or prompt into the full set of sub-queries a modern AI search system would generate from it, then scores and tiers them so the user knows which ones actually matter.

## Why this exists

When someone asks ChatGPT, Perplexity or Google AI Mode a question, the system doesn't run that one query. It silently generates a spread of related sub-queries, runs them in parallel, collects the results, and synthesises a single answer from whatever came back. That expansion is called **query fan-out**.

The consequence for content: a page can be a perfect match for the query someone typed and still never appear in the answer, because the sub-queries the model actually ran went somewhere the page doesn't cover. Optimising for the visible query alone is optimising for a query the machine barely uses.

This isn't marketing folklore. It's described in **US Patent 11663201B2, "Generating query variants using a trained generative model"** (Google LLC, filed 2018, granted 30 May 2023), which names the exact variant categories used below. Cite the patent when the method needs backing — it's verifiable and most competitors' content isn't grounded in it.

---

## Step 1 — Set the seed

Get from the user, asking only what you can't infer:

- **The seed** — a keyword ("fractional CMO") or a natural prompt ("how do I hire a fractional marketer"). Prompts fan out differently from keywords; if the user gives a keyword, also write the prompt version, because that's what people type into AI tools.
- **Whose site** — the user's own site, a sub-brand, or a client's. Drives relevance scoring.
- **Market** — the target country or region, or global. Changes phrasing, spelling, competitors and volumes.

If a project folder has a context folder, read it before asking.

## Step 2 — Generate the eight variant types

Produce **6–10 variants per type, minimum 45 total.** Fewer than that and the map has holes. Each variant must read like something a person or a model would actually issue — not a keyword string.

| # | Type | What it is | Example (seed: "fractional CMO") |
|---|---|---|---|
| 1 | **Equivalent** | Same intent, different words. Paraphrases and synonyms. | "part-time marketing director", "outsourced head of marketing" |
| 2 | **Follow-up** | What they ask *next*, after the first answer lands. | "how much does a fractional CMO cost", "how long do they stay" |
| 3 | **Generalization** | The broader question this sits inside. | "how do small companies get senior marketing help" |
| 4 | **Specification** | Narrower — constraints, audience, geography, budget, timeframe. | "fractional CMO for B2B SaaS under $2M revenue" |
| 5 | **Canonicalization** | The clean, standard form of a messy or colloquial phrasing. | "part time CMO thing where they only work 2 days" → "fractional CMO engagement model" |
| 6 | **Entailment** | What logically follows if the answer is true — consequences, prerequisites, implications. | "what does a fractional CMO need from us to start", "do we still need a marketing manager" |
| 7 | **Clarification** | What the system would ask back to disambiguate. | "do you mean fractional CMO or marketing consultant", "for hire, or how to become one" |
| 8 | **Language translation** | The same query in another relevant language. Only when the audience is genuinely multilingual. | "CMO paruh waktu untuk startup" (skip for single-language audiences) |

Two types carry disproportionate weight and are the ones most people skip:

- **Entailment** exposes the objections and prerequisites nobody writes about. It's where the gap usually is.
- **Clarification** reveals when a seed is genuinely ambiguous. If a query needs several clarifications to make sense, that's a signal the topic should be split into separate pieces rather than one confused article.

## Step 3 — Add real-world signal

Variants generated in a vacuum sound plausible and are sometimes wrong. Ground them:

- **Web search** the seed and 3–4 of the strongest variants. Note the People Also Ask box, autocomplete suggestions, and any "related searches" — those are observed behaviour, not inference.
- **SEO connector** (Ubersuggest / Ahrefs-style) if authorised: pull keyword suggestions, volumes and related questions. If it isn't connected, say so once and continue — don't block on it.
- **Real phrasing** from Reddit, niche forums, comment sections, and the user's own client conversations and DMs. Always outranks invented phrasing.

Mark each query's origin: `generated`, `observed` (PAA/autocomplete/forum), or `data` (from a keyword tool). Observed and data-backed queries get a scoring bump — they're evidence, not guesses.

## Step 4 — Cross-check against the live tools

After generating independently, check the two public tools to catch anything missed. Do this **second, never first** — seeing their output before generating anchors the whole map to what they happen to surface.

Use Claude in Chrome (`mcp__claude-in-chrome__*`; load via ToolSearch if not already available):

- **https://wellows.com/tools/query-fan-out/** — enter the seed keyword, set location, generate. Free, no login, exports CSV. May ask for domain and email.
- **https://geo.otterly.ai/geo/ai-query-fan-out/** — enter the seed as a prompt, run across Google AI Overview, Google AI Mode and ChatGPT. Shows the sub-queries those engines actually expand into, which is the closest thing to observed truth available.

Both are third-party tools that change without notice. **If either is down, gated, changed, or asks for details the user hasn't approved sharing, skip it and say so in the output.** Never enter the user's email or a client domain without asking the user first. The method in Steps 2–3 stands on its own; the tools are a cross-check, not a dependency.

Record anything the tools surfaced that the generated set missed, tagged `tool-found`. That delta is worth noting explicitly — it shows where reasoning alone fell short and is useful feedback for the next run.

## Step 5 — Classify and score

For every query, assign:

**Intent** — informational / commercial / transactional / navigational.

**Funnel stage** — awareness / consideration / evaluation / decision.

**Three scores, 1–5 each:**

- **Popularity** — how many people plausibly ask this. Use real volume data where available; otherwise estimate and label it an estimate. Never present a guessed number as a measured one.
- **Relevance** — how directly this serves the user's or the client's actual offer. A high-volume query nobody can convert on scores low here.
- **Prominence** — how likely the answer is to be quoted or cited rather than skimmed. Clear, factual, answerable-in-a-sentence queries score high; vague opinion queries score low.

**Tier** = average of the three:

- **Tier 1 (4.0+)** — build content for these now. Usually becomes a heading or a full piece.
- **Tier 2 (2.5–3.9)** — cover as a section inside a larger piece, or an FAQ entry.
- **Tier 3 (<2.5)** — note and park. Revisit if the topic grows.

Be honest with scores. A fan-out where everything is Tier 1 is a fan-out that hasn't been thought about.

## Step 6 — Find the gap

The scoring is not the deliverable. This is:

- **Cluster** the queries into 4–8 themes. Themes, not types — a theme cuts across variant types.
- **Coverage check** — for each Tier 1 and Tier 2 query, does existing content (the user's or the client's) already answer it? Mark `covered` / `thin` / `missing`.
- **Name the three biggest gaps** — highest-scoring queries with nothing behind them. These are the recommendations.
- **Flag split candidates** — clusters big enough to deserve their own piece rather than a section.
- **Flag the ambiguity** — if Step 2's clarification variants revealed the seed means two different things to two different audiences, say so plainly. That finding is often worth more than the whole query list.

---

## Output

Two files in the outputs folder, then present both:

**1. `query-fan-out-[seed-slug].md`**

1. Seed, prompt version, market, date run
2. Headline finding — the single most useful thing learned, in one or two sentences
3. The three biggest content gaps, with the queries that prove each
4. Theme clusters, each with its Tier 1 queries
5. Coverage table — what's covered, thin, missing
6. Split candidates and ambiguity flags
7. Method note — which sources were used, which tools ran or were skipped and why, and which numbers are measured vs estimated

**2. `query-fan-out-[seed-slug].csv`**

Columns: `query, variant_type, intent, funnel_stage, popularity, relevance, prominence, avg_score, tier, origin, coverage, theme`

One row per query. Sorted by avg_score descending. This is the working file — the user sorts and filters it herself.

Keep the markdown in plain English. Every acronym gets its meaning on first use. It's a working document, not an SEO report.

## After the output

Offer, in one line: turning the top cluster into a semantic outline (`semantic-outline` skill picks up directly from the question inventory this produces), or re-running the fan-out for a second seed.

## What not to do

- Don't present estimated search volumes as measured data. Label every estimate.
- Don't pad to hit a query count. Forty-five real variants beats eighty with filler.
- Don't let all eight types produce the same query in different clothes — if the equivalent and canonicalization sets look identical, one of them wasn't done properly.
- Don't hand over the CSV alone. The finding is the value; the list is the evidence.

