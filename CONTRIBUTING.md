# Contributing

Internal project. Access is granted for the purpose of developing, reviewing, or operating this site — see
[`LICENSE`](LICENSE).

## Before you start

Read [`docs/DESIGN.md`](docs/DESIGN.md). The whole visual system is one stylesheet with a defined token set
and a semantic colour rule; new work that ignores it is visible immediately and expensive to unpick.

## Setup

There is nothing to install.

```bash
python3 -m http.server 4321
```

Open <http://localhost:4321>.

## Ground rules

**Design**

- Use existing tokens (`--teal-500`, `--copper-400`, `--ink-850`, …). Never hard-code a hex value in
  markup or add a one-off colour to CSS — if a genuinely new value is needed, add a token and say why in
  the PR.
- Respect the accent rule: **teal** = the chain, verification, anchor and tier 1. **Copper** = tier 2+, the
  financeable event, strain and warning states. Copper should stay near 10% of any page.
- Reuse components (`.card`, `.benefit`, `.flow`, `.panel`, `.chain`, `.cmp`, `details.qa`) before writing
  new CSS. Most new sections are a composition of what already exists.
- Monospace is for labels, document IDs, and chips — not for prose.

**Markup**

- Two-space indentation, LF line endings (enforced by `.editorconfig` and `.gitattributes`).
- Each page is standalone: header, nav, and footer are duplicated per file by design, since there is no
  templating layer. **If you change the nav or footer, change it in all five pages.**
- Decorative SVG gets `aria-hidden="true"`. Meaningful diagrams get `role="img"` and a descriptive
  `aria-label`.
- Keep the `logo tbd` chip until the real identity lands.

**Copy**

- No named customers, funders, rates, or volumes until legal has cleared them. This is a
  regulated-adjacent subject; an unverifiable claim is a liability, not a marketing decision.
- Every figure, dashboard, or supplier example must be labelled illustrative and carry a disclaimer.
- Keep the not-an-offer-of-credit line in the footer of every page.

## Checks before opening a PR

- [ ] Renders correctly at **1280px** and **375px**.
- [ ] No horizontal scroll on the page body. Wide content scrolls inside its own container
      (`.tablewrap`), never the body.
- [ ] Mobile nav opens, closes on link click, and highlights the current page.
- [ ] Keyboard tab order is sane and focus rings are visible.
- [ ] Animations respect `prefers-reduced-motion` — with it enabled, all content is visible and static.
- [ ] Nav and footer edits applied to **all five** pages.
- [ ] No new external network requests (no CDN scripts, no remote fonts, no remote images). The site must
      keep working fully offline.
- [ ] No secrets, credentials, or real supplier data committed.

## Commits and branches

- Branch off `main`: `feat/…`, `fix/…`, `copy/…`, `design/…`.
- Imperative, specific subject lines: `copy: tighten tier 1 comparison table`, not `updates`.
- Open a PR rather than pushing to `main`. Copy changes need a second reader — this site makes commercial
  claims about a financing product.
