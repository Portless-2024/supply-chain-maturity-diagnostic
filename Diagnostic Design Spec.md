# Supply Chain Diagnostic — Design Spec (Claude reference)

> Purpose: a self-contained, machine-readable spec so Claude can reproduce the visual language of the
> Portless Supply Chain Diagnostic in any project WITHOUT further guidance. When the user says
> "reference the diagnostic style" (or points at this file), follow everything below literally.
> This is a spec for Claude, not a human style guide. All styling is INLINE (no CSS classes).

---

## 0. One-paragraph vibe
Clean, editorial, operator-facing. Near-white/cream grounds, a single royal blue as the only strong
accent, dark "ink" (#3E3B38) hairline borders on everything, Geist for all headings and body, Geist
Mono for eyebrows/labels/data. Square eyebrow pills, square number badges, lightly-rounded (10–12px)
cards and buttons, fully-rounded status pills. No drop-shadow drama, no gradient backgrounds except
the three defined below. Minimal, numerate, confident.

---

## 1. Fonts
Load in `<helmet>` (or `<head>`):
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Geist:wght@400;500;600;700&display=swap">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Geist+Mono:wght@400;500;600&display=swap">
```
Stacks (always include fallbacks):
- Sans: `'Geist',-apple-system,BlinkMacSystemFont,sans-serif`
- Mono: `'Geist Mono',ui-monospace,'SF Mono',Menlo,monospace`

Usage:
- **Headings** — Geist, weight **500** (medium). letter-spacing -0.01em to -0.015em. color #0B1233. Sizes: hero h1 ~52px, section h2 ~38px, card h3 ~27px.
- **Body** — Geist, weight **400**, size 15–19px, line-height 1.6, color **#596274**.
- **Eyebrows / labels / data figures / sources** — Geist Mono, weight **500**, color **#3E3B38** (or #8D95AD for sources).

---

## 2. Color tokens
| Token | Hex | Use |
|---|---|---|
| Royal blue | `#2050F2` | Primary accent, CTAs, markers, numerals, link hover |
| Ink | `#3E3B38` | ALL borders, eyebrow text/labels, header pills |
| Heading navy | `#0B1233` | Headlines, high-contrast text |
| Body | `#596274` | Paragraph / body copy |
| Muted | `#8D95AD` | Sources, captions, secondary text |
| Powder blue | `#8FA7F8` | Page-gradient base, marker halo (as #A9BEF8) |
| Cream | `#F3F0EA` | Cream card ground |
| Cream border | `#E3DDD1` | Dividers on cream / inner header bands |
| Light option border | `#D8DDE9` | Unselected option / neutral hairline on white |
| Legacy | `#FF5C28` | Grade-1 accent |
| Growing | `#F5A623` | Grade-2 accent |
| Optimized | `#1CA6B0` | Grade-3 accent |
| Modern | `#14A75A` | Grade-4 accent |

Links: default `#2050F2`, hover `#0822A0`.

---

## 3. Gradients (the only three allowed)
- **Page background** (white → powder blue, held white top & bottom so CTAs sit on light):
  `linear-gradient(180deg,#FFFFFF 0%,#FFFFFF 8%,#8FA7F8 48%,#8FA7F8 66%,#FFFFFF 88%,#FFFFFF 100%)`
- **Primary button** (powder → royal):
  `linear-gradient(180deg,#8FA7F8 0%,#2050F2 100%)`
- **Dark emphasis / lead-capture panel** (ink → near-black):
  `linear-gradient(180deg,#3E3B38 0%,#0E1117 100%)`

---

## 4. Radii & borders
- Cards / panels: **12px**. Result/hero panels: 12–14px.
- Buttons & inputs: **10px**.
- Status pills (score): **999px** (fully rounded).
- Eyebrow pills & number badges: **0** (square).
- Default border everywhere: **1px solid #3E3B38** (the "ink" hairline). Neutral/unselected hairlines on white use `#D8DDE9`; dividers on cream use `#E3DDD1`.
- Card shadow (subtle): `0 8px 24px rgba(13,31,95,0.06)`.

---

## 5. Component recipes (copy the inline styles)

### Eyebrow pill (section labels)
```html
<div style="display:inline-flex;align-items:center;font-family:'Geist Mono',ui-monospace,Menlo,monospace;font-weight:500;font-size:12px;letter-spacing:0.02em;text-transform:uppercase;color:#3E3B38;border:1px solid #3E3B38;border-radius:0;padding:6px 10px;background:transparent;white-space:nowrap;">Eyebrow label</div>
```
On dark panels: swap `color` and `border` to `#fff`.

### Number badge (square)
```html
<div style="width:34px;height:34px;border-radius:0;border:1px solid #3E3B38;background:#2050F2;color:#fff;font-family:'Geist Mono',ui-monospace,Menlo,monospace;font-size:14px;font-weight:600;display:flex;align-items:center;justify-content:center;">1</div>
```
Answer-option letter badges are the same, 26–28px.

### Score / status pill (fully rounded, optional line icon)
```html
<div style="display:inline-flex;align-items:center;gap:8px;border:1px solid #3E3B38;border-radius:999px;padding:7px 14px;">
  <!-- optional 14px line icon, stroke #3E3B38 stroke-width 2 -->
  <span style="font-family:'Geist',sans-serif;font-weight:600;font-size:14px;color:#3E3B38;">14 / 24 points</span>
</div>
```

### Primary button
```html
<button style="display:inline-flex;align-items:center;gap:12px;font-family:'Geist',sans-serif;font-weight:400;color:#fff;background:linear-gradient(180deg,#8FA7F8 0%,#2050F2 100%);border:none;border-radius:10px;cursor:pointer;box-shadow:0 10px 26px rgba(32,80,242,0.28);font-size:17px;padding:14px 26px;">Label<span style="font-size:20px;line-height:1;">&#8594;</span></button>
```
Hover: `filter:brightness(1.06)`. Always a trailing → arrow.

### White card
`background:#fff;border:1px solid #3E3B38;border-radius:12px;box-shadow:0 8px 24px rgba(13,31,95,0.06);padding:36px 40px;`

### Cream visual card (for titled diagrams)
Outer: `background:#F3F0EA;border:1px solid #3E3B38;border-radius:12px;overflow:hidden;`
White header band inside: `background:#fff;border-bottom:1px solid #E3DDD1;padding:22px 30px;` with a Geist 600 title, then the visual body on the cream ground below.

### Flush option list (radio-style)
Container `display:flex;flex-direction:column;gap:0;`. Each option:
`display:flex;align-items:center;gap:14px;padding:17px 20px;border-radius:0;margin-top:-1px;` (the -1px collapses shared borders). Unselected `border:1px solid #D8DDE9;background:#fff;color:#0B1233;`. Selected `border:1.5px solid #2050F2;background:#EEF2FF;color:#0822A0;` + higher z-index. Each row starts with a square letter badge.

### Divided list (e.g. steps)
Items in a column; each item `padding:22px 40px;margin:0 -40px;border-top:1px solid #E4E4F0;` so divider lines run full-bleed across the card (negative margin offsets the card's 40px padding).

### Dashed connector + dot markers (progress/scale visual)
Baseline: `height:1.5px;background:repeating-linear-gradient(90deg,#3E3B38 0 4px,transparent 4px 7px);` positioned absolutely between the end markers (e.g. left:12.5% right:12.5%).
Markers (royal core in powder halo): outer `width:28px;height:28px;border-radius:99px;background:#A9BEF8;` centering inner `width:15px;height:15px;border-radius:99px;background:#2050F2;`.

### Source links
Whole label underlined, muted, brand-blue on hover:
```html
<a href="…" target="_blank" rel="noopener" style="color:#8D95AD;text-decoration:underline;text-underline-offset:2px;font-family:'Geist Mono',monospace;font-size:12px;" onmouseover="this.style.color='#2050F2'" onmouseout="this.style.color='#8D95AD'">Full source name, 2026</a>
```
Multiple sources on one line = separate links with an UNLINKED separator ("; ") between them, so they read as distinct.

---

## 6. Rules of thumb
- One strong accent only (#2050F2). Everything structural is ink hairline on white/cream.
- Eyebrows and number badges are SQUARE; status pills are fully round; cards/buttons lightly rounded.
- Sentence case for headings and buttons; UPPERCASE only for mono eyebrows.
- No emoji. No decorative gradients beyond the three above. No heavy shadows.
- Numbers earn space — anchor claims to a unit, cite sources as links.
- Assets: the Portless logo lives at `assets/portless-logo-new.png` (copy it into new projects).
