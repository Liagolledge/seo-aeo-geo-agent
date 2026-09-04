---
name: "source-collection"
description: "Gather authoritative, verifiable references to support the claims in an article, and map each source to the outline section it backs. Use whenever the user asks to find sources, citations, references, research, data, statistics or evidence for a piece of content — including \"back this up\", \"what can I cite here\", \"find me stats on X\", \"is there research on this\", or \"source this article\". Also use as the step between a semantic outline and a draft. Rejects anonymous blogs, affiliate content and unsourced claims, prefers primary research, and returns a mapped source list plus a rejection log."
---

# Source Collection

Finds authoritative references for an article's claims and maps each one to the section it supports. The output is a source pack a writer can draft from without going looking for anything else.

**Why this is a separate step:** sourcing while drafting produces motivated reasoning — you find something that roughly supports the sentence you already wrote. Sourcing first means the evidence shapes the argument instead of decorating it.

---

## Inputs

Work from whichever exists, in this order:

1. **A semantic outline** (from the `semantic-outline` skill) — best case. Every section already states the claim it must make, so the sourcing targets are explicit.
2. **A draft or brief** — extract the claims first, then source them.
3. **A topic only** — ask the user for the outline or the claim list before starting. Sourcing a bare topic produces a pile of links, not a source pack.

Also confirm the **market** (a specific country or region, or global) — regional data usually beats global data for relevance, so pin down which market the piece is for.

## Source tiers

Rate every source. Never present a source without its tier.

### Tier 1 — use freely, lead with these

the user's named preferences:

- **McKinsey** (and McKinsey Global Institute)
- **Harvard Business Review**
- **Andreessen Horowitz (a16z)**
- **Google Research**
- **OpenAI Research**

Plus anything of equivalent standing:

- Peer-reviewed journals and academic institutions
- Government statistics bodies (ABS, BPS Indonesia, Eurostat, US BLS, OECD, World Bank)
- Original research from the organisation that collected the data — the actual report, not a write-up of it
- Standards bodies, patent filings, official documentation

### Tier 2 — usable, attribute clearly

- Named-analyst research from established firms (Gartner, Forrester, Deloitte, PwC, BCG, Bain)
- Reputable business and trade press with a named journalist and original reporting — Financial Times, The Economist, Reuters, Bloomberg, WSJ, AFR
- Industry bodies publishing their own survey data
- Named experts writing under their own name with verifiable credentials
- Company engineering blogs and post-mortems where the company is the primary source on its own system

### Tier 3 — last resort, flag it

- Vendor research (a survey by a company that sells the solution the survey recommends). Usable only when the bias is stated in the text and the number is genuinely unavailable elsewhere.
- Aggregator sites republishing someone else's data. **Always chase the original first** — if the original is findable, cite that and drop the aggregator.

### Rejected outright

- **Anonymous blogs** — no named author, no organisation, no accountability.
- **Affiliate content** — "best X tools" pages monetised by the tools they rank. Structurally compromised.
- **Content farms and AI-generated listicles** — recognisable by the absence of any original data and the presence of every competitor's name.
- **Statistics with no traceable origin** — the "73% of marketers say…" stat that every page repeats and no page sources. If the trail dead-ends, the number doesn't get used.
- **Press releases presented as research.**
- **Anything behind a paywall the user can't access** — no point citing what the user can't verify.

## Method

**1. Extract the claims.** List every factual assertion the article makes that a reader could reasonably challenge. Number them. Opinions and the user's own experience don't need sourcing — mark those `own-authority` and move on.

**2. Search for each claim.** Use web search. Search for the *primary* source, not the claim itself: look for who would have collected this data, then find their report. Searching the claim finds people repeating it; searching the collector finds the origin.

**3. Trace every statistic to its origin.** When a number appears in a Tier 2 source, follow it back. Most widely-repeated marketing statistics trace to a small survey from years ago, or to nothing at all. Finding that out is doing the job properly, not a detour.

**4. Check the date.** Note the publication date of everything. For anything about AI, search behaviour, or technology, **anything older than 18 months needs a reason to still be cited.** For structural or behavioural research, older is often fine. State the age; don't hide it.

**5. Verify it says what you think it says.** Fetch the actual page. Confirm the number, the wording, and the context. A statistic quoted out of context is a wrong statistic. If the page can't be fetched, say so rather than citing it blind.

**6. Note what's missing.** Claims with no credible support are the most valuable finding here. For each, recommend one of: cut the claim, soften it to something defensible, or replace it with the user's own data or experience.

## Rules that matter

- **Prefer primary over secondary, always.** The report beats the article about the report.
- **One strong source beats three weak ones.** Don't pad.
- **Never invent a citation.** No plausible-sounding URLs, no half-remembered statistics, no "a McKinsey study found" without the actual study in hand. If it can't be found and verified, it goes in the gap list.
- **Diversity of sources matters** for AI citation. An article leaning entirely on one organisation reads as promotional; three or four independent sources agreeing reads as established.
- **Original data outranks everything.** If the user has their own numbers — client results, campaign data, survey responses — those are the strongest asset in the piece, because no competitor can cite them. Ask for them explicitly and mark them `original`.

---

## Output

Save `sources-[topic-slug].md` in the outputs folder and present it.

**1. Source map** — the core deliverable, one table row per source:

| Outline section | Claim it supports | Source | Tier | Publisher | Date | Type | URL | Verified |
|---|---|---|---|---|---|---|---|---|

`Type` = primary research / analysis / reporting / original (the user's own). `Verified` = yes if the page was fetched and the claim confirmed, no if not, with a one-line reason.

**2. Ready-to-use citations** — for each source, the exact sentence the user can drop into the draft, phrased naturally with the attribution built in. Not a bare link.

**3. Gap list** — claims with no credible support, each with a recommendation: cut, soften, or replace with original data.

**4. Rejection log** — what was found and deliberately not used, with the reason in a few words ("affiliate", "stat untraceable", "2019, superseded"). This is short but worth keeping: it stops the same weak source being rediscovered on the next run, and it's a credibility asset if a client asks how the sourcing was done.

**5. Freshness note** — anything cited that's over 18 months old, with why it still stands.

## After the output

Offer in one line: writing the draft from the outline and this source pack (`article-draft` skill), or going back to fill the gaps with the user's own data.

