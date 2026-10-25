# Lenilace: redesign demo

A self-contained demo (`index.html` plus `img/`, no build step) of a redesigned
lenilace.com. Open `index.html` in a browser, or run `python3 -m http.server` in this
folder and visit http://localhost:8000.

It includes the real catalogue (5 products, with prices, sizes, sold-out sizes and
descriptions taken from the live site) and photos cropped from screenshots of the
current store. Pages:

| Route | Page |
|---|---|
| `#/` | Home: logo hero, featured sets, "pearl keyhole" story, About, mailing list |
| `#/collections/all` (`/sets`, `/bras`, `/panties`) | Shop, with filter drawer and sort |
| `#/products/<handle>` | Product page: gallery, zoom, size pickers, related products |
| `#/cart` | Full bag page: order note, shipping estimate, pre-order notice |
| `#/contact` | Contact: topics, inline validation, FAQ, confirmation |

## What changed vs. the live site

**Photo grid.** On the live site, the product photos come in different shapes (one tall
portrait next to wide landscapes), so the rows are ragged and there's a big empty gap
under the short cards. Here, every photo sits in the same square frame:
- Full flat-lays are shown **whole** (nothing cropped). The space around them is filled
  with a magnified, blurred patch of the photo's own satin background, and the photo's
  edges are feathered so no seam shows.
- Close-ups fill the frame edge to edge.
- The frames are pre-sized, so the page doesn't jump while images load.
- 2 columns on phones, 3 on desktop. With 5 products, that avoids a lone orphan card on a
  4-column row.

**Card interactions.** On desktop, hovering fades to the close-up photo (or slowly zooms
if there's only one). On phones, you swipe through a card's photos, with dots showing
position. Colour swatches switch the photo in place.

**Product page.** The live page stacks full-size landscape photos, so you scroll a long way
past near-identical images while the tiny thumbnails sit far off to the side. Here:
- **One main image** with arrows, a counter, and thumbnails right next to it. It swipes
  on phones.
- **Hover-to-zoom** follows the cursor on desktop. Click (or tap) opens a **full-screen
  viewer** with tap-to-zoom, drag to pan, swipe or ← → to browse, and Esc to close.
- **Sticky buy column** on desktop. On phones, a **sticky "Choose size / Add to bag"
  bar** appears once the main button scrolls away.
- **Sizes start unselected.** Nothing is pre-picked, so nobody accidentally buys 32A/XS.
  Pressing the button without choosing highlights exactly which option is missing.
  Sold-out sizes are struck through and disabled.
- Pre-order messaging ("Ships by March 15") sits right under the button. Payment-plan
  wording follows the live site's $35 minimum.
- Perk tiles (Hand-stitched in the USA, organic cotton-lined, freshwater pearl), then
  Fit, Care and Shipping sections that expand and collapse.

**Scrolling.**
- Native scrolling with no scroll-jacking; one passive, rAF-throttled listener.
- The header hides when you scroll down and comes back when you scroll up. The shop's
  filter bar stays pinned right under it.
- Page changes jump straight to the top. "Back" to the shop restores where you were.
- Drawers and overlays lock the page without a jump, and scrolling inside them doesn't
  leak to the page behind.
- Respects reduced-motion settings.

**Cart.** Your cart layout is kept (product / quantity / total), plus:
- A free-shipping progress bar and an order summary card (it becomes a sticky side
  panel on desktop).
- A clear pre-order notice.
- The order note and shipping estimate are collapsed until needed, so the checkout
  button stays in view.
- The shipping estimate validates the ZIP.

There's also a slide-out bag drawer with "View bag" and "Checkout".

**Contact.** The live page is a bare form next to an empty half-page. Here:
- The left side answers the common questions (sizing, pre-order timing, returns, care).
- The form has topic chips (choosing "An order" adds an order-number field), floating
  labels, inline errors, a character count, and a confirmation message.

**Home.** It keeps your "L." monogram and spaced LENILACE wordmark over a soft lace
backdrop, with a scroll cue. Below that: featured sets, a detail story, your About copy
(What we do / Who we are), and the mailing list with a thank-you state.

## Before going live

- **Photos:** the demo's photos are low-resolution crops from screenshots. Use the
  original files at 2000px+. For the cleanest grid, shoot the next batch as **square or
  4:5 portrait** on the same satin, then mark them `"cover"` in the `IMG` table.
- **Missing photos:** Set in Pink and Set in Nude only have one photo here, and the pink
  and nude colourways of the Signature Bra/Panty reuse the set photos. Add their real
  photos to `img/`, register them in `IMG`, and list them under each product's `colors`.
- **Placeholder copy:** the Fit, Care, Shipping/returns and contact FAQ text is
  placeholder. Replace it with your actual policies.
- **Shopify:** the layout maps onto a standard Shopify theme (collection grid, product
  media gallery, cart page, contact form). Checkout, search and accounts are stubbed in
  this demo.
