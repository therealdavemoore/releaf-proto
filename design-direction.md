# Releaf Cigars — Design Direction & Visual Brief

**Project:** Shopify → WordPress/WooCommerce Redesign  
**Date:** June 2026

---

## Design Philosophy

Releaf isn't just an online store — it's a neighborhood shop with a lounge. The design should feel like walking into that space: warm, unhurried, knowledgeable. Not stuffy or old-world exclusive, but not discount-retailer either. **The vibe is: trusted local expert who ships nationally.**

---

## Mood & Tone

**Words to design toward:**
- Warm. Rich. Deliberate. Grounded. Inviting.

**Words to avoid:**
- Corporate. Clinical. Flashy. Generic. Masculine-cliché (no fire, skulls, or 90s cigar bar excess).

**Reference experiences:**
- Walking into a well-curated whiskey bar
- A good independent bookstore
- A premium coffee roaster's retail space

---

## Color Palette

### Primary
| Name | Hex | Use |
|---|---|---|
| Tobacco Dark | `#1C1410` | Page backgrounds, nav |
| Warm Cream | `#F5EDD8` | Body text on dark, card backgrounds |
| Aged Amber | `#A0622A` | Accent, buttons, hover states |

### Secondary
| Name | Hex | Use |
|---|---|---|
| Cedar | `#6B3F2A` | Section dividers, secondary accents |
| Stone | `#8A8078` | Muted text, labels, metadata |
| Off-White | `#FAF6EF` | Light backgrounds, cards |

### Functional
| Name | Hex | Use |
|---|---|---|
| Success Green | `#4A7C59` | In stock, confirmation states |
| Sold Out | `#8A8078` | Out of stock badges |

**Overall approach:** Dark backgrounds for hero, nav, and feature sections. Light/cream backgrounds for product grids and editorial content. Amber accent is used sparingly — buttons, hover underlines, category callouts. Never use white-on-white or flat gray everything.

---

## Typography

### Typeface Direction

| Role | Style | Rationale |
|---|---|---|
| Display / Brand | Serif — elegant, slightly editorial | Commands presence on hero and section headers |
| Body / Product | Clean sans-serif — readable, neutral | Scannable in product grids and descriptions |
| Labels / Metadata | Monospace or small-caps sans | Strength, wrapper, vitola — clinical precision fits the detail layer |

### Candidate Typefaces (Google Fonts / free options)

**Display:**
- [Playfair Display](https://fonts.google.com/specimen/Playfair+Display) — editorial, warm serif
- [Cormorant Garamond](https://fonts.google.com/specimen/Cormorant+Garamond) — refined, old-world gravitas
- [Libre Baskerville](https://fonts.google.com/specimen/Libre+Baskerville) — sturdy and readable at all sizes

**Body:**
- [Inter](https://fonts.google.com/specimen/Inter) — neutral, highly readable, great at small sizes
- [DM Sans](https://fonts.google.com/specimen/DM+Sans) — slightly warmer than Inter, good contrast with serifs

**Metadata / Labels:**
- [DM Mono](https://fonts.google.com/specimen/DM+Mono) — pairs well with DM Sans
- Small-caps setting of the body font

### Scale (Desktop)
| Element | Size | Weight |
|---|---|---|
| Hero Headline | 64–80px | Serif, Light or Regular |
| Section Header | 36–48px | Serif, Regular |
| Product Name | 18–20px | Sans, Medium |
| Body Copy | 16px | Sans, Regular |
| Label / Metadata | 11–13px | Mono or Small-caps |
| Price | 18px | Sans, SemiBold |
| Button | 14px | Sans, Medium, All-caps or tracked |

---

## Layout Principles

- **Dark header/nav** always — white logo, minimal items
- **Full-width hero sections** for homepage, lounge, about pages
- **Card grid** for products — 4-up desktop, 2-up tablet, 1-up mobile
- **Generous whitespace** — this is a premium brand, not a clearance sale
- **Left-aligned text** for editorial content; centered sparingly for hero headlines
- **Horizontal rules / thin lines** as dividers rather than boxes or heavy borders

---

## Photography Direction

### Style
- **Atmospheric and editorial, not just product-on-white**
- Warm, slightly moody lighting — golden hour vibes, not harsh studio
- Depth of field — backgrounds soft, product or subject sharp
- Hands in frame are welcome — makes it human and tactile
- Smoke is appropriate used sparingly (not as a cliché — as texture)

### Priority Shots Needed from Client
1. The physical lounge space (wide, medium, detail shots)
2. The walk-in humidor (interior)
3. Staff / people shots (not posed corporate — natural, in context)
4. Product lifestyle shots (cigars in context: on a table with a drink, hands cutting a cigar)
5. Brand/packaging detail shots for featured products

### Until Photography is Available
- Source from Unsplash / Pexels with cigar lounge, whiskey bar, and premium retail searches
- Keep palette consistent with color spec above — warm, not cold

---

## UI Components

### Buttons
- **Primary:** Amber fill, dark text, 0 or 2px border-radius (squared feels more premium than pill-shaped)
- **Secondary:** Transparent with cream border
- **Ghost/text:** Underline on hover, no border
- All caps, tracked (letter-spacing: 0.08em), 14px

### Product Cards
```
[Product Image — 3:4 ratio]
[Brand Name — small, stone color, all-caps]
[Product Name — body, warm cream]
[Wrapper badge] [Strength badge]
[$Price]     [Quick Add →]
```
- On hover: image subtle zoom, Quick Add appears or becomes active
- Out of stock: desaturated image, "Notify Me" instead of Quick Add

### Navigation (Desktop Mega-menu)
```
[ RELEAF CIGARS logo ]  [ SHOP ▾ ]  [ SAMPLERS & GIFTS ]  [ THE LOUNGE ]  [ JOURNAL ]  [ ABOUT ]     [ 🔍 ]  [ 🛒 2 ]
                         ┌────────────────────────────────────────────────┐
                         │  BY BRAND    BY WRAPPER    BY STRENGTH         │
                         │  A–Z list    Connecticut   Mild                │
                         │              Habano        Medium              │
                         │              Maduro        Full                │
                         │              Natural                           │
                         │                            [View All →]        │
                         └────────────────────────────────────────────────┘
```

### Filter Bar (Shop page)
- Horizontal pill-style filters on mobile (scrollable row)
- Left-rail sidebar on desktop
- Active filters shown as dismissible tags below search bar
- "X products" count updates dynamically via AJAX

### Incentive Bar
```
[ ✈ Free shipping on orders $49+ ]  [ 🏷 10% off at $99 ]  [ 🔞 21+ only ]
```
- Sticky below nav on scroll
- Cream text on dark background
- Thin, 40px height

---

## WordPress Theme Direction

### Recommended approach
**Custom child theme on a minimal base** (GeneratePress or Blocksy) rather than a heavyweight page-builder theme. Keeps the site fast, gives full CSS control.

**Alternative:** Kadence or Astra with a dedicated WooCommerce child theme — faster to build, slightly less custom control.

**Avoid:** Divi, Avada, WPBakery — bloated, slow, hard to maintain.

### Key Plugins (Design-relevant)
- **WooCommerce** — core e-commerce
- **YITH WooCommerce Ajax Product Filter** or **FiFilters** — the filtering experience
- **Kadence Blocks** or **GenerateBlocks** — flexible editorial layouts
- **WP Rocket** or **Perfmatters** — performance (critical for e-commerce conversion)
- **Smush** or **ShortPixel** — image optimization

---

## Design Deliverables Checklist

- [ ] Moodboard (color palette + type specimen + photo references)
- [ ] Homepage wireframe (lo-fi)
- [ ] Homepage mockup (hi-fi, desktop)
- [ ] Homepage mockup (hi-fi, mobile)
- [ ] Product listing page mockup
- [ ] Product detail page mockup
- [ ] The Lounge page mockup
- [ ] Navigation mega-menu design
- [ ] Component library (buttons, cards, badges, filters, incentive bar)
- [ ] Style guide / design tokens document
