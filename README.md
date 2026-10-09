# Ken Lee — Personal Site

Source for `https://litkhai.dev`, served by Vercel. A single-page profile:
intro, experience, sidebar credentials, selected work, and contact.

`https://litkhai.github.io` is still published from the same files by the
GitHub Pages workflow until it is turned into a redirect. Project sites under
`litkhai.github.io/<repo>/` are separate repositories and are not affected.

## Structure

- `index.html` — the entire page, including Person JSON-LD
- `palettes/paper-ink.css` — the only file with colour values (paper/ink,
  yellow accent); everything else uses its variables
- `styles.css` — layout and type
- `404.html` — not-found page
- `fonts/inter-latin.woff2` — self-hosted Inter, latin subset, weights 400–800
  (SIL Open Font License, see `fonts/OFL.txt`)
- `tools/og-card.html` — source the social card is rendered from
- `og-image.png` — 1200×630 social preview card
- `favicon.svg` · `favicon.ico` · `apple-touch-icon.png` — icons
- `robots.txt` — web-profile policy: search and answer bots allowed, training
  crawlers disallowed
- `vercel.json` — security headers (CSP trimmed to same-origin only) and font
  caching
- `.vercelignore` — keeps agent and repository files out of the deployment
- `.github/workflows/pages.yml` — GitHub Pages deployment (`litkhai.github.io`)

## Preview

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Deploy

Vercel project `litkhai-dev` in the `litkhai` team, connected to this
repository: a push to `main` deploys production, and a pull request gets a
preview deployment. `www.litkhai.dev` redirects to `litkhai.dev` with a 308.
`vercel link` writes `.vercel/` and `.env.local`, and both are gitignored.

Manual production deploy, if the Git integration is ever disconnected:

```bash
npx vercel --scope litkhai deploy --prod
```

## Checks

From a `khai-harness` checkout next to this one:

```bash
bash ../khai-harness/standards/frontend/profiles/web/harness/verify/lint-web.sh .
bash ../khai-harness/standards/frontend/profiles/web/harness/verify/exposure-check-web.sh https://litkhai.dev
```

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
