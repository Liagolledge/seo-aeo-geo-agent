---
name: "seo-aeo-geo-workflow"
description: "Workflow for writing, auditing, or planning content optimized for traditional search (SEO), answer engines and featured snippets (AEO), and citation inside AI-generated answers from ChatGPT, Perplexity, Gemini, and Claude (GEO). Use this skill whenever the user asks to write a blog post, article, landing page, or content plan that needs to rank in Google, show up in AI Overviews, or get cited by AI assistants — and also when auditing existing content or a site's technical SEO health for AI/search visibility. Trigger this for any brand or project, not just one specific site — personal blogs, company blogs, consulting/client work, and content strategy docs all qualify. Don't wait for the user to say \"SEO\" or \"AEO\" explicitly — phrases like \"get cited by ChatGPT,\" \"show up in AI search,\" \"featured snippet,\" \"rank higher,\" or \"why isn't AI mentioning us\" all call for this skill too."
---

# SEO / AEO / GEO Content Workflow

A brand-agnostic workflow for producing content that ranks in traditional search, gets extracted into answer-driven features (featured snippets, AI Overviews, voice assistants), and gets cited as a source inside AI-generated answers from ChatGPT, Perplexity, Gemini, and Claude.

These three things aren't separate strategies — they're layers on the same foundation. SEO gets a page found. AEO gets a specific answer pulled out of it. GEO gets that answer trusted enough to be quoted by an AI model instead of just linked to. Content built well for one tends to work for the others, provided it's built the right way from the start.

Use this skill for: planning a content programme, auditing a site's search and AI visibility, or diagnosing why something isn't showing up. For producing one specific article, the dedicated pipeline below does the job better.

## The single-article pipeline

For one piece of content, these five skills run in order and go deeper than this workflow does:

1. `query-fan-out` — the full sub-query landscape for a topic
2. `semantic-outline` — the meaning-first blueprint
3. `source-collection` — authoritative references mapped to sections
4. `article-draft` — the first full draft
5. `seo-article-audit` — what to fix before publishing

**Use this workflow instead when** the job is the programme, not the piece: technical health, content architecture across many pages, distribution, and measurement over time.

---

## Research tooling: the Ubersuggest connector

An Ubersuggest MCP connector is available and gives real search data rather than estimates. Use it wherever a phase below calls for numbers.

### Quota discipline — read this first

**The account is on the free tier: 3 reports per day.** Some tools consume a report; the quota resets daily. This changes how research should be run:

- **Plan the calls before making any.** Decide the two or three questions that actually need real data, and spend the quota on those. Don't call a tool to confirm something already known.
- **Batch where the tool allows it.** `keyword_suggestions` accepts up to 3 seed keywords in one call; `google_suggestions` expands up to 10. One well-formed call beats five narrow ones.
- **When the quota is exhausted**, the tool returns an explicit "daily reports limit" error. **Do not retry.** Tell the user plainly that the Ubersuggest data is spent for the day, continue with web search and reasoning, and clearly label any figure produced that way as an estimate.
- **Upstream rate limits happen too** — `google_suggestions` proxies Google autocomplete and sometimes returns a 429. That's temporary and not a quota issue. Say so, don't retry immediately, and move on.
- **Check `auth_status` first** if anything behaves unexpectedly; it returns the account tier.

### Which tool for which job

| Need | Tool | Notes |
|---|---|---|
| Volume, CPC, SEO difficulty for one keyword | `keyword_overview` | Costs a report. Use on the seed and one or two finalists, not everything. |
| Related keywords with metrics | `keyword_suggestions` | Takes 1–3 seeds at once. The workhorse. |
| Paginated / custom-sorted keyword research | `match_keywords` | When `keyword_suggestions` isn't enough. |
| Hundreds of real long-tail phrasings | `google_suggestions` | Fans each seed into ~60 autocomplete queries. No metrics attached — pair with `keyword_overview` on the few worth pursuing. Excellent input for `query-fan-out`. |
| Who currently ranks, and how strong they are | `serp_analysis` | Top URLs with metrics. Use before writing anything competitive. |
| What content already performs on a topic | `content_ideas` | Top pages by shares, estimated visits, backlinks. |
| A domain's traffic, authority, keyword count | `domain_overview` | For competitor sizing or client baselining. |
| A competitor's keywords or best pages | `domain_keywords`, `domain_top_pages` | Gap analysis. |
| Technical health crawl | `site_audit` → poll `site_audit_status` → `site_audit_results` | Three-step flow; `site_audit` needs a paid account. `pagespeed_audit` covers Core Web Vitals separately. |
| Backlink profile | `backlinks`, `backlinks_overview`, `linking_domains`, `anchor_texts` | |
| **AI search visibility** | `brand_visibility_overview`, `brand_prompts` | See below — this is the GEO measurement tool. |
| Prioritised fixes for a tracked project | `seo_opportunities` | Needs a project ID from `list_projects`. |

### Location IDs — never guess one

Tools taking a `locId` need a real Google location ID. **Always call `location_suggest` first** and use an ID it returns. A guessed or ISO country number will silently return wrong-market data, which is worse than no data.

`location_suggest` returns city-level results first, so search the specific city rather than the country. If no country-level entry appears for a market, use the largest relevant city or omit `locId` for global figures — and say which was used.

### The GEO measurement tools

`brand_visibility_overview` and `brand_prompts` are the most directly useful tools here for Phase 6, and the easiest to overlook. They report how often a brand appears in AI assistant answers across **OpenAI, Gemini and Google AI Overviews** — visibility percentage, average rank, share of voice, sentiment, and a competitive brand ranking, plus a per-prompt breakdown.

That is the GEO number this whole workflow exists to move. Both need a `project_id` from `list_projects` where `has_brand` is true. If no such project exists, setting one up is worth recommending — without it, AI visibility is being managed on vibes.

---

## Phase 1: Technical Foundation

Content work is wasted if search engines and AI crawlers can't read the site properly. Before or alongside writing, check:

- **Indexing & crawlability** — confirm the site is indexed in Google Search Console (and Bing Webmaster Tools if relevant); `robots.txt` isn't blocking anything important; the XML sitemap is clean (no parameters, duplicates, or system URLs); pages that are "crawled but not indexed" get more internal links and thicker content.
- **URL hygiene** — one canonical URL structure, used consistently; 301-redirect broken pages, tracking-parameter variants, and duplicate paths into a single clean URL; canonical tags site-wide.
- **On-page basics** — one H1 per page, descriptive title tags, unique meta descriptions, descriptive image alt text (this also helps AI vision models understand images).
- **Schema markup** — Organization schema (homepage/about), Article/Blog schema (posts), FAQ schema (any page with Q&A content), Breadcrumb schema. These are direct machine-readable signals, not SEO folklore.
- **Site speed** — healthy Core Web Vitals (LCP, CLS, FCP); slow pages get deprioritised and are harder to fully render.
- **E-E-A-T signals** — a real "About" page that functions as a knowledge pack (who, credentials, verifiable track record); author bios with credentials and links on every article.

**Tooling:** run `site_audit` for the crawl (paid account required — if it's unavailable, say so and check the basics manually), and `pagespeed_audit` for Core Web Vitals.

Skip this phase only when the task is purely "write me an article" for a site already confirmed technically healthy.

## Phase 2: Audience & Query Research

Know exactly what the audience is asking, in the language they actually use — which is often different across Google and AI tools.

1. **Map the audience to funnel stage.** For each core audience, write the real questions they'd ask at each stage:
   - *Awareness* — "How can I…" (they know the problem, not the solution category)
   - *Consideration* — "Best tools/ways to…" (comparing options within a known category)
   - *Evaluation* — comparison questions, often branded ("X vs Y", "X vs alternatives")
   - *Decision* — feature-verification questions ("Does X do Y?", "Can X integrate with Z?")
2. **Run query fan-out.** Use the `query-fan-out` skill for the full method. Feed it `google_suggestions` output for real autocomplete phrasings and `keyword_suggestions` for volume-backed variants.
3. **Check social listening where relevant.** Real phrasing from forums, niche communities, or social threads beats guessed phrasing.
4. **Check current AI citation gaps.** Run the 10–20 highest-intent queries through ChatGPT, Perplexity, Gemini, and Claude, or read `brand_prompts` if a tracked project exists. Note what gets cited — that's both the competitive benchmark and the content gap list.

Output: a running list of real questions grouped by topic and funnel stage. That list becomes the article backlog and the outline skeleton.

## Phase 3: Content Architecture

Don't plan isolated posts — build topical depth, since both Google and AI models reward authority on a topic over scattered single posts.

- **Pillar + cluster model** — one comprehensive pillar page per core topic, plus 10–15 supporting articles that each answer one specific sub-question and link back to the pillar.
- **Format mix** — comparison/"vs" pages, "best of" listicles, how-to guides, original case studies with real numbers, and founder/personal-authority stories. Rotate rather than defaulting to one format.
- **Comparison content is disproportionately valuable for AEO/GEO** — AI models are frequently asked "X vs Y" or "alternatives to X". With zero comparison content, a site is structurally invisible for that entire query category no matter how good everything else is.
- **Programmatic variation, used carefully** — the same core content can be adapted for genuinely distinct audiences or geographies, but only where the content is meaningfully different. Thin, near-duplicate pages hurt more than they help.

**Tooling:** `content_ideas` shows what already performs on a topic; `domain_top_pages` on a competitor shows where their authority actually sits.

## Phase 4: The Article Template

Use this structure for every individual piece — it's the part that determines whether a model lifts and cites the content. The `semantic-outline` and `article-draft` skills implement this in full.

1. **Answer first.** The opening sentence or two directly answers the implied question. No scene-setting. This is the sentence a model will quote verbatim if it quotes anything.
2. **Go one click deeper.** Right after the answer, explain the reasoning or mechanism. This separates a citable source from a thin snippet that gets paraphrased and discarded.
3. **Include original data or a specific, verifiable number wherever possible.** A real result beats a recycled industry stat every time — originality is one of the strongest citation signals, because it can't be found anywhere else.
4. **Structure so each section stands alone.** Question-phrased headers, bullets, short paragraphs. A model should be able to lift any single section as a complete answer.
5. **Add an FAQ block at the end**, phrased the way someone would actually type it. Pairs with FAQ schema and is one of the highest-leverage additions for both snippets and AI citations.
6. **Tie back to the author's point of view or expertise once, naturally.** A single clear connection between the content and why the person or brand behind it is credible.

## Phase 5: Distribution & Repurposing

One well-built article should become several pieces, each mapped to where the audience actually spends time — a LinkedIn post series (one insight per post, linking back), a short video on the core argument, an email sequence, and, if the article contains a checklist or framework, a downloadable version. The `content-repurposing` skill handles the formats.

Also worth pursuing: guest posts or mentions on the handful of sites AI models already treat as trusted in the relevant space. A citation on a site a model already trusts often outweighs a mention on the brand's own site.

## Phase 6: Measurement & Iteration

- **Track AI visibility as its own channel from day one**, even at zero — the baseline is needed to prove growth later. `brand_visibility_overview` gives the headline number across OpenAI, Gemini and Google AI Overviews; `brand_prompts` shows which specific prompts the brand wins and loses.
- **Track AI referral traffic** (ChatGPT, Perplexity, Gemini visits) separately in analytics.
- **Re-run the Phase 2 benchmark queries monthly** and track whether citations start appearing.
- **Refresh top-performing pages** rather than treating the publish date as final — AI models, ChatGPT especially, have a measurable bias toward the freshest available information.
- **Re-check technical health periodically** — a technical regression silently undoes content work.

## What to skip

Two things pitched as best practice that don't earn their keep: chunking content into unnatural fragments "for AI parsing" (well-structured, genuinely clear writing does this job on its own — over-engineering for a hypothetical crawler makes it worse for readers, and eventually worse for AI models too, since they're trained on what people find useful), and publishing an `llms.txt` file as a growth lever (it isn't what moves the number — clear structure, real answers, and consistent entity naming are).

## Writing style notes

Keep numbers specific and verifiable — "+938% visitors in 6 months" beats "significant growth", always. When a figure comes from Ubersuggest, say so; when it's an estimate made without data, label it an estimate. Use the same name for the brand, product or person consistently across the piece and across the site; entity consistency is part of how AI models resolve who or what is being discussed, and inconsistent naming quietly undermines citation trust even when the content is good.

