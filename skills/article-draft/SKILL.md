---
name: "article-draft"
description: "Write the first full draft of an SEO/AEO/GEO-optimized article from an approved outline and an approved source pack. Use whenever the user asks to write the article, write the post, draft it, \"turn this outline into a piece\", \"write it up\", \"now write it\", or hands over an outline and asks for the copy. Follows the outline strictly, uses only supplied sources, never invents citations, and applies the voice specified in the brief. Produces a labelled first draft for editing — not a finished, publishable asset."
---

# Article Draft

Turns an approved outline and an approved source pack into the first full draft of the article.

**This is a draft, not a final asset.** Say so when handing it over, and label the file accordingly. The value of this step is a complete, structurally correct piece the user can edit — not something to publish as-is. Drafts that are presented as finished get published as finished, and that's how thin content ships.

---

## Required inputs

Do not start without:

1. **The outline** — from `semantic-outline`, or one the user supplies. The draft follows it strictly.
2. **The source pack** — from `source-collection`, or sources the user supplies. **Only these sources may be cited.**
3. **The voice direction** — taken from the brief, the outline's project context, or the project's context folder. If none of those specify it, ask before writing rather than guessing. Voice is expensive to fix afterwards.

If the outline is missing, run `semantic-outline` first. If sources are missing, run `source-collection` first. Writing before either exists produces a draft that has to be rebuilt rather than edited.

## The rules, in priority order

### 1. Follow the outline strictly

Every section in the outline appears in the draft, in the same order, under the same heading, opening with the direct answer the outline specifies. Word budgets are targets, not suggestions — a section that runs triple its budget unbalances the piece.

**If the outline is wrong, stop and say so.** Sometimes writing reveals a structural problem the outline didn't — a section with nothing to say, a missing step, an order that doesn't build. Flag it and propose the fix. Do not silently restructure; the outline is the agreed plan, and quietly departing from it means the user is reviewing something they didn't approve.

### 2. Use only the provided sources

- Every factual claim is backed by a source from the pack, or is the user's own experience or data, or is cut.
- **Never invent a citation.** No plausible-sounding statistics, no half-remembered studies, no "research shows" without the research in hand.
- **Never source from memory mid-draft.** If a section needs evidence the pack doesn't have, mark it `[NEEDS SOURCE: what's needed]` and keep writing. Those markers are a feature — they show the user exactly where the argument outran the evidence.
- Attribute in the prose, not just a link: "McKinsey's 2025 survey of 1,200 executives found…" is citable by an AI model. "Studies show…" with a hyperlink is not.

### 3. Write answer-first, everywhere

- **The opening.** 40–60 words that directly answer the title question, quotable standing alone. No scene-setting, no "in today's rapidly evolving landscape", no throat-clearing. The first sentence is the one a model will lift.
- **Every section.** Opens with its own direct answer, then explains. A reader who lands mid-article gets the answer immediately.
- **Then go one click deeper.** The reasoning or mechanism behind the answer is what separates a citable source from a snippet that gets paraphrased and discarded.

### 4. Write so each section stands alone

A model should be able to extract any single section as a complete answer without the surrounding context. In practice: no "as mentioned above", no "building on the previous section", no pronouns whose antecedent is two headings back. Name the thing again. Mild repetition reads fine and retrieves well.

### 5. Keep entities consistent

The primary entity from the outline is named identically every time. No switching between the full name, an abbreviation, and a nickname — that's how a model loses track of who's being discussed.

### 6. Formatting that helps retrieval

- Short paragraphs, 2–4 sentences.
- Bullets and numbered lists where the content is genuinely a list. Not as decoration.
- A table where the content is a comparison. Comparison content is disproportionately valuable for AI citation, and a table is the format models extract most reliably.
- Bold for the load-bearing sentence in a long section, sparingly.
- One H3 level maximum.

### 7. Include the FAQ block

From the outline. Questions phrased exactly as someone would type them into Google or ChatGPT. Each answered in 2–3 sentences, answer-first. This is one of the highest-leverage sections in the piece for both featured snippets and AI citation.

### 8. Numbers stay specific

"+938% visitors in six months" beats "significant growth", always. If the source gives a specific figure, use it. If the user has original data, lead with it — it's the only thing in the piece a competitor can't also cite.

## Writing quality

- **Plain English.** Every acronym gets its meaning on first use. If a simpler word does the same work, use it.
- **No filler transitions.** "It's important to note", "at the end of the day", "in conclusion", "let's dive in", "unlock", "leverage" as a verb, "in today's fast-paced world", "game-changer", "seamless". These are the phrases that make a draft read as generated.
- **Vary sentence length.** Uniform sentence rhythm is the clearest tell of machine writing.
- **One point of view, stated once.** The credibility tie from the outline appears once, naturally — not as a pitch in every section.
- **Don't hedge everything.** "May potentially sometimes help" says nothing. If the source supports the claim, state it.

## Before handing over

Check and report:

- Every outline section present, in order?
- Every claim sourced, marked `[NEEDS SOURCE]`, or drawn from the user's own experience?
- Any citation in the draft that isn't in the source pack? (There must be none.)
- Does each section survive being read alone?
- Is the primary entity named consistently throughout?
- Word count against the outline's total budget.
- Is there at least one specific, verifiable number?

Report failures honestly rather than fixing them invisibly. A `[NEEDS SOURCE]` marker left in place is more useful than a claim quietly softened until it says nothing.

---

## Output

Save `DRAFT-[topic-slug]-v1.md` in the outputs folder and present it. The `DRAFT` prefix is deliberate — it should be obvious in a file list that this isn't final.

Structure:

1. **Draft status line** at the top: date, version, what it was built from, and that it needs editing before publication.
2. The article itself: H1, answer paragraph, sections, FAQ block.
3. **Sources used** — the full list, so the citations can be checked against the pack.
4. **Open items** — every `[NEEDS SOURCE]` marker, anywhere the outline was departed from and why, and anything the user needs to supply (a number, an example, a screenshot, a personal anecdote the draft has left a gap for).

## After the output

Offer in one line: running `seo-article-audit` on the draft, or a second pass on specific sections the user flags.

## What not to do

- Don't publish-polish. This is v1; over-polishing a draft that will be restructured wastes the effort.
- Don't pad to hit a word count. A short section that fully answers its question is finished.
- Don't fill a `[NEEDS SOURCE]` gap by weakening the claim until it needs no source. That's how an article ends up saying nothing.
- Don't write a conclusion that restates the article. End on the most useful thing, or a clear next step.

