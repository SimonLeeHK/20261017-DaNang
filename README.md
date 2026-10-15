# 我的旅程・十月 (trip companion)

A single-page trip app that works offline once it has been opened online. Put it on your iPhone home screen.

## Files

| File | Purpose |
|---|---|
| `index.html` | The app. Contains no trip data; it unlocks `trip.enc.json` with your password. |
| `trip.enc.json` | The whole plan, encrypted (AES-256-GCM, key from password via PBKDF2-SHA256, 600,000 rounds). |
| `trip.json` | The plain plan. **Only on your PC**, listed in `.gitignore`, never pushed. |
| `encrypt.html` | Turns `trip.json` into `trip.enc.json`, entirely in your browser. |
| `sw.js` | Offline support. Saves the app and fonts on the phone. |
| `manifest.webmanifest` | App name, icon and full-screen mode for "Add to Home Screen". |
| `icons/` | Home-screen icons. |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are. |

## Publish with GitHub Pages

1. On GitHub, create an empty **public** repository `SimonLeeHK/20261017-DaNang` (no README).
2. Push this folder:
   ```
   cd C:\temp\20261017-DaNang
   git push -u origin main
   ```
3. On GitHub, open **Settings**, then **Pages**. Under **Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, then **Save**.
4. After about a minute the site is at `https://simonleehk.github.io/20261017-DaNang/`.

## Install on iPhone

1. Open the link in **Safari** (not inside WhatsApp).
2. Tap **Share**, then **Add to Home Screen**.
3. Open it once from the home-screen icon while online. It now works in airplane mode.

Always use the home-screen icon. Ticks and the packing list are stored separately from Safari.

## Updating the plan

1. Edit `trip.json` on your PC. Placeholders are marked 待填 (to fill) or 待核實 (to verify).
2. Open `encrypt.html` in a browser. Choose `trip.json`, type the password twice, and also choose the current `trip.enc.json` so phones stay unlocked.
3. Replace `trip.enc.json` with the downloaded file.
4. In `sw.js`, change `VERSION` (for example `v1` to `v2`).
5. Commit and push. Open the app online. It shows the saved copy right away and downloads the new one in the background, so the update appears the next time you open it.

### trip.json notes

- `jp` holds a place's name in the local language (Vietnamese here). It is shown big on the "越南文給人看" (show in Vietnamese) screen.
- `lang` sets the language name, the "take me here" sentence and the "booking number" word.
- `money.presets` are the quick amounts in the converter.
- `skyline` picks a drawing per city: `coast` (bridge, Ferris wheel, palms) or `lanterns` (old town, lanterns).
- Places with `kind: "beauty"` appear under the 美甲 filter, `cafe` under 咖啡, `music` under 音樂 and `shop` under 服飾. A filter chip only shows if at least one place has that kind. Places not used in any day show 未排入行程. Optional `links: { ig, fb, x, web }` (https URLs) on places or tickets add Instagram / Facebook / X / 網站 buttons to the card.
- Tickets with `kind: "food"` go into 票夾 → 餐廳訂位. Optional `ask`/`en` set the sentence shown above the booking name.
- Set `hotel: null` on the last day to hide the "tonight's hotel" card. A day with `items: []` shows a 自由活動 (free day) card.
- A day item can set `title` to override the place name, e.g. "退房（可寄存行李）".
- `help.pack` can be a flat list or groups: `[{group, note?, items: [...]}]`. Groups fold open/closed, and ticks are saved per device.

## Preview a moment in the trip

Add `?now=2026-10-17T18:40` to the address to see the app as it would look at that date and time.

## Privacy

The lock-screen emblem (a pizza sun over a sea of spaghetti) is drawn in `index.html`; the home-screen icons in `icons/` use the same artwork.


GitHub Pages sites are public, but the plan itself is encrypted: without the password a visitor sees only the lock screen, and the repository holds only scrambled data.

The repository name itself (`20261017-DaNang`) is public, so it reveals the date and destination. Rename the repository if you would rather hide that.

Each trip on `simonleehk.github.io` uses its own storage prefix (`dn26`), so several trips can sit side by side on one phone.
