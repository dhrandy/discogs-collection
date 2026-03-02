# 🎶 Discogs Collection Viewer

A clean, mobile-friendly single-file web app for browsing your Discogs vinyl (or any format) collection. No server, no build step, no dependencies — just open the HTML file in a browser or self-host it.

![Static Badge](https://img.shields.io/badge/single--file-HTML-blue) ![Static Badge](https://img.shields.io/badge/no_dependencies-✓-blue) ![Static Badge](https://img.shields.io/badge/mobile--friendly-✓-blue)

## Demo Site

https://discogs-collection.netlify.app/

Don't use your token on this site. If there's an error, make sure your Discogs collection is public under your settings/privacy "Allow others to browse my collection" on the Discogs website. Then save and refresh.

## Screenshot

![Screenshot_2-3-2026_184221_collection compact synology me](https://github.com/user-attachments/assets/183b4d3d-849f-4d20-bbb7-93330127665a)

---

## Features

- **Random Button** — picks a random album from your current filtered view
- **Wantlist tab** — toggle between your collection and your Discogs wantlist
- **Browse your full collection** with album art in a responsive grid
- **Grid / Shelf view toggle** — switch between a compact grid and a single-column shelf view with full metadata
- **Grouped duplicates** — multiple pressings of the same album are combined into one card with a copies count badge; tap to expand all pressings
- **Format badges** — coloured tags on each album cover showing Vinyl, CD, Cassette, etc.
- **Live search** — filter by artist, album title, label, exact year, decade (`70s`, `1980s`), or year range (`1965-1972`)
- **Format filter pills** — one-tap to show only Vinyl, CD, Box Set, etc.
- **Genre / style filter** — collapsible filter pills pulled from your collection's genre and style tags
- **Sort** by Artist (A–Z), Year, or Recently Added — your last sort is remembered between sessions
- **Tracklist + runtime** — click any album to expand its track listing
- **Discogs link** — each card has a ↗ button to open the release on Discogs
- **Collector Dashboard** — stats for total releases, top artist, formats, and year range
- **Offline support** — after first load, your collection is cached and the app works without internet
- **Full pagination** — loads your entire collection, not just the first 50
- **Tracklist caching** — re-opening an album is instant after first load
- **XSS-safe** — all API data is handled securely via DOM methods

---

## Getting Started

### 1. Download the file

Save `discogs-collection.html` to your computer. That's the only file you need. Feel free to rename it to `index.html` if self-hosting.

### 2. Open it in your browser

Double-click the file, or drag it into any modern browser (Chrome, Safari, Firefox, Edge).

### 3. Enter your Discogs username

On first launch you'll see a setup screen. Enter your Discogs username (e.g. `dhrandy`) and click **Save**.

> Your username is saved to your browser's `localStorage` so you only need to enter it once.

---

## API Token (Optional)

An API token is required to load your **wantlist** or a **private collection**:

1. Log in to [discogs.com](https://www.discogs.com)
2. Go to **Settings → Developers**
3. Click **Generate new token**
4. Paste the token into the **API Token** field on the setup screen

> Your token is stored locally on your device only and is never sent anywhere except directly to the Discogs API.

---

## How to Use

### Searching

Type anything into the search bar to filter your collection in real time:

| Query | What it matches |
|---|---|
| `Johnny Cash` | Artist name |
| `american` | Album title containing "american" |
| `columbia` | Label name |
| `1975` | Exact year |
| `70s` or `1970s` | Any record from 1970–1979 |
| `1965-1972` | Any record from that year range |

Search, format pills, and genre filters all work together — for example, tap **Vinyl**, pick **Jazz**, and type `60s` to see only 60s jazz vinyl.

### Collection vs. Wantlist

Use the tabs at the top to switch between your **Collection** and your **Wantlist**. Both show the same filters and sorting options. The wantlist requires an API token if it's private.

### Grid vs. Shelf View

Use the view toggle button (next to the Random button) to switch layouts:

- **Grid** — compact multi-column view with album art, good for browsing by cover
- **Shelf** — single-column list with a small thumbnail and full metadata (title, artist, year, label, genres) readable at a glance. Better for scanning a large collection quickly.

Your last view is remembered between sessions.

### Duplicates / Multiple Pressings

If you own more than one pressing of the same album, they are grouped into a single card with an amber **2×** badge in the top-right corner of the cover. Tap the card to expand a list of all your pressings, each showing its year, label, and format. Tap any pressing row to expand its individual tracklist.

### Format & Genre Filters

Tap any **Format** pill (e.g. **Vinyl**, **CD**, **Box Set**) to filter to that format. Tap **All** to clear it.

Click **▶ Genre** to expand the genre/style filter and tap any tag to filter by it. An active genre stays visible as a badge next to the label even when collapsed.

### Sorting

Use the sort dropdown to order results by:
- **Artist (A–Z)** — ignores "The", "A", "An" and Discogs disambiguation numbers like `(2)`
- **Year (Oldest → Newest)**
- **Year (Newest → Oldest)**
- **Recently Added** — newest additions to your collection first
- **First Added** — oldest additions first

Your last sort is automatically restored the next time you open the app.

Records added in the last 30 days show a **🆕 Added X days ago** badge on their card.

### Random Record

Hit the **🎲 Random** button to pick a record at random from whatever you're currently viewing. A modal shows the full album art, tracklist, and a link to Discogs. Hit **Pick Another** to re-roll. If you own other pressings of the same album they'll be listed in the modal too.

### Tracklist

Tap any album card to expand its tracklist with track durations and total runtime. Tap again to collapse. Tracklists are cached after the first load so reopening is instant.

### Discogs Link

Each card has a small ↗ icon in the top-right corner. Tap it to open that release directly on Discogs in a new tab.

---

## Offline Support

After loading your collection for the first time, a service worker caches all Discogs API responses. If you open the app without an internet connection it will serve your collection from cache automatically. The cache refreshes whenever you're back online.

> Note: offline support requires the app to be served over HTTPS or `localhost`. It may not work when opening the file directly from disk in all browsers.

---

## Changing Accounts

Use the **Change User** button in the top-right corner to clear your saved username and token and return to the setup screen.

Alternatively, open your browser's developer tools and run:

```javascript
localStorage.removeItem("discogs_username");
localStorage.removeItem("discogs_token");
location.reload();
```

---

## Privacy & Security

- No data is ever sent to any server other than the official [Discogs API](https://www.discogs.com/developers)
- Your username and API token are stored only in your browser's `localStorage`
- All content from the Discogs API is handled safely (no `innerHTML` injection)
- The app runs entirely client-side with no tracking, analytics, or ads

---

## Limitations

- **Rate limiting** — Discogs allows 60 unauthenticated requests/minute and 240 authenticated requests/minute. Large collections may load slowly due to pagination. An API token helps.
- **Cover images** — some older releases on Discogs may have placeholder or missing artwork
- **Tracklist data** — each album's tracklist requires a separate API call when you first expand it
- **Genre data** — genres and styles come from the collection API and may not be present for all releases
- **Offline on file://** — the service worker may not register when opening the file directly from disk in some browsers. Self-host or use a local server for reliable offline support.

---

## Browser Support

Works in all modern browsers. Requires JavaScript enabled.

| Browser | Support |
|---|---|
| Chrome / Edge | ✅ |
| Safari (iOS + macOS) | ✅ |
| Firefox | ✅ |
| IE 11 | ❌ |

---

## License

This project is released for personal use. The Discogs name and API are the property of [Discogs](https://www.discogs.com). This tool is not affiliated with or endorsed by Discogs.
