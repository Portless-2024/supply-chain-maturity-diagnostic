# Supply Chain Maturity Diagnostic

An interactive lead-gen diagnostic for Portless. Visitors answer 10 questions
about how they move inventory and capital, get a maturity grade
(Legacy → Growing → Optimized → Modern), and unlock a personalized breakdown
with category benchmarks and next moves. On email submit it posts the lead to
HubSpot.

Built in the "Portless Diagnostic" visual style — Geist / Geist Mono type,
warm-grey + royal-blue palette, square eyebrow pills, dashed maturity scale.

---

## What's in here

```
portless-diagnostic/
├── dist/
│   └── index.html                        ← DEPLOY THIS. Self-contained,
│                                            works offline, fonts inlined.
├── Supply Chain Diagnostic.dc.html        ← editable source (needs support.js
│                                            + assets/ alongside it)
├── support.js                             ← runtime for the source file
├── assets/
│   └── portless-logo-new.png              ← logo used by the source files
├── Portless Diagnostic Style Guide.dc.html ← visual style reference / specimen
├── Diagnostic Design Spec.md              ← written spec: colors, type, tokens,
│                                            component recipes
└── .gitignore
```

---

## Deploying (host as its own page)

`dist/index.html` is a single self-contained file. To put it live:

1. Rename or serve `dist/index.html` as your page (it's already `index.html`,
   so most static hosts serve it automatically).
2. Upload to any static host — Cloudflare Pages, Netlify, Vercel, S3, or your
   own web server. No build step, no dependencies.
3. Point a URL at it, ideally a subdomain of your main site
   (e.g. `diagnostic.portless.com`) so HubSpot's tracking cookie carries over.
4. Link to it from your marketing site.

## Editing the source

Open `Supply Chain Diagnostic.dc.html`. Keep `support.js` and `assets/` in the
same folder. After editing, regenerate `dist/index.html` by bundling the source
into a single self-contained file (all assets + fonts inlined).

---

## Before launch: wire up HubSpot

The email step currently posts to placeholder IDs. In the source file, find
`HS_PORTAL` and `HS_FORM` in the `unlock()` method and replace:

```js
const HS_PORTAL = 'YOUR_PORTAL_ID';
const HS_FORM   = 'YOUR_FORM_GUID';
```

with your real HubSpot Portal ID and Form GUID, then rebuild `dist/index.html`.
Until then the diagnostic runs end-to-end but submissions go nowhere.

For lead attribution, also add your HubSpot tracking script to the page so the
`hubspotutk` cookie is set on your domain.

---

## Notes

- Fonts (Inter Tight, Geist, Geist Mono) load from Google Fonts in the source
  and are inlined in `dist/index.html`, so the deployed file renders correctly
  on any machine, online or off.
- The `.dc.html` files are Design Components authored in the design tool; they
  open directly in a browser too.
