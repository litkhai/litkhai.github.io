# Ken Lee — Personal Site

Source for `https://litkhai.github.io`. A single-page profile: intro, experience,
sidebar credentials, selected work, and contact.

## Structure

- `index.html` — the entire page, including Person JSON-LD
- `styles.css` — visual system (light, paper/ink, yellow accent)
- `404.html` — not-found page
- `fonts/inter-latin.woff2` — self-hosted Inter, latin subset, weights 400–800
  (SIL Open Font License, see `fonts/OFL.txt`)
- `tools/og-card.html` — source the social card is rendered from
- `og-image.png` — 1200×630 social preview card
- `favicon.svg` · `favicon.ico` · `apple-touch-icon.png` — icons
- `.github/workflows/pages.yml` — GitHub Pages deployment

## Preview

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Regenerating the images

The card and the icons are rendered from HTML with headless Chrome, so they stay
in the same design system as the page:

```bash
chrome --headless=new --window-size=1200,630 --force-device-scale-factor=1 \
  --screenshot=og-image.png "file://$PWD/tools/og-card.html"
```

`favicon.ico` is `favicon.svg` rendered at 32×32 and wrapped in an ICO container.

## Content notes

- Career content is derived from the LinkedIn profile at
  [linkedin.com/in/keehoonlee](https://www.linkedin.com/in/keehoonlee/).
- Phone number is deliberately not published.
- Selected work is maintained by hand. When a repository gains a docs site or a
  new one appears, the tiles need updating — check
  `gh repo list litkhai --visibility public`.
- Keep the page to one screen-length of scroll; move long-form material to
  linked project sites rather than growing this page.
