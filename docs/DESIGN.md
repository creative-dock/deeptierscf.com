# Design system

Everything visual lives in one file: [`assets/css/site.css`](../assets/css/site.css). There is no
framework, no preprocessor, and no external network request — fonts fall back to the system UI stack, and
all icons are inline SVG. Read this before adding a page so new work stays inside the system.

## Direction

**Dark-first ink base + teal primary + warm copper accent.**

The rationale, from the colour research done before any markup was written:

- **Blue alone is category shorthand.** Over 70% of B2B SaaS and fintech brands use blue as primary, so
  navy reads generic when a buyer sees three vendors side by side. It signals "financial software" without
  signalling *us*.
- **Teal keeps the trust, adds ownability.** It stays in the blue family — which is where the trust
  association actually lives — while sitting off the crowded centre of the category.
- **The warm accent is the differentiator.** Pairing a blue-family hue with copper/terracotta is the 2026
  move in financial services, and it measures better on perceived trustworthiness than blue-on-blue
  schemes. It's also what stops the palette reading as generic dark-mode SaaS.
- **Dark + metallic is the premium-finance signal.** Stripe and Mercury both use it deliberately. For a
  venture selling to OEM treasury and procurement, looking institutional matters more than looking bright.
- **60 / 30 / 10.** Ink neutrals dominate, teal carries structure and CTAs, copper is accent only. When
  copper starts appearing in more than roughly a tenth of a page, something has gone wrong.

## The accent rule (important)

The two accents are **semantic, not decorative**. Keep this when extending the site:

| Colour | Means |
| --- | --- |
| **Teal** | The chain, verification, confirmed states, and the parties who contribute data — anchor and tier 1 |
| **Copper** | Tier 2+, the financeable event, and strain / warning / watch states |

This is why [`tier-2.html`](../tier-2.html) uses copper CTAs (`.btn--copper`) while every other page uses
teal, and why the deepest bar in the logo mark is copper. A reader who never consciously notices the rule
still absorbs "copper = the deep tier, and the deep tier is where the money goes."

## Tokens

All defined on `:root`. Never hard-code a hex value in markup — add a token or use an existing one.

### Ink neutrals (≈60%)

| Token | Value | Use |
| --- | --- | --- |
| `--ink-950` | `#05090e` | Footer, deepest bands |
| `--ink-900` | `#070c12` | Page background |
| `--ink-850` | `#0a111a` | Alternating bands, table backgrounds |
| `--ink-800` | `#0c141d` | CTA blocks, glass header base |
| `--ink-700` / `--ink-600` | `#111c27` / `#16232f` | Panel gradients, mark background |

### Teal primary (≈30%)

| Token | Value | Use |
| --- | --- | --- |
| `--teal-300` | `#6ee7d5` | Eyebrows, links, inline emphasis |
| `--teal-400` | `#35d6c0` | CTA gradient top, mark bars |
| `--teal-500` | `#14b8a6` | Borders, meters, CTA gradient base |
| `--teal-600` / `--teal-700` | `#0d9488` / `#0b6f68` | Gradient ends, flow connector |

### Copper accent (≈10%)

| Token | Value | Use |
| --- | --- | --- |
| `--copper-300` | `#f0b27a` | Accent text, strain labels |
| `--copper-400` | `#e08a3c` | Accent CTA, tier 2 mark bar |
| `--copper-500` | `#c2703a` | Gradient end |

### Text, lines, layout

| Token | Value | Use |
| --- | --- | --- |
| `--text` | `#e8eef4` | Body |
| `--text-mid` | `#b3c3d1` | Paragraphs inside cards, list items |
| `--text-dim` | `#8798a8` | Secondary labels |
| `--text-faint` | `#64758a` | Metadata, disclaimers |
| `--line` / `--line-strong` | white @ 9% / 16% | Hairlines, card and panel borders |
| `--wrap` | `1180px` | Content max width (`.wrap--narrow` = 860px) |
| `--radius` / `--radius-lg` | `14px` / `20px` | Cards / panels and CTA blocks |
| `--ease` | `cubic-bezier(.22,.61,.36,1)` | Every transition |

### Type

System UI stack, Inter first if it is ever self-hosted. Fluid `clamp()` scale: `.h-display`, `.h-1`,
`.h-2`, `.h-3`, `.lead`, `.small`, `.tiny`.

Monospace (`--mono`) is reserved for eyebrow labels, document IDs, chips, and table headers. This is
deliberate — it reads as *trade document*, which is exactly the subject matter. Don't use it for prose.

## Components

| Class | What it is |
| --- | --- |
| `.band`, `.band--tight`, `.band--alt`, `.band--deep` | Section rhythm and background alternation |
| `.gridlines` | Masked hairline grid texture; add to a `section` alongside a band class |
| `.wrap`, `.wrap--narrow` | Content container |
| `.eyebrow`, `.eyebrow--copper` | Uppercase section label with rule |
| `.grad-text` | White→teal→copper gradient for the second clause of a headline |
| `.card` + `.card--problem` / `.card--solution` | Content card; copper or teal left edge |
| `.benefit`, `.benefit--copper` | The three role cards on the landing page |
| `.chain` + `.chain__node` | Three-node anchor → tier 1 → tier 2 diagram |
| `.tierstack` | Hero cascade with PO/invoice connectors |
| `.flow` + `.flow__step` | Auto-numbered step timeline (CSS counters — no manual numbers) |
| `.panel` + `.signal` + `.meter` + `.tagstate` | Dashboard mockups (anchor signals, tier 2 application) |
| `.ticks`, `.ticks--copper`, `.crosses` | Benefit and pain-point lists |
| `.docrow` + `.doc` | Document chips inside flow steps |
| `.chip`, `.chip--teal`, `.chip--copper` | Small role/state labels |
| `.tablewrap` + `table.cmp` | Comparison table; scrolls horizontally inside its own container |
| `details.qa` | FAQ accordion (native `<details>`, no JS) |
| `.cta` | Closing call-to-action block |
| `.btn--primary` / `--ghost` / `--copper` | Buttons |
| `.reveal` + `data-d="1|2|3"` | Scroll-in animation with stagger delay |

## Accessibility & responsiveness

- `prefers-reduced-motion: reduce` disables all transitions and forces `.reveal` visible. Any new
  animation must be covered by that block.
- `:focus-visible` has a teal outline with offset — don't remove it.
- Breakpoints: **1000px** (hero and 3-up grids collapse, chain stacks), **860px** (mobile nav takes over),
  **620px** (everything single column, flow timeline narrows).
- No element may exceed viewport width. Wide content — the comparison tables — scrolls inside
  `.tablewrap`, never the page body. Verified at 1280px and 375px.
- Decorative SVG and diagram furniture carry `aria-hidden="true"`; the hero diagram carries a descriptive
  `role="img"` + `aria-label`.

## The logo placeholder

The venture has no identity yet, so the lockup is provisional and deliberately isolated:

- **Working name:** "Deeptier" — a placeholder, not a naming recommendation.
- **Mark:** `.brand__mark`, three descending bars (teal, teal, copper) = three tiers with the deepest one
  accented. Pure CSS, 30×30, no image asset, no favicon dependency.
- **`logo tbd` chip:** `.brand__tbd`, the dashed monospace tag beside the wordmark. Visible on purpose so
  no stakeholder mistakes it for final.

**To swap in the real identity:** replace the `.brand` block in the header and footer of all five pages,
delete `.brand__tbd` from the markup and from the stylesheet, and update the `--teal-*` / `--copper-*`
tokens if the brand palette differs. Nothing in the layout depends on the mark's shape or size.

## Open assumption

The purchase-order cascade is rendered as **Anchor → PO → Tier 1 → PO → Tier 2**, with tier 2's invoice
raised on tier 1, and tier 1's machined output flowing back to the anchor.

The founding brief described this chain in two slightly different ways. This is the reading consistent
with the rest of it — the tier 2 invoice tracing to tier 1's PO, and tier 1's machining output tracing to
the anchor. If the anchor in fact issues purchase orders directly to tier 2, three places need editing:

1. `.chain` in [`index.html`](../index.html) (Solution section)
2. `.chain` in [`how-it-works.html`](../how-it-works.html) (The chain section)
3. `.tierstack` in the [`index.html`](../index.html) hero

## Copy rules

- Every figure, dashboard, and supplier example is illustrative and must be labelled as such. The two
  mockup panels each carry an "Illustrative" chip **and** a disclaimer line.
- The footer carries a not-an-offer-of-credit line on every page. Keep it there.
- No named customers, funders, volumes, or rates until legal has cleared them. This is a regulated-adjacent
  subject and unverifiable claims are a real liability, not a marketing question.
