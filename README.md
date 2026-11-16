# engage

A static GitHub Pages site (`https://codingintheusa0402.github.io/engage/`) that serves daily, phone-friendly
Instagram engagement checklists for three accounts. Each page is a single self-contained `index.html`
(inline CSS + JS, no build step, no dependencies). The pages are written in Korean.

The pages are **generated and committed by an external job**; the generator is not part of this repo. Every day it
overwrites the same four files, so the repo only ever holds the latest day. Commit subjects follow the pattern
`<YYYY-MM-DD> he1` / `3am` / `owo` (one per account page) and `remind <YYYY-MM-DD>` (the summary page).

## Pages

| Path | Page | What it shows |
|---|---|---|
| `j8t2pt/` | 💻 `he110w0r1.oi` | Daily checklist for that account |
| `zkra73/` | 🌙 `3am.mystery` | Daily checklist for that account |
| `bsqwqx/` | 📷 `owol.snap` | Daily checklist for that account |
| `b7k7cy/` | ⏰ 오늘 소통 남은 것 (what's left today) | One card per account linking to its page (`?d=YYYYMMDD`), with the follows left and the comment count |
| `index.html` | — | Empty placeholder (`noindex`) |

The folder names are random slugs so the pages are not guessable; there is no index linking to them.

## What an account page contains

- Header with the account and date, a "about 5 minutes / check the IG app is logged in as this account" line, and an
  optional orange warning note from the generator (e.g. when it could only collect part of the list).
- Three sections:
  1. **댓글 (comments)** – posts to open, each with a prepared comment and a **복사 (copy)** button
     (Clipboard API, with a `textarea` + `execCommand('copy')` fallback).
  2. **팔로우 (follows)** – accounts to follow and like 2–3 recent posts.
  3. **좋아요 (likes)** – existing accounts to like 1–2 recent posts.
- Each row has a checkbox. Tapping a link also ticks it (after 400 ms). Ticks are stored in `localStorage` under the
  key `eng-<account>-<date>`, so they live only on that phone/browser and reset automatically with the next day's page.

## Behaviour common to all pages

- Opened inside the KakaoTalk in-app browser, a page redirects to the external browser
  (`kakaotalk://web/openExternal?url=…`).
- Dark theme, max width 640 px, sized for phones.
- Not indexed: `robots.txt` disallows everything and every page has `<meta name="robots" content="noindex,nofollow">`.
- `.nojekyll` makes GitHub Pages serve the files as-is.

## Setup / running

Nothing to install. GitHub Pages serves the `main` branch root. To preview locally:

```sh
python3 -m http.server 8000
# open http://localhost:8000/b7k7cy/
```

There is no configuration or environment variable in this repo; all content is baked into the HTML by the generator.
