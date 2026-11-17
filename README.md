# Day of China

**Day of China** — *A Day in the Life of a Chinese Person.*

A small guide to Chinese traditional culture, taught the way it is actually
lived: one ordinary day at a time. From morning tai chi in the park to a foot
soak before bed.

## Site

- Live: https://dayofchina.com
- Status: live — homepage, 3 moment pages, guides, and About. The first guide is on its way.

## This repo

A static site. No build step, no JavaScript, no tracking, no external
dependencies. System font stack only.

- `index.html` — homepage (English-first; Chinese terms marked with `lang="zh"`).
- `moments/` — the eleven moments; 3 written so far (6:30, 10:30, 16:00).
- `guides/` — printable PDF guides; the first (Tai Chi) is coming soon.
- `about/` — what the site is, and the twelve two-hour periods.
- `llms.txt`, `llms-full.txt`, `sitemap.xml`, `robots.txt`.

## Preview

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
```

## Deploy

Cloudflare Pages, connected to this repo (production branch `main`, no build
command, output directory `/`). Custom domain: `dayofchina.com`.
