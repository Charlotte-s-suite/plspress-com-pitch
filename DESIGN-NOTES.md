# DESIGN NOTES — plspress.com

_Site head's record for the quality gate. Standard: `merritt-studio/kit/DESIGN-STANDARD.md`._

## The one-line test

> **The site IS a holo-foil die-cut sticker on the press bed.**

## Law 6 — where the design language came from

**The brief's stated source was unusable.** `plspress.com` is registered (Cloudflare NS
`cass`/`clark`, valid SOA) but publishes **no A or AAAA record** — nothing is served, and there
is no current site to extract from. `library/` is empty and
`merritt-studio/specimens/plspress-com/` contains no extraction sheet.

Schyler redirected the extraction to **https://bridge.pulsechain.com/** mid-build. That is a
stronger law-6 object than a storefront would have been: it is the chain's own official surface,
and the client transacts exclusively in that chain's tokens. The palette below is read out of the
bridge's shipped stylesheet and logo, not eyeballed from a screenshot.

| Role token | Value | Extracted from |
|---|---|---|
| `--field` | `#000000` | `body{background-color:rgb(0 0 0)}` |
| `--field-panel` | `#2D2D2D` | `:root{--bg:#2d2d2d}` |
| `--field-deep` | `#08080A` | `bg.jpg` sampled — black with a faint violet/blue bloom (`#0D0219`, `#070E24`) |
| `--affirm` | `#4CAF50` | `:root{--green:#4caf50}` — the checkmark banner |
| `--paper` / `--paper-ink` | `#FFFFFF` / `#111111` | `.bigLink` (their primary button) |
| `--ink` / dim / faint | `#FFF` / 72% / 56% | `.textLink` state ladder |
| **`--foil`** | `#00EAFF 0% → #0080FF 25.25% → #8000FF 49.74% → #E619E6 74.99% → #FF0000 99.91%`, ~160° | `linearGradient-1` in `logo.svg`, stops and offsets verbatim |

The five-stop diagonal spectrum **is** the brand device, and a five-stop spectrum **is** a
holographic foil. A holo foil is a sticker. That is the whole design.

## The object's grammar → site components (Part II step 3)

1. **Foil edge** → 2px spectrum ring on every sticker, the hero rule, the primary button, the crest.
2. **Matte `#2D2D2D` panel on pure black** → the §3.1 presentation-window role, re-skinned from
   paper to sticker backing. 1px white ring + long shadow retained.
3. **Green affirm chip** → in-stock badges, footer hallmarks, the live-feed dot. Their own device.
4. **Kiss-cut die line** → dashed contour inset on every sticker face; peel-lift on
   hover/focus/active (`translateY(-5px) rotate(-1.2deg)`).
5. **Press-bed ornament** → §3.4 technique with a press vocabulary instead of filigree: registration
   targets, crop marks, plotter cut-paths, halftone arcs. One motif (`#press-motif`), deployed
   5× at different crops/mirrors/opacities (.16 → .10 → .08).
6. **Voice inversion** — the bridge uses zero serif and the client asked for a large bold header,
   so **heavy system sans = things of value, mono = apparatus**. This deliberately inverts the
   kit's serif-is-value rule of thumb, per §III's adaptation clause. System stacks only (law 3).

## Client asks, delivered

- **Magic wand trail behind the products, toggleable** — canvas behind the shelf, spectrum trail on
  pointer/touch. Toggle persists to `localStorage`; **defaults off under `prefers-reduced-motion`**;
  initialises on `requestIdleCallback`; clears on `visibilitychange`. The toggle button ships
  `hidden` and is revealed by JS, so there is no dead control when JS is off. This is the page's
  one hero moment (§5.0.5).
- **Interactive map of people using the stickers** — a dot-matrix world (the map is *printed*, same
  halftone vocabulary as the ornament). Land rasterised from Natural Earth 110m polygons into 1,672
  dots emitted as **one** `<path>` of round-capped zero-length segments (15.5kB). Static markup, so
  it survives JS off; JS only adds list ⇄ pin sync.
- **Simple, easy to use** — one screen per idea, six products, no menus, no cart ceremony.
- **PulseChain core tokens only** — PLS, PLSX, HEX, INC, chain ID 369, priced live.

## Law 4 — the live element

CoinGecko keyless (`access-control-allow-origin: *`), ids `pulsechain`, `pulsex`, `hex`,
**`pulsex-incentive-token`** (note: `incentive-token` returns empty — wrong id for INC). Drives the
hero rate window, the counter's accepted-token list, **and re-prices every sticker in PLS at the
live rate**. Seeded values in markup; every write guarded; both terminal states honest.

## Gate results

| Check | Result |
|---|---|
| Three-viewport width law | 390/834/1280 — `scrollWidth` == viewport exactly, 0 JS errors |
| Single file, zero dependencies | 59kB, one file, no CDN/webfont/build step |
| CWV (390, 4× CPU throttle, worst of 3) | **LCP 464ms**, **CLS 0.0040**, flat through a full scroll cycle |
| JS disabled | 6 products, 10 sightings, 10 pins, 1,672 map dots, seeded prices, no dead controls |
| `prefers-reduced-motion` | 12 reveals all land on end-states, wand defaults off, canvas opacity 0 |
| Touch targets @390 | every interactive element ≥44px tall |
| Slop gate (`impeccable@3.3.1`) | 9 findings, all three categories documented in `.impeccable/config.json`; every genuine finding fixed |

Ornament bleeds off-edge at all three widths and is contained by each section's own
`overflow:hidden` — that is why the widths match exactly despite elements extending past the
viewport.

## Open — needs the client

1. **Product photographs.** All six sticker faces are placeholder line-art drawn for this build,
   captioned as such on the page.
2. **Real names, descriptions, prices, sizes.** Current values are plausible placeholders.
3. **Sightings are seeded** (10 cities), labelled on the page. Real submissions need a backend.
4. **No checkout exists.** Payment rails are shown as UI only — no wallet connection, no address
   that could receive funds. Stated in the provenance line.
