# Deploy Guide — geocho.github.io/thunderads

The workspace folder isn't mounted to the `thunderads` git repo, so the push needs to happen from your local clone. Two minutes, three commands.

## Files to copy into the repo

From this workspace (the folder containing `index.html`):

| Source file | Target location in repo | Status |
|---|---|---|
| `index.html` | replaces existing `index.html` | updated — 2 featured + 3-col grid (3 live + 2 placeholders), all-English |
| `hoper-radio-case-study.html` | new file at repo root | new — Easter + Black Friday, LinkedIn share button |
| `hoper-brand-case-study.html` | new file at repo root | new — Don't go. Fly. platform + interactive system |
| `oilbattles-case-study.html` | new file at repo root | new — LinkedIn share button |
| `mastercard-review-case-study.html` | new file at repo root | new — 2024 Review brand film, YouTube embed |
| `google-tourism-case-study.html` | new file at repo root | new — Grow Greek Tourism Online, Drive video embed |
| `mastercard-case-study.html` | replaces existing `mastercard-case-study.html` | updated — OG tags, LinkedIn share button, next-case link |
| `hoper-apetaksamen-28.mp3` | new file at repo root | new audio asset |
| `hoper-easter-rf-30.mp3` | new file at repo root | new audio asset |
| `hoper-blackfriday-32.mp3` | new file at repo root | new audio asset |
| `hoper-blackfriday-9.mp3` | new file at repo root | new audio asset |

Leave `images/` and any other Mastercard assets in place.

## One-shot terminal script

Replace `~/thunderads` with the actual path to your local clone, then run:

```bash
REPO=~/thunderads
WORK="/Users/gc/Library/Application Support/Claude/local-agent-mode-sessions/62ebef5e-1903-4045-96eb-3974f292530e/d35da031-5487-481a-bea7-53364b0c3a03/local_e6b7987f-dd01-4fcb-8a03-7fa6bb479b55/outputs"

cp "$WORK/index.html" "$REPO/index.html"
cp "$WORK/hoper-radio-case-study.html" "$REPO/hoper-radio-case-study.html"
cp "$WORK/hoper-brand-case-study.html" "$REPO/hoper-brand-case-study.html"
cp "$WORK/oilbattles-case-study.html" "$REPO/oilbattles-case-study.html"
cp "$WORK/mastercard-review-case-study.html" "$REPO/mastercard-review-case-study.html"
cp "$WORK/google-tourism-case-study.html" "$REPO/google-tourism-case-study.html"
cp "$WORK/mastercard-case-study.html" "$REPO/mastercard-case-study.html"
cp "$WORK/hoper-apetaksamen-28.mp3" "$REPO/hoper-apetaksamen-28.mp3"
cp "$WORK/hoper-easter-rf-30.mp3" "$REPO/hoper-easter-rf-30.mp3"
cp "$WORK/hoper-blackfriday-32.mp3" "$REPO/hoper-blackfriday-32.mp3"
cp "$WORK/hoper-blackfriday-9.mp3" "$REPO/hoper-blackfriday-9.mp3"

cd "$REPO"
git add index.html hoper-radio-case-study.html hoper-brand-case-study.html oilbattles-case-study.html \
        mastercard-review-case-study.html google-tourism-case-study.html mastercard-case-study.html \
        hoper-apetaksamen-28.mp3 hoper-easter-rf-30.mp3 hoper-blackfriday-32.mp3 hoper-blackfriday-9.mp3
git commit -m "Add Google Grow Greek Tourism Online, Hoper (Brand + Radio), Mastercard 2024 Review and #OilBattles case studies"
git push
```

GitHub Pages will redeploy automatically, usually live at https://geocho.github.io/thunderads/ within a minute.

## After it's live, smoke-test these URLs

- https://geocho.github.io/thunderads/ — landing (Mastercard Forum + Hoper Radio featured; 2024 Review, Hoper Brand, Oilbattles in grid)
- https://geocho.github.io/thunderads/hoper-brand-case-study.html — the Pillar × Stage interactive demo should respond to clicks
- https://geocho.github.io/thunderads/hoper-radio-case-study.html — four audio spots should play inline (2 Easter, 2 Black Friday)
- https://geocho.github.io/thunderads/oilbattles-case-study.html — 5 Facebook video iframes should render
- https://geocho.github.io/thunderads/mastercard-review-case-study.html — the YouTube film should play inline
- https://geocho.github.io/thunderads/google-tourism-case-study.html — the Drive video should play inline (depends on the file staying link-shared)
- https://geocho.github.io/thunderads/mastercard-case-study.html — Share button at the bottom, next-case links to 2024 Review
- Paste any case study URL into https://www.linkedin.com/post-inspector/ to preview the LinkedIn share card

## Known Cloudflare quirk

Cloudflare on `geocho.github.io` re-wraps mailto links via its email-obfuscation script. The `george@thunderads.com` link works, but the URL Cloudflare shows looks like `/cdn-cgi/l/email-protection#...`. That's normal and clicking it still opens the user's mail client. If you want to clean it up later, the fix is one of:

1. Add `data-cfemail="0"` to the `<a>` tag, or
2. Disable Email Obfuscation under Cloudflare, Scrape Shield, for that domain.

Not blocking, just flagging since it's bitten the project before.
