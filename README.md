# engage

Static, unlisted GitHub Pages site with daily Instagram engagement checklists, built for a phone screen.
Each page lists the comments, follows and likes to do that day for one Instagram account, so the work can be ticked
off quickly on the phone.

The pages are **generated output**. The tool that picks the target accounts and writes the comment drafts is not in
this repository. It overwrites the HTML files here and commits them once a day.

## Layout

| Path | What it is |
| --- | --- |
| `index.html` | Blank placeholder (`noindex`), so the site root shows nothing. |
| `robots.txt` | `Disallow: /` for all crawlers. |
| `.nojekyll` | Serves the files as-is, with no Jekyll processing. |
| `j8t2pt/`, `zkra73/`, `bsqwqx/` | One checklist page per Instagram account. The folder names are random slugs, so the URLs can't be guessed. |
| `b7k7cy/` | Daily reminder page that links to the three checklists and shows what is still left on each. |

Every page is a single self-contained `index.html` with inline CSS and JS. There are no dependencies and no build
step. All pages carry `noindex,nofollow`.

## Checklist page (`<slug>/index.html`)

- The header shows the account and date. Below it: "about 5 minutes", a reminder to check that the Instagram app is
  logged in to the right account, and a note that ticks are saved on this phone only.
- If few candidates qualified that day, a warning shows how many did (`오늘은 조건 맞는 계정이 N곳뿐이에요`).
- The page has three sections:
  1. **댓글 (comments)**: a link to the post, a short note on the post, a comment draft and a **댓글 복사** button
     that copies the draft to the clipboard. It has a `textarea` fallback for browsers without the Clipboard API.
  2. **팔로우 (follows)**: profiles to follow, with follower count and niche. The page asks you to also like 2–3
     recent posts.
  3. **좋아요 (likes)**: accounts you already follow; like 1–2 recent posts on each.
- Each row has a checkbox. Tapping a row's link marks it done automatically. Ticks are stored in `localStorage`
  under `eng-<account>-<YYYY-MM-DD>`, so each day starts fresh. A section with nothing to do that day shows only its
  heading with count 0.
- In the KakaoTalk in-app browser, the page redirects itself to the external browser
  (`kakaotalk://web/openExternal`).

## Reminder page (`b7k7cy/index.html`)

Titled `오늘 소통 남은 것 · <date>` ("what's left today"). It shows one card per account with the follows left and the
comment count, linking to `https://codingintheusa0402.github.io/engage/<slug>/?d=YYYYMMDD`. Unfinished items don't
carry over: the next day brings a new list.

## Daily update cadence

The commits follow a fixed pattern each day:

- `YYYY-MM-DD he1`: updates `j8t2pt/index.html`
- `YYYY-MM-DD 3am`: updates `zkra73/index.html`
- `YYYY-MM-DD owo`: updates `bsqwqx/index.html`
- `remind YYYY-MM-DD`: updates `b7k7cy/index.html`

## Running locally

```sh
python3 -m http.server 8000
# open http://localhost:8000/j8t2pt/
```

## Deploying

Serve from GitHub Pages on the default branch, from the repo root. Pushing a regenerated page publishes it.
