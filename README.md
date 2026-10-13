# TV Tracker

A phone-first TV tracker. Static site, no server. Data is stored in your browser.

- Two lists: **Watching** and **To-watch**
- Per-episode watched tracking; filter Watching by **Behind** / **Caught up**
- Shows where each show streams
- Refreshes episodes from TVmaze every time you open the app; a new episode shows up as "behind" the moment it airs, flagged NEW

## Deploy on GitHub Pages

1. Create a repo (e.g. `tv-tracker`) and upload all files in this folder to the repo root:
   `index.html`, `sw.js`, `manifest.webmanifest`, `icon.svg`, `icon-192.png`, `icon-512.png`
2. Repo **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main`, folder = `/ (root)`.
3. Open `https://<your-username>.github.io/tv-tracker/` on your phone.
4. Add to Home Screen (Safari: Share → Add to Home Screen; Chrome: menu → Install app).

## Streaming services

Out of the box the app shows a show's original network/streamer from TVmaze.
For current US streaming services, add a free TMDB API key in Settings (data via JustWatch, attribution required and included).

## Backup

Settings → Export saves a JSON copy; Import restores it. Browsers can clear site storage, so export occasionally.

## Data sources

Episodes: TVmaze (CC BY-SA). Streaming: JustWatch via TMDB.
