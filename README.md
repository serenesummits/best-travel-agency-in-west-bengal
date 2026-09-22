# Serene Summits — West Bengal (SEO Site)

Static HTML/CSS site: 1 homepage + 23 district pages + 75 town pages, each
targeting "Best Travel Agency in [Place]" search intent, with unique on-page
content, meta tags, canonical URLs, Open Graph tags and TravelAgency JSON-LD
schema per page, plus a full sitemap.xml and robots.txt.

## Before you deploy — edit these

1. **`generate.py` → `BUSINESS` dict at top of `data.py`**
   - `email`: currently a placeholder (`info@serenesummits.in`) — set your real one.
   - `base_url`: currently `https://serenesummits.in/west-bengal` — change if this
     will live at a different domain or path (e.g. a brand-new domain, or your
     GitHub Pages URL like `https://yourusername.github.io/repo-name`).
   - `address_region`: add a real street address if you want full NAP (Name,
     Address, Phone) consistency for local SEO — currently region-only.
   - Phone number is already set to **+91 86382 26178**.
2. Add a real logo at `assets/img/logo.png` (referenced in the schema markup;
   currently that path doesn't exist yet — either add the file or remove the
   `image` field in `schema_localbusiness()` in `generate.py`).
3. If you change anything, re-run `python3 generate.py` — it rebuilds every
   page from `data.py`, so you never hand-edit the HTML files directly.

## Deploying to GitHub Pages

1. Create a new GitHub repo (or a folder inside your existing `serenesummits.in` repo).
2. Copy everything in this `out/` folder into the repo (or into a `west-bengal/`
   subfolder if you're nesting it under your existing site).
3. Commit and push.
4. In the repo's **Settings → Pages**, set the source to the branch/folder you pushed to.
5. Once live, submit `sitemap.xml` in Google Search Console for faster indexing.

## Structure

```
index.html                          Homepage — directory of all districts
about/index.html
contact/index.html
services/index.html
{district-slug}/index.html          23 district pages
{district-slug}/{town-slug}/index.html   75 town pages nested under their district
assets/css/style.css
assets/js/main.js
sitemap.xml
robots.txt
```

## Adding more towns or districts later

Everything is generated from `data.py`. To add a town, add an entry to the
relevant district's `"towns"` dict (needs a `name` and a one-line `note`), then
re-run `python3 generate.py`. To add a whole new district, copy the shape of
an existing entry in `DISTRICTS` and add its slug to the right division in
`DIVISIONS`.

## SEO notes

- Each page has a unique `<title>`, meta description, canonical URL, and
  `TravelAgency` JSON-LD schema scoped to that place.
- District pages link down to their town pages; town pages link back up to
  their district and sideways to nearby towns — this internal linking is what
  helps Google understand the site's geographic structure (a "silo").
- Content per page is written to be genuinely different (real facts about
  each district/town), not spun/duplicated text, which search engines
  penalize.
- `sitemap.xml` lists all 102 URLs; `robots.txt` points to it.
