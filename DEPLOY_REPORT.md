# Deploy report — 2026-11-21

## Links
- GitHub repo: https://github.com/seyedhasanmirhoseini1367/sports-prototype
- Live site (Render): https://sports-prototype.onrender.com
- Custom domain https://sports.hasanai.net: **not set up yet** (see Step 4 and NEXT_STEPS.md)

## Status per step
| Step | Status |
|---|---|
| 1. Project setup (folder, index.html, README, .gitignore, first commit) | Done |
| 2. UI change: sticker reactions by default, meter behind flag | Done, tested |
| 3. GitHub repo `sports-prototype` (public) and push | Done |
| 4. Render static site | Done: deploy succeeded, site returns HTTP 200 |
| 4.5. Custom domain on Render | **Blocked**: workspace plan allows 2 custom domains and both are used (hasanai.net + www, healthcompass.hasanai.net) |
| 5. DNS CNAME `sports` in Cloudflare | **Not done on purpose**: a record pointing at Render would fail verification while the domain cannot be added there |
| 6. Report | Done |

## Test results (local browser, before deploy)
- No console errors.
- Feed renders 3 posts; no cheer button or meter bar in sticker mode.
- Sticker button opens the tray with the sport's own stickers (Football: Goal!, Fire, Great save, Red card, GOAT), icon only, with aria-label and title.
- Picking a sticker adds 1 to the count (2,140 → 2,141); picking the same one again removes it (back to 2,140).
- Double-tapping a video picks that sport's first sticker (Drill → Respect).
- Bottom nav (Home, Explore, Create, Chat, Me) and Home tabs (Feed, Challenges, Training, Events) all switch correctly.
- With `REACTION_MODE = 'meter'`, the old cheer button and meter work as before.

## Decisions I made on my own
1. **Toggle and count:** the count is the post's base count plus 1 while you have a sticker picked. Picking the same sticker again removes it and the +1.
2. **Double-tap** sets the first sticker; if it's already picked, it stays picked instead of toggling off.
3. **Sticker stack on the video** (top-right corner) is hidden in sticker mode, because the same stack now sits in the action row. It still shows in meter mode.
4. **Pass/share button:** the old row had no share icon, so I added a paper-plane "Pass" button that shows a toast "Pass to a teammate".
5. **Render GitHub access:** Render's GitHub app could only see HealthCompass, so I added `sports-prototype` to it (you entered the 2FA code). HealthCompass access was left unchanged.
6. **Render settings:** name `sports-prototype`, branch `main`, no build command, publish directory `.`, auto-deploy "On Commit".
7. **No DNS record added**, because Render could not accept the domain (plan limit). Existing Render services and DNS records were not touched.
8. Local testing used a small Node server, since Python isn't installed.

## How to update the site
1. Edit `index.html`.
2. `git commit -am "your message"`
3. `git push`
4. Render deploys automatically within a minute.

To switch back to the old crowd meter, change `REACTION_MODE` to `'meter'` in `index.html`.
