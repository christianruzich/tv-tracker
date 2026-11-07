# TV Tracker

A phone-first TV tracker. It's a static site (no server), and your data lives in your browser.

## What it does

**Lists**
- **Watching** and **To-watch** tabs. Add a show by searching TVmaze, then choose **Watching**, **Occasional** or **To-watch**.
- Open any show to see its seasons and episodes, newest first. Tap an episode to mark it watched, or mark a whole season / all aired episodes at once.
- On the Watching tab, a **TV-icon** button at the right of each show's card, vertically centered, marks its next unwatched aired episode as watched (tap it again for the one after). It disappears once you're caught up.
- **Skip a season** you don't plan to watch (a **Skip** button on each season, on shows in Watching). Skipped seasons are greyed out and labeled, never count as "behind", and are ignored by the TV-icon button and **Mark all aired watched**. **Unskip** brings them back. Skipping covers the whole season, including episodes that haven't aired yet.
- Each Watching card shows how many episodes you're behind and when the next one airs.
- One **Sort** dropdown above the list: **Title**, **Most behind** (Watching only), **Next airing** or **Most recent**. Each tab remembers its own choice. **Most recent** puts the newest additions first; a show moved between Watching and To-watch counts as added when you moved it. **Favorites** (★) always sort to the top. On the Watching tab, shows with a **NEW** episode go above everything else (favorites that are NEW first, then other NEW shows, then favorites, then the rest) until you open the show.

**Who's watching**
- Every show is **Together** (default) or **Just me**, set on the show's page. Each card is tagged.
- The **Together** and **Just me** chips are independent toggles. Both on shows everything; at least one must stay on.

**Hiding shows you aren't actively following** (Watching tab)
- Chips in the second row pick the view: **Active** (default), **Behind**, **Paused**, **Caught up** and **All**. The **+ Occasional** and **+ Between** chips below add those shows to Active, Behind and Caught up.
- **Active** hides three kinds of show: *Occasional* shows you follow loosely (tap **+ Occasional** to include them); *Paused* shows you're behind on but not watching right now; and *between seasons* shows (tap **+ Between** to include them).
- **All** lists every show on the Watching tab, whatever its flags. **Paused** lists only paused shows. Those two views ignore the + chips (they dim).
- Paused shows are still tracked quietly: episodes and the behind count keep updating and the Show updates pop-ups still fire, but they never appear in the NEW banner. Pause and Resume are manual.
- **Between seasons**: a show you're caught up on whose next episode is more than 10 days away, or has no date yet, is hidden automatically. It reappears 10 days before the next episode airs, or as soon as you're behind. Ended shows you're caught up on count here too and are tagged "Ended".
- Moving a show to To-watch clears its Occasional and Paused flags.

**Updates**
- Each time you open the app (or return to it), it refreshes episodes from TVmaze, skipping any show refreshed in the last 30 minutes. The ↻ button forces a refresh of every show. TVmaze caches for up to an hour.
- A new episode that has aired shows up as "behind", with a **NEW** badge and a banner.
- A **Show updates** pop-up appears, and stays until you dismiss it, when a show moves from Running / TBD to **Ended** (TVmaze doesn't distinguish cancelled from concluded).
- When a show on your **Watching** tab (including Occasional, Paused and between-seasons shows) gets an **air date for a new season**, a **New season dates** banner appears at the top of the Watching tab, e.g. "Severance S3, Jan 10". Tap a name to open the show. It stays until you tap **Dismiss** or the season premieres. It does not sync between devices, and shows on To-watch don't trigger it.
- A show's status of "To Be Determined" is displayed as **TBD** and treated like Running. On a show's page, if it's between seasons, the status line shows when it returns ("Returns Jan 10, 2027", or "Returns TBA").

**Streaming**
- By default each show lists its original network or streamer from TVmaze.
- With a free **TMDB API key** (Settings), shows list the US services that carry them (subscription, free and ad-supported; rent/buy are not counted).
- **My streaming services** (Settings, needs the key): tick the services you have. Cards and show pages then list only those. If a show isn't on any of your services, the card says "Not on your streaming services" and the show's page lists where it is available. With nothing ticked, every service is listed. The list is A–Z with your ticked services pinned at the top. Tap **Hide** on services you'll never use to remove them from the list (**Show hidden** brings them back). Ticked services can't be hidden.
- Streaming info refreshes at most every 14 days per show. **Refresh streaming** on a show's page forces it.

## Put it on GitHub Pages

1. Create a **public** repo (e.g. `tv-tracker`) and upload these files to the repo root (not inside a folder):
   `index.html`, `sw.js`, `manifest.webmanifest`, `icon.svg`, `icon-192.png`, `icon-512.png`
2. Repo **Settings → Pages**: Source = *Deploy from a branch*, Branch = `main`, folder = `/ (root)`, then Save.
3. After a minute or two, open `https://<your-username>.github.io/<repo-name>/` on your phone.
4. Add to Home Screen (Chrome: menu → Install app; Safari: Share → Add to Home Screen).

**Updating:** upload the new `index.html` over the old one (Add file → Upload files) and commit. Your data is stored under the same web address, so it carries over. If the old version still shows after the new one is live, close and reopen the app.

## Settings

- **TMDB key**: paste a free TMDB API key or read-access token, then **Save key & refresh streaming**. Get one by logging into your TMDB account, then Settings → API.
- **My streaming services**: see above.
- **Cloud sync (Google account)**: the real copy of your tracker lives in a Firebase Firestore database that only your Google account can read or write. The browser's storage is just a cache.
  - **Sign in with Google** in Settings. Changes upload a few seconds after you make them, and the app pulls in changes from other devices when you open it or return to it.
  - It syncs shows, watched episodes, flags (Together / Just me, Occasional, Paused, Favorite, skipped seasons), your TMDB key and your streaming-service choices. Episode lists are re-fetched from TVmaze.
  - **If the browser loses its data**, open the tracker, go to Settings, and sign in again. Everything comes back, including your TMDB key.
  - Per show, the most recent edit wins. Only your own changes count as edits, not TVmaze refreshes. Deleting a show on one device removes it on the others.
  - Setup is one-time, in the Firebase console (project, Google sign-in, Firestore, security rules); the config block is pasted into `index.html`.
- **Automatic cloud backup (GitHub Gist)**: keeps a private copy of your data on GitHub so a browser clearing its storage can't lose it. Create a classic GitHub token with only the **gist** scope (instructions are in Settings), paste it, and tap **Connect**. After that the app backs up a few seconds after each change. It never overwrites the backup with an empty tracker.
  - The backup holds your shows, watched episodes, flags and settings. It leaves out episode lists (re-fetched from TVmaze on restore), your TMDB key and the GitHub token.
  - It's a *secret* Gist: unlisted, but anyone with its exact link could read it.
  - **To recover** after the browser loses its data: open Settings, paste the token again, tap **Connect**. It finds the backup and restores it; episodes reload from TVmaze. Keep the token in a password manager. You'll also need to paste your TMDB key again.
  - Syncs one way, from this browser to the Gist. It doesn't merge edits made on two devices.
- **Backup file**: **Export** saves a JSON copy to your device (without the GitHub token); **Import** restores it.

## Good to know

- **Data is stored in this browser on this device.** Clearing site data erases it, so connect the cloud backup in Settings (or export backups). Without a backup, nothing else holds a copy.
- The app needs a connection to refresh. Without one it opens from its cache and shows what it last had.
- Return dates depend on TVmaze having listed the next season's date. Until it does, a caught-up show stays hidden as "between seasons".
- The app relies on TVmaze's status wording ("Running", "To Be Determined", "Ended").

## Data sources

- Episodes and show info: [TVmaze](https://www.tvmaze.com) (CC BY-SA).
- Streaming availability: JustWatch, via [TMDB](https://www.themoviedb.org). This product uses the TMDB API but is not endorsed or certified by TMDB.
