# SEO/AEO/GEO context pack

This file is what makes the pipeline write as *you* — your voice, your market, your sources, your
brand — instead of generic content. Every skill reads it before it runs.

**Two ways to fill it in:**

1. Run the setup skill — say *"set up the SEO agent"* or invoke `seo-aeo-geo:setup`. It interviews
   you and writes a completed `seo-context.md` into your project for you.
2. Or copy this file to your project root as `seo-context.md` and fill in each field by hand.

Leave a field blank only if you genuinely have no preference — the skills fall back to sensible
neutral defaults and will tell you when they're guessing. The more you fill in, the less the
pipeline has to ask mid-task.

Save the completed file as **`seo-context.md`** in your project root (the skills also check
`.claude/seo-context.md`).

---

## Who

- **Operator / brand name:** <!-- the name the content is published under, used identically everywhere for entity consistency -->
- **One-line description of who you are:** <!-- e.g. "a fractional CMO serving B2B SaaS founders" -->
- **Credibility angle:** <!-- what makes you worth citing on your topics — the single tie the article makes to your expertise -->

## Sites

- **Primary site:** <!-- e.g. example.com — the main publishing destination and internal-link hub -->
- **Other sites / properties:** <!-- any others the content might link to or be published on -->

## Market

- **Primary market:** <!-- country / region — changes phrasing, spelling, competitors, search volumes -->
- **Other markets:** <!-- if you publish for more than one -->
- **Location for search-data lookups:** <!-- the city or region to resolve a real location ID against when a search tool needs one; name the specific city, not just the country -->

## Voice & style

- **Spelling / locale:** <!-- e.g. Australian (-ise, colour), US, UK -->
- **Point of view:** <!-- first person singular, first person plural (we), third person -->
- **Tone:** <!-- e.g. plain, direct, warm; no hype -->
- **Words / phrases to avoid:** <!-- your personal banned list on top of the pipeline's built-in anti-cliché rules -->
- **A short sample of your writing:** <!-- paste 3–5 sentences you've written, or link a page — the strongest single signal for matching your voice -->

## Sources

- **Preferred lead publishers:** <!-- the 3–6 sources you want cited first when relevant — e.g. specific consultancies, journals, research bodies, trade press. Leave blank to use broadly-trusted defaults (peer-reviewed journals, government statistics bodies, major consultancies, primary research). -->
- **Sources to avoid:** <!-- anything you never want cited -->

## Search-data tool

- **Connected search/SEO MCP:** <!-- e.g. Ubersuggest, Ahrefs, none. If none, the pipeline uses web search + reasoning and labels every figure an estimate. -->
- **Usage cap, if any:** <!-- e.g. "Ubersuggest free tier: 3 reports/day". The agent budgets its calls against this and stops rather than burning through it. -->

## Brand visual system (for featured images)

- **Colour palette (hex):** <!-- your brand colours as hex values — quoted exactly, these go straight into image prompts. Leave blank to use a neutral placeholder palette. -->
- **Typography:** <!-- typeface or type feeling — e.g. "monospace, technical, editorial" -->
- **Shape / motif language:** <!-- any recurring visual signature — e.g. "flat colour, generous padding, no gradients" -->
- **Brand guidelines file / folder:** <!-- path to a brand or visual-guidelines doc the featured-image skill should read, if you have one -->

## Publishing (facts, not a connection)

- **CMS:** <!-- e.g. WordPress, Ghost, Webflow — used only to shape outputs, not to publish for you -->
- **Does your CMS overlay the post title on the featured image?** <!-- yes/no — if yes, the image is generated with no text and a quiet region for the overlay -->
- **Separate Open Graph image needed?** <!-- yes/no and size, if your CMS wants one distinct from the hero -->

## Original material you can bring

<!-- The single biggest lever on whether a piece gets cited is data only you have. List what you
can supply per piece: client results, campaign numbers, survey data, screenshots, transcripts,
first-hand experience. The pipeline will ask for these by name at the outline stage. -->
