# SkyWatch 🛰️

A live dashboard for everything moving through the sky — weather, aircraft, the ISS, ISRO missions, and rocket launch countdowns. Built as a static website (plain HTML/CSS/JS, no build step, no backend).

## What's inside

```
skywatch/
├── index.html          → Home page
├── forecast.html        → 7-day weather forecast + hourly chart
├── map.html            → Interactive world map
├── aircraft.html        → Live aircraft radar embed
├── iss.html             → ISS live position tracker
├── isro.html            → ISRO mission timeline
├── launches.html        → Live launch countdowns
├── css/                 → One stylesheet per page + base.css (shared)
├── js/                  → One script per page + core.js (shared)
└── README.md            → You are here
```

All pages share the same dark "mission control" look, the top telemetry bar (HUD), and the navigation — so it feels like one connected dashboard rather than separate sites.

## Live data sources (all free, no API key required)

- **Weather** — [Open-Meteo](https://open-meteo.com)
- **Map tiles** — [CARTO](https://carto.com) dark tiles + [OpenStreetMap](https://www.openstreetmap.org) data, via [Leaflet.js](https://leafletjs.com)
- **Aircraft radar** — embedded [Flightradar24](https://www.flightradar24.com) live map
- **ISS position** — [WhereTheISS.at](https://wheretheiss.at)
- **Launch schedule** — [Launch Library 2](https://thespacedevs.com) by The Space Devs
- **ISRO timeline** — hand-written, fact-checked mission history (static data, no API)

Because everything calls free public APIs directly from the browser, **there is no backend to host and no secret keys to manage.** This also means the site needs an internet connection to show live data — the page structure and design always work, but weather/map/ISS/launch numbers need a live connection.

## How to put this on GitHub (step by step)

You don't need to know git command-line for this — GitHub's website can do it all.

### 1. Create a GitHub account
If you don't have one already, sign up at [github.com](https://github.com).

### 2. Create a new repository
1. Click the **+** icon top-right → **New repository**.
2. Name it something like `skywatch` (this name will appear in your URL).
3. Set it to **Public**.
4. Don't add a README/gitignore (you already have one) — just click **Create repository**.

### 3. Upload the files
1. On your new (empty) repository page, click **uploading an existing file**.
2. Unzip the `skywatch.zip` file you downloaded on your computer first.
3. Drag the **contents** of the unzipped folder (the `index.html` file, the `css` folder, the `js` folder, etc — not the outer folder itself) into the upload box.
4. Scroll down, write a commit message like "Initial upload", and click **Commit changes**.

### 4. Turn on GitHub Pages (this makes it a live website)
1. In your repository, go to **Settings** (top tab).
2. In the left sidebar, click **Pages**.
3. Under "Build and deployment" → "Branch", choose **main** and folder **/ (root)**, then click **Save**.
4. Wait about 1–2 minutes. Refresh the page — you'll see a green box with your live URL, something like:
   `https://yourusername.github.io/skywatch/`

That's it — your site is live and free, forever, with no server to maintain.

### 5. Making changes later
Any time you want to edit something:
- Click the file in GitHub → pencil/edit icon → make your change → **Commit changes**.
- GitHub Pages automatically redeploys within a minute or two.

## Running it locally before you upload (optional)

If you want to preview it on your own computer first:
1. Unzip the folder.
2. Open a terminal/command prompt inside the folder.
3. Run: `python3 -m http.server 8000` (Python is preinstalled on most Macs/Linux; on Windows, install Python first or use the VS Code "Live Server" extension instead).
4. Open `http://localhost:8000` in your browser.

You can also just double-click `index.html` to open it directly in a browser, though a couple of features (like geolocation) work better served from a real local server.

## Customizing

- **Colors / fonts** — edit the CSS variables at the top of `css/base.css` (the `:root` block). Every page inherits from these.
- **Default city on the forecast page** — edit the last line of `js/forecast.js` (`loadWeather(18.5204, 73.8567, "Pune, India")`).
- **Nav links / page order** — edit the `<nav class="primary">` block, which is repeated at the top of every HTML file.

## Notes & known limitations

- The aircraft radar page embeds Flightradar24's public simple map. If a network blocks third-party iframes, the radar panel will show blank — this is a network/browser restriction, not a bug in the code.
- All "live" data depends on third-party free APIs staying up; if one is temporarily down, that page will show a small status message rather than breaking the page.
- Page transitions and animations respect `prefers-reduced-motion` for visitors who have that turned on.
