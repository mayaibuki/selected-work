# Jorge Maya · Selected Work

Case-study sampler deck. Live: **https://selected-works.mayaibuki.com**

Full case studies at [mayaibuki.com](https://mayaibuki.com).

---

## Working on the deck

### Files

- `deck.html` — the deck. Everything is here: CSS in the `<style>` block near the top, each slide is a `<section class="slide …">` further down. Fonts and images are embedded as base64, so the file is large (~5.9 MB); search with Cmd+F instead of scrolling.
- `index.html` — a copy of `deck.html` that GitHub Pages serves. Regenerate it from `deck.html` before every push (see below).
- `og-image.png` (repo root) — the social preview image, a rendered PNG of slide 2. The only asset that is not embedded, because Open Graph images cannot be data URIs.
- `CNAME` (repo root) — holds the custom domain.

### Hosting

| Item | Value |
|---|---|
| Repo | `mayaibuki/selected-work` |
| Branch / path | `main`, root |
| Domain | `selected-works.mayaibuki.com` (GitHub Pages + `CNAME`) |
| Old URL | `https://mayaibuki.github.io/selected-work/` — 301-redirects to the custom domain |

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

Pages redeploys in about a minute.

### Export to PDF

Open the deck in Chrome → Print (Cmd+P) → Save as PDF. Print CSS emits one 1280×720 page per slide. Enable "Background graphics".

---

## Deck structure

12 slides, in this order:

| # | Slide |
|---|---|
| 1 | Cover |
| 2 | Bio / intro — "A story of making products users love" |
| 3 | ERGO NEXT — AI quote funnel (live embedded prototype) |
| 4 | ERGO NEXT — design system for AI agents |
| 5 | Mailchimp — migration roadmap / behavior change |
| 6 | Mailchimp — homepage refresh |
| 7 | Mailchimp — semantic-token design system |
| 8 | BBVA — Glomo mobile banking app |
| 9 | BBVA — Blue, first AI assistant in banking |
| 10 | Graava — AI action camera |
| 11 | More selected work — 6-card grid (Velo, Rogers & Fido, Vegan Moto Club, BBVA Agent, BBVA Bedrock, 31 Cats) |
| 12 | Closing / Thanks |

---

## Editing notes

- **Accent color**: the class after `project` on each slide sets it (`ergo`, `mc`, `bbva`, `coral`, `velo`, `rogers`, `graava`, `vmc`, `cats`), defined in the CSS "Per-project accents" block.
- **Slide structure** (STAR): left rail = eyebrow + headline + `.p-body` paragraphs (Situation / Task / Action) + `.spec` table; right = `.visual` panel + `.metrics` cards (the Results).
- **Images**: case-study slides use transparent PNGs sitting directly on the project's tint colour. There is no white card frame. The rule is `.visual img` with `object-fit: contain`, so nothing is cropped. All images are base64 data URIs.
  - **One exception**: `.proto-frame` on the ERGO funnel slide (3) keeps a white frame, because it frames the live prototype iframe. That frame is intentional — leave it.
- **Placeholders**: placeholders are `<div class="ph">…</div>` inside a `.visual`. Put an `<img src="…" alt="…" onerror="this.remove()">` next to it and the placeholder auto-hides (`.visual:has(img) .ph { display:none }`).
- **Slide 2 layout is tuned, not arbitrary**: the portrait column is 420px. The headline must stay on one line at 42px, which needs 727px of width, and the left column + 48px gap + 64px left padding are balanced against that. Widening the portrait will wrap the headline.
- **Social metadata**: the `<head>` carries Open Graph + Twitter card tags and a favicon. The OG image is referenced by absolute URL (`https://selected-works.mayaibuki.com/og-image.png`). If the domain ever changes, update every absolute URL in the `<head>`.
- **No external CSS/JS** — the deck must stay a single self-contained file.

### Copy rules (kept consistent across the deck)

- Facts come only from the career source-of-truth docs; do not invent metrics.
- Public surface: year-only dates (no months), no phone number.
- No em dashes. Concise, understated, first person where natural.
- "sole designer" appears exactly once (the ERGO design-system slide).

---

## Known pending

- **HTTPS certificate.** GitHub has not issued the Let's Encrypt cert for the custom domain yet, so HTTPS may fail while HTTP works. Once the cert exists, enforce HTTPS:

  ```bash
  gh api -X PUT repos/mayaibuki/selected-work/pages -F https_enforced=true
  ```

  If the cert is still missing after several hours, clear the custom domain in repo Settings → Pages, save, then re-enter it to re-trigger provisioning.
- **Live prototype on slide 3.** It is an external iframe: blank offline, and unreliable in PDF export. A static screenshot fallback for print is an option, not done yet.
- **File size.** The deck is ~5.9 MB. Subsetting the embedded fonts would cut roughly 1.5–2 MB if load time becomes a concern.
