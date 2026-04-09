# Music Player

A self-contained web-based music player in a single HTML file. Runs entirely in the browser — no backend, no accounts, no tracking.

## Features

- **Local music** — add files or scan folders (Chrome/Android)
- **YouTube** — paste a link, plays as audio with optional video toggle
- **Library** — browse by songs, artists, albums; search and filter
- **Playlists** — create, rename, reorder; add tracks from any view
- **Queue** — play next, add to queue, shuffle, repeat (off/all/one)
- **Now Playing** — album art or video, seek bar, volume, lock-screen controls (Media Session API)
- **Themes** — Dark, AMOLED, Light, Ocean, Purple, Rose
- **Custom background** — set any image URL as a tinted wallpaper
- **Persistent** — library, playlists, playback position, settings all stored in IndexedDB
- **Offline** — local files work without internet; YouTube requires a connection
- **Mobile-first** — touch-friendly, responsive, safe-area aware

## Quick Start

### Docker (recommended)

```bash
cp env.example .env    # edit PORT if needed
docker compose up -d
```

Open `http://localhost:8080`.

### Without Docker

Any static file server works:

```bash
# Python
python -m http.server 8080

# Node
npx serve -p 8080

# Or just open index.html directly (YouTube won't work from file://)
```

## Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `PORT`   | `8080`  | Host port mapping |

Copy `env.example` to `.env` and adjust as needed.

## Deployment

The app is a single static file. Serve it from any web server, CDN, or hosting platform.

Behind **Cloudflare**: point your domain to the server, enable proxying. The 120KB file caches well at the edge. No server-side processing — all data stays in each user's browser.

## Limitations

- **YouTube on `file://`** — YouTube IFrame API requires `http://` or `https://`. Use a server.
- **YouTube background playback** — YouTube pauses when the tab/screen is not visible on mobile. This is a YouTube policy restriction.
- **iOS Safari** — no folder picking; file selection only. IndexedDB storage may be purged by the OS.

## Tech Stack

- Vanilla HTML/CSS/JS — no frameworks, no build tools
- IndexedDB for persistence
- Web Audio via `<audio>` element
- YouTube IFrame Player API
- Media Session API for lock-screen controls
- nginx:alpine Docker image for serving
