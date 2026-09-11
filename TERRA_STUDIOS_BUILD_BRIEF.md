# Terra Studios — Shopify theme build brief

This document is the implementation source of truth for a Shopify Online Store 2.0 theme based on the supplied Terra Studios homepage reference. It is a build guide, not an instruction embedded in the reference image.

## 1. Brand and design direction

**Store:** Terra Studios  
**Tagline:** Tactile stoneware, shaped by hand  
**Category:** Handmade ceramic tableware, drinkware, and home decor  
**Audience:** Shoppers seeking durable, tactile, small-batch ceramic pieces for everyday ritual and gifting.  
**Brand voice:** Warm, artisanal, grounded, and sustainability-forward.

The visual character is quiet and editorial: clean white/cream surfaces, direct product photography, large friendly display type, compact utility text, and one restrained terracotta accent. The memorable motif is the contrast of perfectly circular collection thumbnails with the irregular, hand-made forms they frame.

### Design tokens

| Token | Value | Use |
| --- | --- | --- |
| `--terra-rust` | `#C4592E` | Primary buttons, small eyebrow labels, sale accents, active controls |
| `--terra-oatmeal` | `#F5EFE6` | Warm section backgrounds and input fill |
| `--terra-charcoal` | `#2B2925` | Primary headings and body text |
| `--terra-paper` | `#FFFFFF` | Main canvas and cards |
| `--terra-muted` | `#77716B` | Supporting copy |
| `--terra-line` | `#E9E4DD` | Fine borders and dividers |
| `--terra-dark` | `#332E29` | Sold-out badge and footer text |

### Type, spacing, and interaction

- Headings: rounded, high-weight sans serif (use a Shopify font-picker heading font; `Archivo`/`Nunito Sans`-like personality is appropriate). Use 700–800 weight and tight line height.
- Body: clean sans serif using the existing primary font setting or a separate Shopify font picker. Use 14–16px body copy with relaxed 1.45–1.6 line height.
- Utility labels: 10–12px uppercase or semibold, modest tracking.
- Desktop content width: 1360px maximum with 40px side gutters; mobile gutters: 20px.
- Section rhythm: 72–112px desktop vertical padding; 44–64px on mobile.
- Corners: square for buttons and inputs. Product images may have a subtle 2px radius only if needed.
- Buttons: solid rust background/white text for primary; white/charcoal border for secondary; no pill-shaped buttons. Provide obvious `:focus-visible`, hover, disabled, and reduced-motion treatment.
- Do not use gradients, glass effects, excessive shadows, or animation that competes with the product photography.

## 2. Global storefront structure

### Header group

1. **Announcement bar** — rust background; centered text: “Free shipping on domestic orders over $150 — handcrafted in small batches”.
2. **Header** — wordmark at left (“TERRA” charcoal, “STUDIOS” rust); primary navigation in the center; search, account, and cart controls on the right.
3. **Navigation**

```text
New Arrivals                  /collections/new-arrivals
Tableware
  Dinnerware                  /collections/dinnerware
  Serving Bowls               /collections/serving-bowls
  Drinkware                   /collections/drinkware
Vases & Decor
  Vases                       /collections/vases
  Accessories                 /collections/accessories
Our Story                     /pages/our-story
Journal                       /blogs/journal
```

Use accessible desktop dropdowns and a keyboard-friendly mobile drawer. The cart icon must expose item count and accessible text.

### Footer group

- Brand introduction and social links.
- Shop links: All Ceramics, Dinner Sets, Mugs & Drinkware, Serving Vases, Sale Highlights.
- Studio links: Our Craftsmanship, Sourcing Practices, Apprentice Program, Journal, Collaborations.
- Customer care: Shipping & Delivery, Returns & Exchanges, Care & Lifetime Guide, FAQs, Contact Support.
- Bottom line: copyright, privacy policy, terms, payment icons, and cart link.

## 3. Homepage assembly order

Replace the current `hello-world` section in `templates/index.json` with the sections below, in this exact order. Every section needs a complete `{% schema %}` block so merchants can replace copy, images, links, color scheme, spacing, and section-specific content without editing Liquid.

| Order | Section file | Purpose and reference behavior |
| --- | --- | --- |
| 1 | `sections/terra-hero.liquid` | Two-column hero: text/CTAs/trust mini-panel at left and full-height ceramic table image at right. Stack image first or text first intentionally on mobile; preserve readable copy. |
| 2 | `sections/terra-collection-circles.liquid` | “Browse by collection” with five circular linked image tiles: Dinnerware, Drinkware, Serving Bowls, Vases, Accessories. |
| 3 | `sections/terra-trust-bar.liquid` | Four icon/value propositions: Sustainably Sourced, Kiln-Fired Durability, Direct Artisan Trade, Conscious Packaging. Use editable blocks. |
| 4 | `sections/terra-featured-products.liquid` | “Best sellers / Featured Ceramics”, collection picker, 4-up desktop responsive product grid, View all products link. |
| 5 | `sections/terra-heritage-split.liquid` | Image/text 50–50 story section: “Designed for durability, styled for life.” with quote and “Meet our apprentices” link. |
| 6 | `sections/terra-testimonials.liquid` | “Loved by Cook & Host”, review cards from editable blocks; include rating and verified-buyer label. |
| 7 | `sections/terra-newsletter.liquid` | Oatmeal full-width signup: “Be the first to hear about Batch 05”, Shopify customer form, consent/error/success states. |

Use native Shopify sections and blocks rather than hard-coded data. The homepage should still look complete with placeholder images and empty optional blocks.

## 4. Product-card contract

Create `snippets/card-product-terra.liquid` and render it from featured products and collection grids. It receives a `product` and optional `show_quick_add` boolean.

- Product image uses `image_url` and `image_tag` with responsive widths, meaningful alt text, lazy loading below the fold, and a stable aspect ratio.
- Position a **SAVE** badge when `compare_at_price > price`; percentage copy may be calculated, or the badge may use a product metafield if exact editorial text is needed.
- Position **SOLD OUT** when `product.available == false`.
- Use a `NEW` product tag or metafield for the new-arrivals badge.
- Show title, sale/original price when applicable, and a quick-add button only for single-variant products. Multi-variant products link to the product page.
- Never determine availability from a custom badge alone; use Shopify inventory/availability state.

## 5. Product and collection templates

### Product page

Use `sections/product.liquid` or a Terra-specific product section with: gallery, title, price/sale price, selected variant state, option controls, quantity, add-to-cart, stock messaging, description, material, care note, shipping note, and related products. Preserve Shopify form semantics and dynamic checkout if enabled.

### Collection page

Use `sections/collection.liquid` with collection title/description, product count, filters/sort where supported, responsive grid (four columns desktop, two mobile), and the Terra product-card snippet. The “Best Sellers” and “New Arrivals” sections are ordinary Shopify collections, not hard-coded grids.

## 6. Content model

### Collections

| Title | Handle | Description |
| --- | --- | --- |
| Dinnerware | `dinnerware` | Plates, bowls & dinner sets hand-pressed in stoneware |
| Drinkware | `drinkware` | Mugs, cups & tumblers fired for daily use |
| Serving Bowls | `serving-bowls` | Statement bowls for the table and kitchen |
| Vases | `vases` | Sculptural vessels for florals and display |
| Accessories | `accessories` | Trays, coasters & small studio goods |
| Best Sellers | `best-sellers` | Our most-loved pieces; homepage featured collection |
| New Arrivals | `new-arrivals` | Latest from Batch No. 04 |
| Sale | `sale` | Discounted stock and seconds |

### Sample products

| Product | Handle | Collections | Price | SKU | Inventory | Display state |
| --- | --- | --- | ---: | --- | ---: | --- |
| Oatmeal Carafe & Cup Set | `oatmeal-carafe-cup-set` | drinkware, best-sellers, sale | $85.00 ($110.00 compare-at) | TS-CCS-001 | 24 | SAVE |
| Stoneware Salad Bowl | `stoneware-salad-bowl` | serving-bowls, best-sellers | $64.00 | TS-BWL-014 | 18 | — |
| Hand-Thrown Espresso Mug | `hand-thrown-espresso-mug` | drinkware, best-sellers | $28.00 | TS-MUG-032 | 56 | — |
| Sculptural Ochre Vase | `sculptural-ochre-vase` | vases, best-sellers | $120.00 | TS-VAS-007 | 0 | SOLD OUT |
| Terracotta Dinner Plate Set (4pc) | `terracotta-dinner-plate-set` | dinnerware, new-arrivals | $96.00 | TS-PLT-041 | 40 | NEW |
| Ribbed Ceramic Tray | `ribbed-ceramic-tray` | accessories | $42.00 | TS-ACC-019 | 33 | — |

Product descriptions, variant options, material, and weights are supplied in the original project brief and should be imported to Shopify as product data. Store editorial badge overrides in a product metafield (for example `custom.card_badge`) only when Shopify state cannot express the intended badge.

## 7. File and CSS plan

Keep shared styling centralized. Create one theme stylesheet at `assets/terra-studios.css`; load it from `layout/theme.liquid` after `critical.css`. Do not place a full duplicate CSS system inside every section. Section-specific CSS belongs in a short `{% style %}` block only when it cannot be shared.

```text
assets/
  terra-studios.css             # tokens, layout primitives, header/footer, cards, responsive rules
sections/
  terra-hero.liquid
  terra-collection-circles.liquid
  terra-trust-bar.liquid
  terra-featured-products.liquid
  terra-heritage-split.liquid
  terra-testimonials.liquid
  terra-newsletter.liquid
snippets/
  card-product-terra.liquid
  icon-terra-*.liquid           # optional inline SVG icons
templates/
  index.json                    # section order and merchant defaults
```

Extend `config/settings_schema.json` with a **Terra Studios** settings group for heading font, body font, rust accent, oatmeal background, charcoal text, and social links. Expose those values as CSS custom properties from `snippets/css-variables.liquid`; keep the given values as defaults.

## 8. Implementation requirements

- Use Shopify Liquid best practices: `render`, `image_url`, `image_tag`, `routes`, translation strings where practical, and valid schema JSON.
- Keep all interactive JavaScript vanilla and progressive-enhancement friendly. Avoid jQuery and external page builders.
- Use semantic landmarks, labelled form controls, visible keyboard focus, image alt fields, adequate contrast, and `prefers-reduced-motion` support.
- Optimize images with Shopify CDN widths and `srcset`; do not use base64 images or fixed remote image URLs.
- Verify desktop, tablet, and mobile: no horizontal scroll, header/nav usable by keyboard/touch, cards remain legible at 2-up mobile, buttons meet 44px touch target where possible.
- Test product states: regular price, sale, sold out, single variant quick add, multi-variant detail link, and no product image.

## 9. Suggested delivery sequence

1. Add global settings, CSS tokens, announcement/header/footer refinements.
2. Create the product card and test its six states.
3. Build hero, collections, trust bar, and featured products; update `index.json`.
4. Build heritage, testimonials, newsletter, and footer content.
5. Complete PDP and collection-page layouts.
6. Run responsive/accessibility QA and Shopify theme check before handoff.

## 10. Decisions still owned by the merchant

- Final photography and rights-cleared image assets.
- Exact font choices available in Shopify’s font picker.
- Shipping, return, legal, social, and contact URLs.
- Whether “Batch No. 04/05” is seasonal editorial copy or a live collection/marketing campaign.
- Product tags/metafield definitions and final Shopify CSV import mapping.
