# Florida Tea and Honey — theme dev context

Shopify **Horizon** theme (v3.5.1) for the store **Florida Tea and Honey**, customized
with a **"KICK"-inspired** redesign. This file exists so a new Claude session gets in
context fast. Read it first.

## Store / theme / repo

- **Storefront:** https://floridateaandhoney.com (the `myshopify` domain
  `wgjk0q-k3.myshopify.com` redirects here).
- **Live theme:** `Horizon - dev` **#149313814614** — yes, the live theme is *named*
  "Horizon - dev" (it was the staging theme that got published). It IS the live theme.
- **Rollback themes (unpublished):** old `Horizon` #148741390422, `Backup-Jun-19` #149313159254.
- **Repo:** https://github.com/carlitomm/florida-tea-and-honey (personal account `carlitomm`).
  Local git identity only; never touch global git/npm config (see `../CLAUDE.md`).
- Shopify CLI is brew-installed (`shopify`, v3.93.x). Auth is browser device-code as
  `mindmiguelez@gmail.com`; the **dev-server token expires** periodically — if the preview
  shows "access token … expired", just restart `shopify theme dev`.

## ⚠️ Non-negotiable workflow rules (ALWAYS follow, every session)

These are absolute. Do not skip them, do not assume they were done. New people work in this
repo through Claude, so the safety comes from these rules being enforced every single time.
A plain-language version for non-technical teammates lives in **`ONBOARDING.md`** — keep both
in sync when the process changes.

1. **PULL BEFORE YOU TOUCH ANYTHING — never overwrite Carlos's admin work.**
   The store owner edits content in the Shopify admin (Theme Editor). Those edits land in
   `config/settings_data.json` and `templates/*.json` and exist ONLY on the live theme until
   pulled. At the START of every working session:
   - Confirm git is clean (`git status`). If not, commit or stash first.
   - `shopify theme pull --theme 149313814614 --store wgjk0q-k3.myshopify.com --nodelete`
   - Review what came down (`git diff`) and **commit it** with a message like
     "Pull admin edits: …" BEFORE writing any code. Skipping this risks silently destroying
     content the owner created in the admin.

2. **NEVER publish or push to the live theme without an explicit "go live" from Carlos.**
   #149313814614 is BOTH the dev and the live theme, so any push to it writes to the live
   storefront. Each "go live" is a ONE-TIME OK for that one change — it does not carry over to
   the next change. When you do go live:
   - Push only the files you changed: `--only <file>` (repeat `--only` per file). Never push
     the whole theme — it would clobber `templates/*.json` admin edits.
   - `--allow-live` is required (the push targets the live theme).
   - Example:
     `shopify theme push --theme 149313814614 --store wgjk0q-k3.myshopify.com --only snippets/custom-foo.liquid --allow-live`

3. **ALWAYS verify visually with Playwright before and after — don't trust code alone.**
   Iterate on the local dev server: `shopify theme dev --store wgjk0q-k3.myshopify.com`
   (http://127.0.0.1:9292, hot-reload, throwaway dev theme — does NOT touch live). Take
   Playwright screenshots at **1440px (desktop)** and **390px (mobile)** and actually look at
   them before saying something works. After going live, screenshot the real storefront URL
   (floridateaandhoney.com) to confirm.

4. **ALWAYS document in English.** All code, comments, commit messages, and `.md` files are
   written in English, regardless of the chat language. (Conversation with Carlos is in
   Spanish; the artifacts are English.)

5. **ALWAYS keep the GitHub repo up to date.** Commit every change with a clear English
   message. After a change is approved/live, push to GitHub (`git push origin main`) so the
   repo always reflects what is live. Git/credentials are LOCAL-scoped only (see `../CLAUDE.md`)
   — identity is `carlitomm`, never touch global git config.

6. **Before going live, safety-diff** when in doubt: pull the live theme into a temp `--path`
   dir and `diff -rq` against local to confirm no admin-only edits would be lost.

7. **All customization goes in `custom-*.liquid` files** with CSS isolated inside them; core
   theme files get only minimal `{% render 'custom-…' %}` hooks. Colors come from the theme
   color schemes, never hard-coded (see Conventions below).

## Conventions

- All customizations live in **`custom-*.liquid`** files (sections/snippets), with CSS
  isolated inside them. Core theme files get only minimal `{% render 'custom-…' %}` hooks.
  Each custom file documents how to revert it in its top comment.
- **Colors come from the theme color schemes**, never hard-coded brand colors. Carlos sets
  colors/menu in the admin, not in code. Key schemes (in `settings_data.json` →
  `current.color_schemes`):
  - **scheme-1** `#f6efe2` = cream (Teas section, featured bento bg)
  - **scheme-2** `#7c8a5a` = green (header + page background)
  - **scheme-4** / `--color-primary` ≈ honey-gold `#d59154`/`rgb(200,136,28)` = accent
- Mobile carousels use a CSS scroll-snap pattern (cards 82% width = peek) + pagination
  dots driven by a small IntersectionObserver script, scoped per `#shopify-section-{id}`.

## Custom files (what each does)

| File | Purpose |
|---|---|
| `snippets/custom-header-pill.liquid` | KICK header: nav in a rounded pill capsule, circular account/cart icons (gapped), search centered in the pill; logo capped at 56px so the header stays ~86px tall |
| `snippets/custom-search.liquid` + `snippets/search-modal.liquid` | Pill search input, floating themed Search button, vertical product results |
| `snippets/custom-announcement-marquee.liquid` + `sections/header-announcements.liquid` | Announcement bar as a full-width scrolling marquee (gold fill, bold uppercase, leaf separator). Toggle "Scroll as marquee" (on). **Reads messages from a `marquee_messages` textarea setting**, NOT the announcement block (this Horizon section renders blocks via `content_for 'blocks'`, so `section.blocks` is empty in Liquid) |
| `sections/custom-collection-cards.liquid` | KICK landscape collection cards under the header; mobile = swipeable carousel + dots |
| `sections/custom-trust-bar.liquid` | "Trusted by … Customers" + auto-scrolling testimonial marquee, under the hero (scheme-2 green) |
| `sections/custom-featured-bento.liquid` | Featured-products bento (1 large + 2 small + 1 wide via grid-areas `"a b c"/"a d d"`), cream bg, between trust bar and Teas. Each card = merchant-picked **product** (product picker → image+link) + free-text title/subtitle/button. **Full-bleed image (object-fit cover) fills each card**, text overlaid on a gradient. Mobile = carousel + dots |
| `snippets/custom-hero.liquid` | Contained, rounded hero |
| `snippets/custom-page-background.liquid` | Whole-page background = header green (scheme-2), read from settings; rendered in `layout/theme.liquid` |
| `snippets/custom-breadcrumb.liquid` | Product-page breadcrumb (Home / collection / product) |
| `snippets/custom-product-styles.liquid` | Product page: 40% media / 60% details (overrides equal-columns grid); price box styling + larger/regular-weight price; selected variant swatch uses `--color-primary`; top-aligns the details box flush with the image top |

## Homepage section order (`templates/index.json`)

`collection_cards_kick` → `hero_jVaWmY` → `trust_bar_kick` → `featured_bento_kick` →
`product_list_fa6P9H` (Teas) → …

## Product page (`templates/product.json`)

Section `product-information` with `media-gallery` + `product-details` blocks. Gallery is
**carousel with thumbnails on the LEFT** (`thumbnail_position: left`), `media_radius: 16`.
The title, price, variant picker and buy-buttons (quantity + add-to-cart) are all moved
into the one **"Header" group block** (`group_icgrde`) so they render inside a single box;
the description stays outside. The box CSS/40-60 split live in `custom-product-styles.liquid`.

## Current state (2026-06-20)

Everything above is **LIVE** on floridateaandhoney.com. Outstanding: the **Cacao** and
**Teas** cards in the featured bento have no product assigned yet (showing placeholders) —
Carlos to assign products in the Theme Editor → *Featured bento*.
