---
name: "featured-image"
description: "Design a blog featured image (hero image) from a finished article — reads the piece, picks the visual concept, writes a production-ready Nano Banana Pro prompt, and optionally generates the image in Gemini. Use whenever the user asks for a featured image, hero image, blog image, cover image, OG image, thumbnail, header graphic, \"an image for this post\", \"what should the image be\", \"make me a banner\", or asks for an image prompt for Nano Banana / Gemini / Midjourney. Also runs as the final step of the SEO/AEO/GEO article pipeline, after the audit. Outputs the prompt, alt text, filename and social crop notes — and the image file itself when generation is approved."
---

# Featured Image

Turns a finished article into its featured image: the concept, a production-ready prompt for **Nano Banana Pro** (Google's `gemini-3-pro-image-preview`), the alt text, and the file naming. Generates the image itself when the user wants that and approves it.

**The image is not decoration.** It's the thumbnail in search results, the card on LinkedIn, and the first thing a reader judges the piece by. A generic stock-photo-shaped image says the article is generic. So this skill starts from what the article actually argues, not from its keywords.

---

## Inputs

Work from whichever exists, in this order:

1. **The finished draft or published article** — best case. Read it properly; the concept comes from the argument, not the title.
2. **The semantic outline** — its *Image plan* section already names what's needed and the alt text. Follow it rather than inventing a new direction.
3. **A title only** — workable, but say plainly that the concept is built on the title alone and will be more generic for it.

Confirm three things, asking only what can't be inferred:

- **Where it will be used** — blog hero, Open Graph card, LinkedIn, or all three. This sets the aspect ratio and how much text can survive the crop.
- **Whether the CMS overlays the title** on the image. If it does, the image must not contain the title as well, and needs deliberate empty space for the overlay.
- **Which Gemini tier** the user is on. This decides the visible watermark question below, and it's the one that most often ruins a hero image after the work is done.

If the project has a visual guidelines or brand assets folder, read it first — the palette, typography and logo usage should come from there rather than being invented. If there's no brand system yet, ask the user for their colours, fonts and any reference images, and treat the palette in Step 3 as a placeholder to replace.

---

## Step 1 — Find the one idea

Read the article and write a single sentence: *"This image has to make someone feel ___ about ___ in under a second."*

Then pull out:

- **The central claim** — the thing the article proves. Usually the answer paragraph.
- **The most concrete noun in the piece** — a real object, place, tool or number. Concrete beats conceptual every time, because "strategy" and "growth" have no shape but a filing cabinet does.
- **The original data point**, if there is one. A specific figure is often the strongest possible hero image on its own, set large.

An image that tries to carry the whole article carries nothing. One idea.

## Step 2 — Pick the archetype

Four options. Pick deliberately and say why, because the archetype decides everything downstream.

| Archetype | Use when | Watch out for |
|---|---|---|
| **Typographic poster** | The title or a single number is the hook. Strong match for text-forward, minimal brands. | Text must be short — under about 8 words. Long strings are where image models still fail. |
| **Conceptual still life** | There's one concrete object that carries the metaphor. | Don't stack metaphors. One object, well lit. |
| **Abstract geometric** | The piece is about a system, process or relationship. | Slides into generic corporate wallpaper fast. Needs a real structural idea. |
| **Editorial illustration** | Human situations, opinion pieces, personal stories. | Hardest to keep on-brand across a series. |

**Rotate across a series.** Five typographic posters in a row on a blog index looks like a template, not a body of work.

**A note worth taking seriously:** for a pure typographic poster in a simple flat brand style — solid colour, a defined typeface, basic geometric shapes — a hand-built SVG or HTML render is *better* than any image model. The hex values are exact, the font is real, the text is guaranteed correct, and it takes seconds. Offer that when the archetype is typographic and the layout is simple. Use Nano Banana Pro where it actually wins: texture, light, depth, objects, illustration, and typography that needs to feel physical rather than placed.

## Step 3 — Lock the brand

Pull the real brand system from the user's guidelines or existing assets. If a source uses a different aspect ratio (say a 4:5 carousel while this is 16:9), translate the *language*, not the layout.

Establish and write down, before prompting:

| Element | What to capture |
|---|---|
| **Palette** | The exact hex values for background, primary, accent, and text. |
| **Typography** | The typeface and its character (e.g. geometric sans, editorial serif, monospace). |
| **Shape language** | Any recurring motif — circles, hard rules, rounded cards, none. |
| **Composition** | Default alignment and where visual weight sits. |
| **Attribution** | How a byline or URL appears, if it appears at all. |

If the user has no brand system, use this **neutral placeholder palette** and say clearly that it's a placeholder to swap for their own:

| Role | Hex |
|---|---|
| Background | `#F5F1E8` |
| Primary | `#2B4C7E` |
| Accent | `#D98E48` |
| Text | `#1A1A1A` |
| Secondary text | `#6B6B6B` |

**Always quote hex values in the prompt.** "Warm terracotta" gets an approximation; a specific hex gets much closer.

**General principles that hold across most brands:**

- **Name the typeface explicitly and describe its character** (technical, editorial, evenly spaced) rather than naming a font the model may not have.
- **Flat solid backgrounds** usually read cleaner than gradients, drop shadows, or glow — unless the brand is deliberately rich.
- **Generous padding.** Content shouldn't bleed to the edge.
- **Use any signature motif sparingly**, and reserve it for hero images that open a series.
- **Keep composition consistent** with the brand's usual alignment and weight.

Match the brand's actual feel. Avoid defaulting to generic corporate SaaS, glossy 3D, gradient-mesh, or stock photography unless that is genuinely the brand.

## Step 4 — Write the prompt

Nano Banana Pro responds to a described scene, not a keyword list. Write in prose, ordered most to least important — the model weights the opening most heavily.

Cover these, in this order:

1. **Medium and format** — "A 16:9 editorial blog hero image, flat vector illustration" / "…minimalist studio photograph".
2. **The subject**, concretely and specifically.
3. **Composition** — what sits where, and crucially **where the empty space is**.
4. **Palette**, by hex.
5. **Typography**, only if the image carries text. Give the exact string in quotes and keep it short.
6. **Light and texture** — the thing that stops it looking generated. Named light ("raking late-afternoon light from the left") beats "good lighting".
7. **Mood**, in two or three words.
8. **What to exclude** — state as positives where possible ("flat matte surfaces" rather than "no gradients"), since exclusions phrased as negatives are less reliably followed.

**Rules that matter:**

- **Text goes in quotation marks, verbatim, and short.** Nano Banana Pro renders legible text far better than most models — that's its headline strength — but the failure rate climbs with length. Under 8 words. Check every generated character; a typo in a hero image is worse than no text.
- **Never let the model write the copy.** Give it the exact string. A model asked to "add a headline about SEO" will invent one.
- **Design for the crop.** Open Graph is 1.91:1 and 16:9 is 1.78:1, and LinkedIn and X crop differently again. Keep every important element — text, faces, the focal object — inside the middle 80%. Say so in the prompt.
- **If the CMS overlays the title**, the image must contain no text at all, and the prompt must specify a deliberately quiet region for the overlay: "the left third is uncluttered flat colour, reserved for a text overlay."
- **Ask for 16:9 at 2K.** 4K is slower and larger than a blog hero needs; 1K is thin on a retina display.

Also produce **two variants** — the chosen archetype and one genuinely different alternative. Not the same prompt reworded. A real choice takes one extra minute and avoids settling for the first thing.

## Step 5 — Generate it (only if the user wants the file)

The prompt alone is often the whole job. Generating is optional and needs a route:

**Reference images are the strongest lever available.** Nano Banana Pro accepts up to 14 reference images and holds style across them. Attaching existing on-brand assets (past hero images, brand boards, logo or pattern PNGs) locks the aesthetic far more reliably than any amount of prompt description. Recommend this whenever brand consistency matters.

**Routes, in order of preference:**

1. **Gemini app or Google AI Studio, by hand.** The user pastes the prompt and attaches the reference images. Most reliable, full control, no permissions needed. Default to this.
2. **Browser automation** via the Chrome tools, driving `gemini.google.com`, when the user asks for it to be done for them. Uses their logged-in session. **Ask before downloading the result** — name the file and where it's going. Never enter the user's email, a client domain, or any account details.
3. **API** — `gemini-3-pro-image-preview`, with `aspect_ratio` and `resolution` parameters. Needs a `GEMINI_API_KEY` in the environment. Mention it only if the user wants to script this repeatedly.

**The watermark, before generating anything:** every Google-generated image carries an invisible SynthID watermark, which is harmless. But free and **Google AI Pro** tiers also get a **visible Gemini sparkle** burned into the image — only AI Ultra removes it. On a blog hero that is a real problem, and it is much better raised now than discovered after the work is done. If the user isn't on Ultra, say so plainly and offer the SVG route for typographic images, which has no watermark at all.

## Step 6 — The publishing layer

Nothing here is optional; this is what connects the image to the SEO work.

- **Alt text** — describes the image for someone who can't see it, and is how vision models read it. Include any text that appears in the image. Describe, don't keyword-stuff: *"Flat editorial illustration in warm clay and cream, showing a single filing cabinet with one drawer open"* — not *"SEO featured image blog content marketing"*.
- **Filename** — `featured-[topic-slug].png`, matching the article's slug. Underscores and camelCase both read worse to crawlers than hyphens.
- **Dimensions** — 1600×900 for the blog hero; 1200×630 if the CMS wants a separate OG image.
- **File size** — under 200KB where possible. Featured images are the most common cause of a slow Largest Contentful Paint, and Core Web Vitals feed back into the ranking this whole pipeline exists to move. Convert to WebP unless the CMS won't take it.
- **Caption**, if the blog shows one — a sentence that adds something, not a restatement of the alt text.

---

## Output

Save `featured-image-[topic-slug].md` in the outputs folder and present it:

1. **The one idea** — the single sentence from Step 1
2. **Archetype chosen**, and why
3. **Prompt A** — the recommended one, ready to paste
4. **Prompt B** — the genuine alternative
5. **Reference images** to attach, if any
6. **Alt text, filename, dimensions, caption**
7. **Notes** — watermark tier, whether the CMS overlays text, anything the user needs to decide

If an image was generated, save it as `featured-[topic-slug].png` alongside and show it.

## After the output

Offer in one line: generating it in Gemini with the reference images attached, or building the typographic version as an exact-brand SVG instead.

## What not to do

- **Don't write the prompt from the title alone** when the article is available. The title is the topic; the article has the idea.
- **Don't ask a model to generate long text.** Anything over about 8 words belongs in a text overlay, not in the pixels.
- **Don't hand over a generated image without reading every character in it.** Text rendering is good now, not perfect.
- **Don't produce two variants that are the same idea reworded.** If both prompts would produce interchangeable images, there's only one variant.
- **Don't default to the typographic poster every time** because it's the easiest to keep on-brand. A blog index of identical posters is a template.
- **Don't skip the alt text.** It's the part that does SEO work, and it's the part most often left out.
