# Releaf Cigars — WooCommerce Migration Plan

**From:** Shopify  
**To:** WordPress + WooCommerce  
**Date:** June 2026

---

## Overview

This migration involves three major workstreams running in parallel:
1. **Data migration** — products, customers, orders from Shopify → WooCommerce
2. **Platform setup** — WordPress + WooCommerce environment, plugins, theme
3. **Design build** — new site design implemented in WordPress

Go-live should only happen when all three are complete and validated in staging.

---

## Phase 0: Pre-Migration Decisions (Client Input Required)

Before touching any data, get answers to these:

| Question | Why It Matters |
|---|---|
| Migrate all 1,344 SKUs or only in-stock (726)? | Determines import scope and redirect list size |
| Migrate historical orders? | Affects customer history, accounting, loyalty |
| Migrate customer accounts? | Password hashing differs — customers may need to reset |
| Keep the same domain? | Yes = DNS cutover plan needed |
| Current payment processor? | Tobacco is high-risk — must confirm WooCommerce gateway compatibility |
| Are there Shopify product reviews? | If yes, export them now (Shopify deletes data on plan cancellation) |
| Is there a loyalty/rewards program? | Needs equivalent in WooCommerce |

---

## Phase 1: Environment Setup

### Hosting Requirements
Cigars/tobacco e-commerce needs a host that:
- Allows age-restricted product sales
- Supports WooCommerce at scale (1,000+ SKUs)
- Has staging environment capability

**Recommended hosts:**
- **WP Engine** — managed WordPress, excellent staging, WooCommerce optimized
- **Kinsta** — fast, developer-friendly, good WooCommerce support
- **Cloudways** — flexible, good performance, lower cost

### WordPress Stack
```
WordPress (latest)
└── WooCommerce (latest)
    ├── Theme: GeneratePress or Blocksy (base) + custom child theme
    ├── YITH WooCommerce Ajax Product Filter
    ├── WooCommerce Product Add-Ons (for gift notes, etc.)
    ├── Age Gate or Age Checker for WooCommerce (21+ verification)
    ├── WP Rocket (caching + performance)
    ├── Yoast SEO or Rank Math (with WooCommerce SEO module)
    ├── WooCommerce Stripe Gateway or Authorize.net (confirm processor)
    └── ShortPixel or Imagify (image optimization)
```

### Payment Gateway — Critical Decision
Tobacco/cigar retailers are classified as **high-risk merchants**. Standard processors (Stripe, Square) may reject or terminate accounts without warning.

**Confirmed WooCommerce-compatible high-risk options:**
- **Authorize.net** — widely used, stable, WooCommerce plugin available
- **PayKings** — specializes in high-risk, WooCommerce integration
- **Durango Merchant Services** — high-risk specialty
- **NMI (Network Merchants)** — gateway-only, works with many high-risk acquirers

Confirm current Shopify payment processor and whether they have a WooCommerce integration before switching.

### Age Verification
- Install age gate plugin on site entry and/or at checkout
- Options: **Age Gate** (free), **WooCommerce Age Verification** (premium)
- Must be compliant: collect DOB or simple 21+ confirmation
- Consider whether to gate the whole site or only checkout

---

## Phase 2: Product Data Migration

### Step 1 — Shopify Export
From Shopify Admin → Products → Export:
- Export all products as CSV (includes variants, pricing, images, inventory)
- Export separately: collections, metafields (if using custom attributes)
- Export customer data: Admin → Customers → Export
- Export orders if migrating history: Admin → Orders → Export

**Do this before canceling Shopify.** Data access ends when the plan is canceled.

### Step 2 — Clean and Enrich the CSV
The Shopify CSV will not include wrapper type, strength, origin, or vitola — these attributes need to be added manually or sourced.

**Process:**
1. Open Shopify export in Google Sheets or Excel
2. Add columns: `wrapper`, `strength`, `origin`, `vitola`, `format`
3. Fill in for all 1,344 SKUs (or a subset — this is the most labor-intensive step)
4. Decision: can the client provide this data? Are any attributes on the Shopify product pages already?

**Shortcut:** Start with in-stock SKUs only (726) for launch, migrate out-of-stock later.

### Step 3 — WooCommerce Import
Use **WooCommerce Product CSV Import Suite** (built into WooCommerce) or **WP All Import Pro** (more flexible):
- Map Shopify CSV columns to WooCommerce fields
- Import product attributes (wrapper, strength, etc.) as WooCommerce product attributes
- Import images — WooCommerce can pull from URLs in the CSV (Shopify CDN URLs work temporarily)

### Step 4 — Image Migration
Shopify hosts images on their CDN. After migration:
- Re-upload images to WordPress media library OR
- Use **Auto Upload Images** plugin to pull from Shopify CDN URLs during import and host locally

Shopify CDN URLs remain accessible for a period after migration but should not be relied on long-term.

### Step 5 — Inventory Sync (if staying live on Shopify during build)
If the store remains live on Shopify during the WordPress build:
- Do not import inventory until launch day or use a real-time sync tool
- At launch: export fresh inventory CSV from Shopify, import to WooCommerce, flip DNS

---

## Phase 3: Taxonomy and Attribute Setup

Set up WooCommerce product attributes BEFORE importing products:

```
Product Attributes (WooCommerce Admin → Products → Attributes):
- Wrapper: Connecticut | Habano | Maduro | Natural | Oscuro
- Strength: Mild | Medium | Full
- Origin: Dominican | Honduran | Nicaraguan | Ecuadorian | Cuban | Honduran | etc.
- Vitola: Robusto | Toro | Churchill | Gordo | Belicoso | Lonsdale | etc.
- Format: Single | 5-Pack | Bundle | Gift Set

Product Categories (hierarchical):
- Shop (parent)
  - By Brand → [each brand as subcategory]
  - By Wrapper → Connecticut / Habano / Maduro / Natural
  - By Strength → Mild / Medium / Full
- Samplers & Gifts
- New Arrivals
```

---

## Phase 4: SEO Preservation

Losing SEO on migration = losing organic traffic. This is non-negotiable.

### 301 Redirect Map
Every old Shopify URL → new WordPress URL.

**Priority redirects:**
| Old URL pattern | New URL |
|---|---|
| /collections/all | /shop/ |
| /collections/[brand] | /shop/?brand=[brand] or /product-category/brand/[brand]/ |
| /products/[slug] | /shop/[slug]/ |
| /pages/about | /about/ |
| /pages/contact | /contact/ |

**How to implement:**
- Export full product/page URL list from Shopify
- Map to WordPress equivalents
- Implement with **Redirection** plugin (free) or via Nginx/Apache config
- Validate with Screaming Frog post-launch

### Other SEO Checklist
- [ ] Transfer meta titles and descriptions (export from Shopify, import via Yoast/Rank Math)
- [ ] Verify canonical URLs on all product pages
- [ ] Resubmit sitemap to Google Search Console post-launch
- [ ] Monitor 404s in Search Console for 30 days post-launch
- [ ] Verify structured data (Product schema) on product pages

---

## Phase 5: Testing Checklist (Staging)

### Functional
- [ ] Age gate works on site entry and/or checkout
- [ ] Products display correctly with all attributes
- [ ] Filtering (wrapper, strength, origin, format, price) returns correct results
- [ ] Add to cart, quantity update, remove from cart
- [ ] Shipping threshold calculation is correct ($49)
- [ ] Discount logic works correctly ($99 = 10% off)
- [ ] Checkout flow: guest and account
- [ ] Payment processing (use test mode)
- [ ] Order confirmation emails send correctly
- [ ] Account creation and login
- [ ] Mobile checkout (critical — test on real devices)

### Content
- [ ] All product images load correctly
- [ ] No broken links (crawl with Screaming Frog or Broken Link Checker plugin)
- [ ] All redirects return 301 (not 302)
- [ ] Blog/journal posts display correctly

### Performance
- [ ] Homepage loads under 3 seconds (test with PageSpeed Insights)
- [ ] Product grid pages load under 3 seconds
- [ ] Core Web Vitals pass (LCP, CLS, FID)

---

## Phase 6: Launch Checklist

**24 hours before:**
- [ ] Final content review on staging
- [ ] Disable any Shopify discount codes (or replicate in WooCommerce)
- [ ] Export final inventory from Shopify, import to WooCommerce
- [ ] Test all payment methods in WooCommerce production mode (not test)
- [ ] Back up WordPress staging environment

**At launch:**
- [ ] Enable maintenance mode on WordPress while flipping DNS
- [ ] Update DNS: point domain to new WordPress host
- [ ] DNS propagation: allow 1–24 hours (TTL-dependent)
- [ ] Remove maintenance mode
- [ ] Test checkout on live domain with a real transaction
- [ ] Verify age gate is live
- [ ] Monitor error logs for first 2 hours

**Post-launch (first week):**
- [ ] Monitor 404s in Search Console
- [ ] Watch WooCommerce orders for any checkout errors
- [ ] Monitor page speed (WP Rocket cache warms over first few days)
- [ ] Cancel Shopify plan (keep data accessible for 30+ days if possible)

---

## Timeline Estimate

| Phase | Duration | Notes |
|---|---|---|
| Phase 0: Decisions | 1 week | Client-dependent |
| Phase 1: Environment setup | 1 week | Hosting, WP install, plugins, staging |
| Phase 2–3: Data migration + taxonomy | 2–3 weeks | Depends on attribute enrichment scope |
| Phase 4: Design build | 4–6 weeks | Concurrent with data work |
| Phase 5: Testing | 1–2 weeks | Full QA on staging |
| Phase 6: Launch | 1 day | DNS cutover |
| **Total** | **~10–13 weeks** | From kickoff to go-live |

---

## Risks and Mitigations

| Risk | Mitigation |
|---|---|
| Payment processor rejection (high-risk) | Confirm processor compatibility BEFORE any build starts |
| Attribute data missing for 1,344 SKUs | Decide scope at Phase 0; start with in-stock only |
| SEO traffic drop post-launch | Comprehensive 301 redirects + Search Console monitoring |
| Shopify data lost after plan cancellation | Export everything before canceling |
| WooCommerce performance at 1,000+ SKUs | Quality hosting + caching layer (WP Rocket) + image optimization |
| Customer password migration | Force password reset email at launch — this is normal and expected |
