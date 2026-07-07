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
├── index.html                            ← THE LIVE PAGE. Self-contained,
│                                            works offline, fonts inlined.
│                                            This is what GitHub Pages serves.
├── .nojekyll                             ← tells GitHub Pages to skip Jekyll
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

> `index.html` (the standalone build) lives at the repo root so GitHub Pages
> serves the diagnostic — not this README — at the site URL. When you edit the
> source, rebuild and overwrite this root `index.html`.

---

## Deploying (host as its own page)

The root `index.html` is a single self-contained file. To put it live:

**GitHub Pages (what you're using):** in the repo's Settings → Pages, set the
source to your default branch, root folder. Because `index.html` is at the root,
Pages serves the diagnostic at
`https://<user>.github.io/<repo>/`. (Without a root `index.html`, Pages falls
back to rendering this README — that's why it looked wrong at first.)

**Any other static host** (Cloudflare Pages, Netlify, Vercel, S3, your own
server): upload `index.html`. No build step, no dependencies. Ideally serve it
from a subdomain of your main site (e.g. `diagnostic.portless.com`) so HubSpot's
tracking cookie carries over, then link to it from your marketing site.

## Editing the source

Open `Supply Chain Diagnostic.dc.html`. Keep `support.js` and `assets/` in the
same folder. After editing, regenerate the root `index.html` by bundling the
source into a single self-contained file (all assets + fonts inlined).

---

## Before launch: wire up HubSpot

The email step currently posts to placeholder IDs. In the source file, find
`HS_PORTAL` and `HS_FORM` in the `unlock()` method and replace:

```js
const HS_PORTAL = 'YOUR_PORTAL_ID';
const HS_FORM   = 'YOUR_FORM_GUID';
```

with your real HubSpot Portal ID and Form GUID, then rebuild the root `index.html`.
Until then the diagnostic runs end-to-end but submissions go nowhere.

For lead attribution, also add your HubSpot tracking script to the page so the
`hubspotutk` cookie is set on your domain.

---

## Notes

- Fonts (Inter Tight, Geist, Geist Mono) load from Google Fonts in the source
  and are inlined in the root `index.html`, so the deployed file renders correctly
  on any machine, online or off.
- The `.dc.html` files are Design Components authored in the design tool; they
  open directly in a browser too.
