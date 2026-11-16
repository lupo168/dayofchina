# Day of China

**Day of China** — *A Day in the Life of a Chinese Person.*

A small guide to Chinese traditional culture, taught the way it is actually
lived: one ordinary day at a time. From morning tai chi in the park to a foot
soak before bed.

## Site

- Live: https://dayofchina.com
- Status: coming soon — the first guide is on its way.

## This repo

A single static page. No build step, no JavaScript, no tracking, no external
dependencies. System font stack only.

- `index.html` — the coming-soon homepage (English-first; Chinese terms
  marked with `lang="zh"`).

## Preview

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
```

## Deploy

Cloudflare Pages, connected to this repo (production branch `main`, no build
command, output directory `/`). Custom domain: `dayofchina.com`.
