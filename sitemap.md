# Releaf Cigars — Official Sitemap

**Source:** Client-provided sitemap (received July 2026)  
**Platform:** WordPress + WooCommerce

---

## Primary Navigation (8 items)

```
Home | Shop | Brands | Samplers | Accessories | Blog | Visit Us | About
```

---

## Pages

### Home
- `/`

---

### Shop
- `/shop` — All Products
- `/shop/new-arrivals`
- `/shop/best-sellers`
- `/shop/releaf-exclusives`
- `/shop/limited-editions`
- `/shop/flash-sales`
- `/shop/clearance`

---

### Brands
- `/brands` — All Brands A–Z
  - `/brands/[brand-name]` — Individual brand pages (56+ brands)

---

### Samplers
- `/samplers` — All Samplers
- `/samplers/brand-samplers`
- `/samplers/wrapper-samplers`
- `/samplers/country-samplers`
- `/samplers/pairing-samplers`
- `/samplers/beginner-samplers`

---

### Accessories
- `/accessories` — All Accessories
- `/accessories/cutters`
- `/accessories/lighters`
- `/accessories/humidors`
- `/accessories/ashtrays`
- `/accessories/cases`
- `/accessories/humidification`

---

### Blog
- `/blog` — All Posts
- `/blog/[post-slug]`

---

### Visit Us
- `/visit` — Hours, Location, Map
- `/visit/lounge-info` — House Rules, Amenities
- `/visit/events`

---

### About
- `/about`
- `/about/our-story`

---

## Account & Support
- `/account` — Login / Dashboard
- `/account/register`
- `/account/orders`
- `/wishlist`
- `/cart`
- `/checkout`
- `/faq`
- `/contact`
- `/gift-cards`

---

## Legal
- `/shipping-policy`
- `/return-policy`
- `/privacy-policy`
- `/terms-of-service`
- `/age-verification`

---

## WooCommerce System Pages
- `/shop` — Main store archive
- `/cart`
- `/checkout`
- `/my-account`
- `/my-account/orders`
- `/my-account/downloads`
- `/my-account/addresses`
- `/my-account/account-details`
- `/my-account/lost-password`

---

## WooCommerce Taxonomy Plan

| Attribute | Values | Use |
|---|---|---|
| Wrapper | Connecticut, Habano, Maduro, Natural, Oscuro | Filter + browse |
| Strength | Mild, Medium, Full | Filter + browse |
| Origin | Dominican, Honduran, Nicaraguan, Ecuadorian, Cuban, etc. | Filter |
| Format | Single, 5-Pack, Bundle, Gift Set | Filter |
| Brand | 56+ values (imported from Shopify) | Brand pages |
| Vitola | Robusto, Toro, Churchill, Gordo, Belicoso, Lonsdale, etc. | Filter |

---

## Notes

- **Shop is collection-based** (Best Sellers, Exclusives, Flash Sales) — not attribute-based in nav. Wrapper/strength/origin filtering lives on the shop page itself as sidebar/top-bar filters.
- **Brands** is a first-class nav item — individual brand pages under `/brands/[brand-name]` give each of the 56+ brands a dedicated landing page (good for SEO).
- **Samplers** are their own top-level section with 5 curated types — not nested under Shop.
- **Accessories** is a new category not in the original proposal — 6 subcategories (cutters, lighters, humidors, ashtrays, cases, humidification).
- **Gift Cards** live under Account & Support (`/gift-cards`), not under Samplers.
- **Visit Us** replaces "The Lounge" — includes lounge-info and events sub-pages.
- **Blog** replaces "Journal."
