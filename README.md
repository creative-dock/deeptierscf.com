# Deep-Tier Supply Chain Finance — microsite

Marketing microsite for a venture that delivers supply chain financing to the **deeper tiers** of
industrial supply chains — tier 2 and below — without either the anchor OEM or the tier 1 having to stand
up a funding program inside treasury.

Static, dependency-free, five pages. No build step, no framework, no external network requests.

> **Status:** pre-launch. The brand identity is not defined; the site ships a deliberate, clearly-labelled
> logo placeholder. All figures and dashboards in the copy are illustrative.

---

## Table of contents

- [What this site argues](#what-this-site-argues)
- [Pages](#pages)
- [Running it locally](#running-it-locally)
- [Project structure](#project-structure)
- [Design system](#design-system)
- [The logo placeholder](#the-logo-placeholder)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [Open assumption](#open-assumption)
- [Legal](#legal)

---

## What this site argues

Conventional supply chain finance reaches only the suppliers an anchor invoices directly. Below that line,
small firms fund the anchor's production order out of their own pocket or on a high-street rate priced
against their own balance sheet — and nobody upstream can see the strain until a delivery is missed.

The venture's answer is to replace the *program* with a *verified story*. With permissioned access to
documents already moving between ERP systems, the chain behind a single invoice is reconstructed:

```
Anchor / OEM  ──PO──▶  Tier 1  ──PO──▶  Tier 2
                                          │
                          invoice + delivery
                                          ▼
                                       Tier 1
```

A funder bank then lends **directly into that transaction**, with the anchor's and tier 1's credit quality
in view, rather than underwriting a small supplier in isolation. Neither the anchor nor the tier 1
contracts a facility, confirms payables, or changes payment terms — their contribution is data.

In exchange, they get back what they never had: a mapped deeper supply base with financial-health and
criticality signals on firms they have no commercial relationship with. Liquidity flows down; supply-chain
intelligence flows up.

## Pages

| File | Audience | Contents |
| --- | --- | --- |
| [`index.html`](index.html) | All | Hero, **§1 Problem**, **§2 Solution**, **§3 three benefit cards** (OEM/Anchor · Tier 1 · Tier 2+), closing CTA |
| [`anchors.html`](anchors.html) | OEM / anchor buyers | The exposure, deep-tier signal dashboard, visibility as return on data, what they never take on, 4-step participation |
| [`tier-1.html`](tier-1.html) | Tier 1 suppliers | The squeeze from both sides, sub-tier liquidity they don't fund, comparison vs. paying early or extending their own credit |
| [`tier-2.html`](tier-2.html) | Tier 2 and beyond | The two bad options today, six benefits, funding-application panel, what the application needs |
| [`how-it-works.html`](how-it-works.html) | All | The chain, 7-step end-to-end flow, the data-for-liquidity exchange per party, comparison vs. conventional SCF, 8-question FAQ |

Each benefit card on the landing page deep-links to its role page; every role page routes onward to
`how-it-works.html#start`.

## Running it locally

Any static file server works. With Python's standard library:

```bash
python3 -m http.server 4321
```

Then open <http://localhost:4321>.

Opening the files directly over `file://` also works, since there is no bundler and no fetch call — but
serve over HTTP if you want root-relative paths and nav highlighting to behave exactly as in production.

## Project structure

```
.
├── index.html              # Landing page (problem / solution / benefits)
├── anchors.html            # OEM / anchor
├── tier-1.html             # Tier 1
├── tier-2.html             # Tier 2+
├── how-it-works.html       # Mechanics, comparison, FAQ
├── assets/
│   ├── css/site.css        # The entire design system — tokens + components
│   └── js/site.js          # Mobile nav, active-nav state, scroll reveal (~50 lines)
├── docs/
│   └── DESIGN.md           # Design system reference — read before adding a page
├── .editorconfig
├── .gitattributes
├── .gitignore
├── CONTRIBUTING.md
├── LICENSE                 # Proprietary — all rights reserved
└── README.md
```

There is intentionally no `package.json`. Adding a toolchain to five static pages would cost more than it
returns; if the site later grows into a product surface, that is the moment to reconsider.

## Design system

**Dark-first ink base + teal primary + warm copper accent.** In brief:

| Role | Token | Value |
| --- | --- | --- |
| Background | `--ink-900` | `#070c12` |
| Primary | `--teal-500` → `--teal-300` | `#14b8a6` → `#6ee7d5` |
| Accent | `--copper-400` | `#e08a3c` |
| Body text | `--text` | `#e8eef4` |

Why not navy: over 70% of B2B SaaS and fintech brands use blue as primary, so it reads generic on a
shortlist. Teal keeps the trust association of the blue family while being ownable, and pairing a
blue-family hue with a warm copper accent is the 2026 differentiator in financial services — it measures
better on perceived trustworthiness than blue-on-blue. Dark plus a metallic accent is the current
premium-finance signal.

**The accents are semantic, not decorative:** teal = the chain, verification, and the data contributors
(anchor, tier 1). Copper = tier 2+, the financeable event, and strain states. This is why `tier-2.html`
uses copper CTAs and nothing else does.

Full token table, component reference, accessibility rules, and breakpoints: **[`docs/DESIGN.md`](docs/DESIGN.md)**.

## The logo placeholder

No identity exists yet, so the lockup is provisional and isolated:

- **Working name** "Deeptier" — a placeholder, not a naming recommendation.
- **Mark** — three descending CSS bars (teal, teal, copper): three tiers, deepest one accented. No image
  asset.
- **`logo tbd` chip** — visible on purpose, so no stakeholder mistakes it for final.

To swap in the real identity: replace the `.brand` block in the header and footer of all five pages,
delete `.brand__tbd` from markup and CSS, and update the colour tokens if the brand palette differs.
Nothing in the layout depends on the mark.

## Deployment

Because the output is plain static files, any of these work with zero configuration — point the host at
the repository root:

- **GitHub Pages** — Settings → Pages → deploy from branch `main`, folder `/ (root)`.
- **Cloudflare Pages / Netlify / Vercel** — no build command, output directory `.`.
- **S3 + CloudFront** or any other object store behind a CDN.

No deployment workflow is committed. That is deliberate: the repository is proprietary and pre-launch, so
publishing should be an explicit decision rather than a side effect of merging to `main`. Add a workflow
when the venture is ready to be publicly visible.

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md). The short version: read `docs/DESIGN.md` first, use existing
tokens and components rather than new hex values, check 1280px and 375px, and don't add unverifiable
commercial claims.

## Open assumption

The purchase-order cascade is rendered as **Anchor → Tier 1 → Tier 2**. The founding brief described the
chain in two slightly different ways, and this is the reading consistent with the rest of it (the tier 2
invoice tracing to tier 1's PO, and tier 1's machined output tracing to the anchor).

If the anchor in fact issues purchase orders directly to tier 2, three blocks need editing — they are
listed in [`docs/DESIGN.md`](docs/DESIGN.md#open-assumption).

## Legal

Proprietary and confidential. See [`LICENSE`](LICENSE) — all rights reserved, no reuse rights granted.

Nothing in this repository or the site it produces constitutes an offer of credit or investment, legal,
tax, or financial advice. All figures, dashboards, and supplier examples are illustrative. The footer
carries a not-an-offer-of-credit disclaimer on every page; keep it there.

Once the venture is incorporated as its own legal entity, update the copyright holder in `LICENSE`.
