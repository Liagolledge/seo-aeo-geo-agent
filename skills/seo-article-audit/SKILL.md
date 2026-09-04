---
name: "seo-article-audit"
description: "Audit a draft or published article for answer-first structure, header clarity, LLM-friendly formatting, how likely it is to be retrieved and cited by ChatGPT and other AI assistants, and alignment with the brand positioning in the brief. Use whenever the user asks to audit, review, check, critique or score an article, blog post or landing page — including \"is this good enough to publish\", \"will AI cite this\", \"why isn't this ranking\", \"check this before it goes live\", or \"review my draft\". Returns structured, prioritized recommendations with specific before/after rewrites, not vague advice."
---

# SEO Article Audit

Audits a draft or live article against the five things that decide whether it gets found, extracted, and cited — then returns specific fixes, not general advice.

**The test for every recommendation:** could the user act on it without asking a follow-up question? "Improve your headings" fails. "Change H2 3 from 'The Approach' to 'How does a fractional CMO engagement actually work?'" passes. Every finding in the output carries the actual replacement text.

---

## Inputs

- **The article** — a file, a pasted draft, or a URL. For a URL, fetch it; if the page is client-rendered and the fetch returns a shell, use the Chrome browser tools to get the real content.
- **The brand positioning** — from the brief, the outline, or the project's context folder: who it serves, what it claims, the language it uses, what it doesn't claim. If none is supplied, ask for it in one line or run Section 5 as a general consistency check and say clearly that's what was done. **Never invent positioning to audit against.**
- **The outline**, if one exists. Auditing against the agreed plan catches drift that reading alone misses.

---

## Section 1 — Answer-first structure

The single biggest determinant of whether a model quotes the piece.

Check:

- **The opening.** Does the first sentence directly answer the question in the title? Or does it set a scene, define a term nobody asked about, or open with "in today's landscape"? Anything before the answer is a reason to skip the page.
- **The answer's quotability.** Read the first 40–60 words alone, with no surrounding context. Do they stand as a complete answer? If they need the next paragraph to make sense, they won't be lifted.
- **Every section.** Does each one open with its own direct answer before explaining? List every section that buries its answer, with the sentence that should be moved to the front.
- **Depth after the answer.** Does the reasoning or mechanism follow, or does it jump to the next point? An answer with no "why" gets paraphrased and discarded rather than cited.

Report: pass/fail per section, and a rewritten opening sentence for every failure.

## Section 2 — Section headers

Check every heading:

- **Question-phrased or plainly descriptive?** "Background", "Overview", "Getting Started", "The Approach" are invisible to readers scanning and to models matching sub-queries. Rewrite each into the question it answers.
- **Does it match how people actually search?** Headings that mirror real query language get matched to sub-queries during fan-out. Headings written for elegance don't.
- **Hierarchy.** One H1. No skipped levels. No H3s nested under H3s. Deeper than H3 fragments meaning.
- **Does the heading promise what the section delivers?** A mismatch here is worse than a dull heading — it breaks trust for readers and confuses extraction.

Report: a table of every heading, current vs. suggested, with a one-line reason for each change.

## Section 3 — LLM-friendly formatting

How easy is it for a model to lift a clean chunk?

- **Paragraph length.** 2–4 sentences. Flag every wall of text with where to break it.
- **Section independence.** Can each section be read alone? Hunt for "as mentioned above", "as we discussed", "this approach" where "this" refers to something two headings back. Every one of these breaks a section's ability to be extracted. List them with the fix — usually just naming the thing again.
- **Lists and tables.** Is anything written as prose that is structurally a list or a comparison? Comparison content in table form is among the most reliably extracted formats there is. Flag prose comparisons and show the table.
- **Entity consistency.** Is the main subject named identically throughout? List every variant found. Inconsistent naming quietly undermines citation trust.
- **FAQ block.** Present? Phrased as people actually type? Answered in 2–3 sentences, answer-first? If missing, draft 4–6 questions from the article's own content.
- **Schema.** Which is applied, which should be: Article always, FAQPage with an FAQ block, HowTo for step content, Product/Review for comparisons.
- **Metadata.** Title tag ≤60 characters, meta description ≤155, both present and matching the page's actual promise. Supply rewrites if either is missing or off.

## Section 4 — Retrieval likelihood in ChatGPT and other assistants

The judgement call section. Assess honestly — a flattering audit is a useless one.

- **Extractability.** Pick the three most likely questions someone would ask an assistant that this article should answer. For each, name the specific passage a model would lift. If there isn't one, that's the finding — the article covers the topic without answering the question.
- **Information gain.** What does this piece contain that a model couldn't already assemble from three other pages? If the answer is nothing, no amount of formatting will earn a citation. Say so plainly; it's the most important thing in the audit.
- **Verifiable specifics.** Count the specific, checkable numbers. Zero is a serious finding. Original data — the user's own or the client's — is the strongest citation asset available, because no competitor can cite it.
- **Source quality.** Are claims attributed to named, credible sources in the prose, or hyperlinked behind "studies show"? In-prose attribution is citable; a bare link isn't.
- **Freshness.** Publication or update date visible? Anything cited over 18 months old on a fast-moving topic? Assistants, ChatGPT especially, lean toward the freshest available information.
- **Author credibility.** Named author, credentials, link to a real profile? This is a direct E-E-A-T signal and is frequently missing entirely.

Report a **retrieval likelihood rating — high / moderate / low** — with the two or three changes that would move it up a level. Justify the rating with evidence from the article, not vibes.

## Section 5 — Positioning alignment

Audit against the positioning supplied in the brief.

- **Does the piece sound like the brand it's for?** Terminology, tone, formality, the words it uses for its own category.
- **Does it claim what the brand claims — and only that?** Flag anything overstated, anything a competitor could equally say, anything the brand can't actually back.
- **Is the credibility tie present, once, naturally?** Not absent, not in every paragraph.
- **Audience fit.** Is it pitched at the person the positioning names, or has it drifted toward a broader, vaguer reader?
- **Consistency with the rest of the site**, where that's visible.

If no positioning was supplied, run this as a general internal-consistency check — does the article maintain one voice, one audience, one claim throughout — and state clearly that's what was assessed.

---

## Output

Save `audit-[article-slug].md` in the outputs folder and present it.

1. **Verdict** — one paragraph. Publish as-is / publish after the priority fixes / needs structural rework. Be direct; a hedged verdict is no verdict.
2. **Retrieval likelihood: high / moderate / low**, with the reasoning.
3. **Priority fixes** — the 3–5 changes with the most impact, each with the exact rewrite. Ordered by impact, not by where they appear in the article.
4. **Full findings by section** — the five sections above, each finding tagged **Critical / Important / Minor**, each with current text and replacement text.
5. **Quick wins** — anything fixable in under five minutes, listed so the user can knock them out in one pass.
6. **What's working** — genuinely, briefly. Not padding: knowing what to preserve matters when editing, and an audit that finds nothing good is usually not looking properly.

## How to audit well

- **Be specific or say nothing.** A finding without a rewrite is an opinion.
- **Be honest about severity.** If the piece has no information gain, that's Critical and belongs at the top, above any formatting note. Don't bury the real problem under twelve small ones.
- **Don't flag style as error.** A deliberate voice choice isn't a defect. Distinguish "this breaks retrieval" from "I'd have written it differently" — and only report the first.
- **Count the things that can be counted.** Number of sections burying their answer, number of specific figures, number of entity name variants. Countable findings are actionable; impressions aren't.

## After the output

Offer in one line: applying the priority fixes directly to the draft, or re-auditing after the user edits.

