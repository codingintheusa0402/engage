# engage

Static, unlisted GitHub Pages site with daily phone checklists for Instagram engagement (comment / follow / like).
The pages are written in Korean, made for a phone, and overwritten by an outside generator. Nothing in this repo is
written by hand.

## How it runs

- Served from `main` by GitHub Pages at `https://codingintheusa0402.github.io/engage/`. `.nojekyll` makes Pages serve
  the files as they are.
- Not for search engines: `robots.txt` disallows everything, every page has `<meta name="robots" content="noindex">`,
  and the root `index.html` is an empty placeholder. Pages live under random folder names.
- The generator (not in this repo) commits a new version of each page every day:
  - `<date> he1`, `<date> owo`, `<date> 3am`: one checklist per Instagram account.
  - `remind <date>`: the "오늘 소통 남은 것" (what's left today) reminder page.

## Pages

| Folder | Content |
| --- | --- |
| `j8t2pt/` | Checklist for the 💻 account |
| `bsqwqx/` | Checklist for the 📷 account |
| `zkra73/` | Checklist for the 🌙 account |
| `b7k7cy/` | Reminder page: one card per account with what's left (follows left, comments, likes), linking to that account's checklist with `?d=YYYYMMDD` |

Each checklist page has:

1. **① 댓글 (comments)**: a link to the post, a short note, the suggested comment, and a **댓글 복사** (copy comment) button.
2. **② 팔로우 (follows)**: accounts to follow and like 2–3 recent posts.
3. **③ 좋아요 (likes)**: accounts already followed; like 1–2 recent posts.

A section can be empty (count 0). An orange `⚠️` note at the top says when the generator found fewer items than usual,
for example when its browser was logged out of Instagram or only one account met the criteria that day.

## Usage

Open the page on the phone that is logged in to the right Instagram account (the page tells you to check this first).
Tapping a link or a checkbox ticks the row. Ticks are stored in `localStorage` on that phone only, under the key
`eng-<account>-<date>`, so a new day starts with a clean list. When opened in the KakaoTalk in-app browser, the page
reopens itself in the phone's default browser.

## Setup

Nothing to build or install. To change the content, change the generator; edits made by hand here are overwritten by
the next daily commit.
