# Day of China

**Day of China** — *A Day in the Life of a Chinese Person.*

A small guide to Chinese traditional culture, taught the way it is actually
lived: one ordinary day at a time. From morning tai chi in the park to a foot
soak before bed.

## Site

- Live: https://dayofchina.com
- Status: live — homepage, 3 moment pages, guides, About, magazine, daily, and the calendar (Nov 2026 – Dec 2027, Gregorian + lunar + solar terms).

## This repo

A static site. No build step, no JavaScript, no tracking, no external
dependencies. System font stack only.

- `index.html` — homepage (English-first; Chinese terms marked with `lang="zh"`).
- `moments/` — the eleven moments; 3 written so far (6:30, 10:30, 16:00).
- `daily/` — one short piece a day (today's date, today's solar term, one thing in season).
- `guides/` — printable PDF guides; the first (Tai Chi) is coming soon.
- `magazine/` — the magazine: daily pieces become a biweekly issue every solar term, and a monthly issue every month. Coming soon.
- `calendar/` — the old calendar, month by month (Nov 2026 – Dec 2027): Gregorian dates, lunar dates, the twenty-four solar terms and the festivals. Built from `/tmp/cal_data.json` by `/tmp/doc_build.py`.
- `about/` — what the site is, and the twelve two-hour periods.
- `DESIGN.md` — the design system: thesis, tokens with contrast figures, type, spacing, components, references, and the considered decisions.
- `llms.txt`, `llms-full.txt`, `sitemap.xml`, `robots.txt`.

## Preview

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
```

## Deploy

Cloudflare Pages, connected to this repo (production branch `main`, no build
command, output directory `/`). Custom domain: `dayofchina.com`.
