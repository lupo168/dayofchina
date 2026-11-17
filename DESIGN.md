# Day of China — Design system

## Thesis

A day in China, printed like a page from an almanac. One day, eleven moments,
one calendar. The site is a printed page, not an app: rice paper, ink, and one
seal stamp in vermilion.

## Why this is not a template

Warm cream with a serif and a terracotta accent is a common generated look.
Here the palette is the almanac's own materials, not a default: the paper is
rice paper, the vermilion is the seal stamp (朱砂), the ink is printing ink.
The vermilion is spent in exactly one place — solar terms, today, and labels —
and nowhere else. If the vermilion were removed, the site would still be
itself; if the paper were removed, it would not.

## Tokens

| Token | Value | Role | Contrast on paper |
| --- | --- | --- | --- |
| paper | `#faf6ef` | Page background | — |
| card | `#fffdf8` | Card / table background | 1.06:1 (decorative) |
| ink | `#211c16` | Body text, structural rules | 15.69:1 |
| muted | `#5c554b` | Secondary text (lunar dates, metadata) | 6.83:1 |
| vermilion | `#a93226` | Terms, today, current page, focus | 6.15:1 |
| vermilion-dark | `#8e2a1f` | Vermilion at small sizes if needed | 7.79:1 |
| rule | `#e3d9c8` | Hairline rules (decorative only) | 1.30:1 |

All text meets 4.5:1. The current-page indicator is vermilion (6.15:1, above
the 3:1 non-text minimum) **plus** an underline — never color alone. Today is
vermilion **plus** the word "Today". Past days are not dimmed: dimming would
drop their text below 4.5:1, and past days are still content.

## Type

- Display: system serif (`Georgia, 'Times New Roman', serif`) for headings
  and the big numbers. Body: system serif. Metadata: system sans.
- Scale (rem only, never px for font sizes): h1
  `clamp(1.75rem, 1.25rem + 2vw, 2.5rem)`, h2 `1.5rem`, body `1.0625rem`
  with unitless line-height `1.7`, small text `0.875rem` minimum (10 pt floor).
- `text-wrap: balance` on headings, `text-wrap: pretty` on prose.
- Column: `44rem` (about 70 characters, under the 80-character cap).

## Spacing

- Section: `2.5rem`. Between months: `4rem` with a 2 px ink rule.
- Nav gap: `0.5rem`; nav links padded to a 24 px minimum target
  (`0.4rem 0.55rem`), larger on coarse pointers.
- Day cell: `0.6rem 0.25rem`; three lines — Gregorian number, lunar date,
  term or festival.

## Components

- **Nav**: one `<nav aria-label="Main">`, links as a `<ul role="list">`
  (Safari drops list semantics on flex lists without the role). Current page:
  `aria-current="page"` + vermilion + underline. Wraps on narrow screens;
  no JavaScript, no popover — the site promises zero JS.
- **Skip link**: "Skip to main content", visually hidden until focused,
  targeting `<main id="main" tabindex="-1">`.
- **Header / footer**: `<header>` wraps the nav; `<footer>` is one quiet line.
- **Month table**: semantic `<table>` (a month is tabular data) with a
  visually-hidden `<caption>`, `<th scope="col">` weekday headers with
  `<abbr>` full names, sticky `<thead>`, and a `.table-wrapper`
  (`tabindex="0"`, `role="region"`, `aria-labelledby`, `overflow: auto`,
  `container-type: inline-size`). On narrow containers the cells shrink
  their padding; the grid never becomes stacked cards — the grid is the
  meaning.
- **Day cell**: Gregorian number largest, lunar date smaller and muted, term
  or festival smallest in vermilion. English first, Chinese as the note.
- **Focus**: `:focus-visible` — 3 px vermilion outline, 3 px offset.
  Forced Colors Mode: system keywords for the current-page indicator and
  focus ring.
- **No**: rounded cards, shadows, fills, gradients, emoji, icons, JS.

## References (refero.design, 2026-11-17)

- Niccolò Miranda — paper system and vermilion used only for tiny labels.
  https://refero.design/styles/fccd276e-3af9-49c2-9673-d7f7e3f5e9a9
- Kinfolk — quiet editorial type, 32 px section headings, 2 px rules, big
  gaps between sections.
  https://refero.design/styles/225a1a8d-48b2-4b1e-a3a8-ca2b797f4701
- Coinbase date picker — month grid with no cell borders or fills, two-letter
  weekday headers, one marked day.
  https://refero.design/pages/4c255140-dde9-4931-9614-97cbe65fd127
- OKURI tear-off calendar — three-line day cell: big number, small note,
  smallest accent.
  https://refero.design/screens/b977ab0d-3578-49e9-92a5-8ea423cc7de0
- It's Nice That (supplementary) — 1 px seams, right angles, titles never
  bolded for hierarchy.
  https://refero.design/styles/0956bb40-31e2-4a19-85ea-fd0d373add96

Avoid: colour-blocked scheduling calendars, gamified/neon calendars, filled
cells, floating shadows, bold condensed titles as hierarchy.

## Considered decisions

- **No dark mode.** The paper is the product; inverting it would break the
  almanac thesis. Documented, not overlooked.
- **No popover nav.** The navbar guide's popover pattern needs JavaScript
  and anchor positioning; the site promises zero JS, so the nav wraps.
- **No dimming past days.** See Tokens: dimming breaks the 4.5:1 floor.
- **Calendar as `<table>`, not CSS grid.** A month is tabular data; the
  responsive-table guide requires real table semantics for it.
- **Lunar dates precomputed at build time** (lunardate library, cross-checked
  against public almanacs), not calculated in the browser — no Temporal
  polyfill, no Safari gap.

## Guides applied (modern-web-guidance)

- `responsive-table` — month tables: semantic table, sticky header, scrollable
  region wrapper, container queries.
- `support-global-calendar-systems` — checked; not applied as client code
  (dates are precomputed, see above), its invariant lesson honored in the data.
- `css-layout` — grid/flex decision tree, logical properties, intrinsic sizing.
- `navbar` — one nav landmark, `aria-current="page"` plus a non-color
  indicator, `:focus-visible`, no menu roles.
- `accessibility` — landmarks, one h1, skip link, `scope="col"`, 24 px
  targets, visually-hidden utility.
- `responsive-design` — `clamp()` type, container queries over viewport queries.
- `color` — 4.5:1 / 3:1 floors computed from hex, forced-colors fallbacks.
- `typography` — rem font sizes, unitless line-height, `text-wrap: balance`
  and `pretty`, 80-character cap.

## Process

Refero references → design system (this file) → modern-web-guidance search and
retrieve → build → Apple design lens review → axe-core scan (serious and
critical to zero) → push gate (file list vs live inventory, no deletions) →
launch checks (curl every sitemap URL, www/apex/http/https, MD5, purge) →
cloud-browser screenshot verification.
