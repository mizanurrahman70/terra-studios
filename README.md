<h1 align="center" style="position: relative;">
  <br>
    <img src="./assets/shoppy-x-ray.svg" alt="logo" width="200">
  <br>
  Terra Studios Theme
</h1>

A handcrafted Shopify theme for Terra Studios — ceramics, dinnerware, and studio storytelling. Built on the Shopify Skeleton Theme foundation with a set of modular, reusable sections, JSON templates, and a fully paginated gallery.

<p align="center">
  <a href="./LICENSE.md"><img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License"></a>
</p>

## Getting started

### Prerequisites

Before starting, ensure you have the latest Shopify CLI installed:

- [Shopify CLI](https://shopify.dev/docs/api/shopify-cli) – helps you download, upload, preview themes, and streamline your workflows

If you use VS Code:

- [Shopify Liquid VS Code Extension](https://shopify.dev/docs/storefronts/themes/tools/shopify-liquid-vscode) – syntax highlighting, linting, inline documentation, and auto-completion for Liquid templates

### Preview

Preview this theme using Shopify CLI:

```bash
shopify theme dev
```

Run Theme Check to lint Liquid and validate schemas:

```bash
shopify theme check
```

## Theme architecture

```bash
.
├── assets          # Static assets (CSS, JS, images, fonts)
├── blocks          # Reusable, nestable theme blocks
├── config          # Global theme settings and settings schema
├── layout          # Top-level page wrappers (theme.liquid, password.liquid)
├── locales         # Translation files
├── sections        # Modular full-width page components
├── snippets        # Reusable Liquid fragments
└── templates       # JSON templates that compose sections into pages
```

To learn more, refer to the [theme architecture documentation](https://shopify.dev/docs/storefronts/themes/architecture).

## Sections

Each `terra-*` section ships with a `{% schema %}` and is available in the theme editor via **Add section**.

| Section | File | Description |
| --- | --- | --- |
| Hero | `sections/terra-hero.liquid` | Headline, copy, buttons, image, and proof stats |
| Trust bar | `sections/terra-trust-bar.liquid` | Icon + heading + text trust points |
| Feature list | `sections/terra-feature-list.liquid` | Grid of feature items with icons |
| Featured products | `sections/terra-featured-products.liquid` | Collection or manual product carousel |
| Collection circles | `sections/terra-collection-circles.liquid` | Circular collection navigation |
| Heritage split | `sections/terra-heritage-split.liquid` | Image + text split with optional quote |
| Gallery | `sections/terra-gallery.liquid` | Masonry image gallery with show-all and pagination |
| Testimonials | `sections/terra-testimonials.liquid` | Customer quotes with ratings |
| FAQ | `sections/terra-faq.liquid` | Grouped accordion questions |
| Newsletter signup | `sections/terra-newsletter-signup.liquid` | Email capture form |
| Image banner | `sections/terra-image-banner.liquid` | Full-width promotional banner |
| Image with text | `sections/terra-image-text.liquid` | Alternating image/text rows |
| Rich text | `sections/terra-rich-text.liquid` | Freeform content block |
| Logo bar | `sections/terra-logo-bar.liquid` | Row of partner/press logos |
| Video | `sections/terra-video.liquid` | Embedded video with poster |
| Story intro | `sections/terra-story-intro.liquid` | Page intro for story/content pages |
| Contact form | `sections/terra-contact-form.liquid` | Contact form block |

## Gallery

`sections/terra-gallery.liquid` renders a masonry image gallery (CSS columns) with an optional **Show all photos** button and page-wise navigation.

### Settings

| Setting | ID | Notes |
| --- | --- | --- |
| Eyebrow | `eyebrow` | Small uppercase label |
| Heading | `heading` | Section heading |
| Columns | `columns` | 2–4 masonry columns |
| Gap | `gap` | Space between photos |
| Show all button label | `show_all_label` | Text for the button |
| Show less button label | `show_less_label` | Text for the collapse button (inline mode) |
| Show all page | `show_all_link` | When set, the button becomes a link to this page |
| Show all photos with pagination | `paginate_all` | Renders every photo paginated — use on the gallery page |
| Photos before button | `photos_to_show` | How many photos show before the button |
| Photos per page | `photos_per_page` | Photos per page in paginated modes |
| Spacing & colors | `padding`, `background`, `text_color`, `muted_color`, `accent_color` | Theme styling |

Each **Image** block supports an image, a caption, and an optional link. When no image is uploaded, a bundled fallback image (`gallery-1.webp` … `gallery-4.jpg`) is shown so the layout can be previewed.

### Modes

The section automatically selects a behavior based on the settings:

1. **Inline** *(default)* — shows `photos_to_show` photos, then expands in place with page-wise navigation.
2. **Link** — set **Show all page** to a URL and the button navigates to that page. Use this on the home page.
3. **Full** — enable **Show all photos with pagination** to render all photos page-wise immediately. Use this on the dedicated gallery page template.

### Setting up the gallery page

Theme code cannot create Shopify pages, so one manual step is required:

1. In Shopify admin, go to **Pages → Add page**.
2. Set the title to `Gallery` and the handle to `gallery`.
3. Under **Theme template**, choose `gallery` (from `templates/page.gallery.json`).
4. On the home page gallery section, set **Show all page** to `/pages/gallery`.

If you use a different page handle, update the **Show all page** setting to match (`/pages/<handle>`).

`templates/page.gallery.json` ships with the gallery section already configured in **Full** mode (`paginate_all: true`, `photos_per_page: 3`) plus a newsletter section.

## Templates

[JSON templates](https://shopify.dev/docs/storefronts/themes/architecture/templates/json-templates) compose sections into pages. This theme includes:

- `index.json` — home page
- `product.json`, `collection.json`, `cart.json`, `search.json`, `blog.json`, `article.json`, `list-collections.json`, `404.json`, `password.json`
- Story/content pages: `page.our-story.json`, `page.craftsmanship.json`, `page.sourcing.json`, `page.collaborations.json`, `page.apprentice.json`, `page.faqs.json`, `page.journal.json`, `page.care-guide.json`, `page.contact.our-story.json`, `page.contact.journal.json`
- `page.gallery.json` — full paginated gallery page
- `page.json` — default page template

## CSS & JavaScript

Styling and behavior live beside each section:

- Section CSS is loaded with `{{ 'name.css' | asset_url | stylesheet_tag }}` and stored in `assets/`.
- Section JavaScript uses the `{% javascript %}` tag so Shopify includes it once per page.
- Global/baseline styles live in `assets/critical.css`, which separates essential CSS loaded on every page.

When adding settings, prefer CSS variables for single-property settings and CSS classes for multi-property settings. See the [section schema documentation](https://shopify.dev/docs/storefronts/themes/architecture/sections/section-schema) for details.

## Contributing

Please keep contributions lean, lightweight, and focused. Visit [CONTRIBUTING.md](./CONTRIBUTING.md) for the full process and guidelines.

## License

This theme is built on the Shopify Skeleton Theme. See [LICENSE.md](./LICENSE.md) for the full license terms governing use of the software.
