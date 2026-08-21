# RRE — Early-Stage Venture Capital Partner

A faithful local replica of the Webflow site **`rre-staging.webflow.io`**, rebuilt from the downloaded site bundle and the live staging pages.

## Structure

```
rre-ipr25/
├── index.html          # Homepage (Webflow markup, fully local assets)
├── portfolio.html      # Portfolio page (companies grid + category filters + search)
├── team.html           # Team page (partner/associate cards)
├── rrepov.html         # RRE POV podcast page
├── css/                # Site styles + vendor CSS (video.js, swiper, etc.)
├── js/                 # Webflow runtime + chunks, jQuery, GSAP, video.js, swiper
│   └── dist/           # Finsweet attributes library chunks (offline mirror of jsdelivr)
├── fonts/              # ABC Monument Grotesk (the site typeface)
├── images/             # All page imagery (logos, team photos, blog/testimonial images)
├── video/              # Background videos (homepage + per-page) and poster thumbnails
├── player/             # Local vidzflow video player pages (iframe targets)
├── serve.mjs           # Zero-dependency static file server (extensionless → .html)
└── package.json        # npm start / npm run serve
```

## Run locally

```bash
npm start
# or
node serve.mjs 8080
```

Then open <http://localhost:8080>. Clean URLs work too: `/portfolio`, `/team`, `/rrepov`.

## Notes

- All four pages (home, portfolio, team, RRE POV) are served fully locally — no CDN dependencies.
- The portfolio page's CMS-driven list was converted to a static grid: all available companies show by default (ALL filter), with working category filters, search, and click-to-open company sliders. Because the offline page only contains the first page of the Webflow CMS collection, some companies (e.g., Datadog) that the live site loads via its CMS fetch are not present locally.
- Individual team-member pages (`/team/<name>`) are not included; they 404 locally.
- Background videos are local per page: `video/rre-bg*.mp4` (home), `video/portfolio/*` and `video/team/*`.
- The Finsweet `attributes` library chunks are mirrored locally under `js/dist/`; `attributes.js` was patched to match its module `<script>` tags by filename so the `fs-mirrorclick`/`fs-scrolldisable` interactions work offline.
- SRI `integrity` attributes were removed from the locally-served CSS/JS tags.
- Images are loaded eagerly (`loading="eager"`) so nothing depends on lazy-load behavior.
- External links (blog posts, LinkedIn, X, LP/GP portals, podcasts) point to the real destinations exactly as the original site.
