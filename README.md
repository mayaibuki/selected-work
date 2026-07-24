# Jorge Maya · Selected Work

Case-study sampler deck. Live: **https://mayaibuki.github.io/selected-work/**

Full case studies at [mayaibuki.com](https://mayaibuki.com).

---

## Working on the deck

### Files

- `deck.html` — the deck. Everything is here: CSS in the `<style>` block near the top, each slide is a `<section class="slide …">` further down. Fonts and most images are embedded as base64, so the file is large; search with Cmd+F instead of scrolling.
- `index.html` — a copy of `deck.html` that GitHub Pages serves. Regenerate it from `deck.html` before every push (see below).

### Preview locally

```bash
cd "/Users/mayaibuki/Documents/Claude/Job search 2026/recruiter-deck/case-study-deck"
python3 -m http.server 8000
```

Open http://localhost:8000/deck.html. Or use the VS Code **Live Server** extension (right-click `deck.html` → Open with Live Server).

Navigate: arrow keys / space, click the left or right half of a slide, or the on-screen prev/next buttons.

### Publish

```bash
cd "/Users/mayaibuki/Documents/Claude/Job search 2026/recruiter-deck/case-study-deck"
cp deck.html index.html
git add -A && git commit -m "your message" && git push
```

Pages redeploys in about a minute. Repo: `mayaibuki/selected-work`.

### Export to PDF

Open the deck in Chrome → Print (Cmd+P) → Save as PDF. Print CSS emits one 1280×720 page per slide. Enable "Background graphics".

### Editing notes

- **Accent color**: the class after `project` on each slide sets it (`ergo`, `mc`, `bbva`, `coral`, `velo`, `rogers`, `graava`, `vmc`), defined in the CSS "Per-project accents" block.
- **Slide structure** (STAR): left rail = eyebrow + headline + `.p-body` paragraphs (Situation / Task / Action) + `.spec` table; right = `.visual` panel + `.metrics` cards (the Results).
- **Add an image to a placeholder**: placeholders are `<div class="ph">…</div>` inside a `.visual`. Put an `<img src="…" alt="…" onerror="this.remove()">` next to it and the placeholder auto-hides (`.visual:has(img) .ph { display:none }`). Keep it self-contained: prefer a base64 data URI, or an https hotlink with the `onerror` fallback.
- **No external CSS/JS** — the deck must stay a single self-contained file.

### Copy rules (kept consistent across the deck)

- Facts come only from the career source-of-truth docs; do not invent metrics.
- Public surface: year-only dates (no months), no phone number.
- No em dashes. Concise, understated, first person where natural.
- "sole designer" appears exactly once (the ERGO design-system slide).

### Open TODOs

- **Slide 2 portrait** — replace the placeholder with a real portrait (vertical crop, chest up, plain/soft background).
- **Graava slide** — add a real camera-hardware / app image (currently a placeholder; no third-party press images).
- **Mailchimp design-system slide** — add a token/component screenshot (currently a placeholder).

### Current state

12 slides, one per project: cover, bio, ERGO design system, ERGO funnel, Mailchimp homepage, Mailchimp design system, Mailchimp migration, BBVA Blue, BBVA Glomo, Graava (featured), a "More selected work" card grid (Velo, Rogers/Fido, Vegan Moto Club, BBVA Agent, BBVA Bedrock), and the close.
