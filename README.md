# TV Tracker

A phone-first TV tracker. It's a static site (no server), and your data lives in your browser.

## What it does

**Lists**
- **Watching** and **To-watch** tabs. Add a show by searching TVmaze, then choose **Watching**, **Occasional** or **To-watch**.
- Open any show to see its seasons and episodes. Tap an episode to mark it watched, or mark a whole season / all aired episodes at once.
- Each Watching card shows how many episodes you're behind and when the next one airs.
- Sort by **Title**, **Most behind** or **Next airing**. **Favorites** (★) always sort to the top.

**Who's watching**
- Every show is **Together** (default) or **Just me**, set on the show's page. Each card is tagged.
- The **Together** and **Just me** chips are independent toggles. Both on shows everything; at least one must stay on.

**Hiding shows you aren't actively following** (Watching tab)
- **Occasional**: shows you follow loosely. Hidden unless the **Occasional** box is checked.
- **Paused**: shows you're behind on but not watching right now. Hidden unless the **Paused** box is checked. They are still tracked quietly: episodes and the behind count keep updating, and the Show updates pop-ups still fire, but they never appear in the NEW banner. Use the **Paused** chip (next to All / Behind / Caught up) to see every paused show on its own. Pause and Resume are manual.
- **Between seasons**: a show you're caught up on whose next episode is more than 30 days away, or has no date yet, is hidden automatically. It reappears about a month before the next episode airs, or as soon as you're behind. Check the **Between** box to see them all. Ended shows you're caught up on are hidden under this box too and tagged "Ended".
- Moving a show to To-watch clears its Occasional and Paused flags.

**Updates**
- Each time you open the app (or return to it), it refreshes episodes from TVmaze, skipping any show refreshed in the last 30 minutes. The ↻ button forces a refresh of every show. TVmaze caches for up to an hour.
- A new episode that has aired shows up as "behind", with a **NEW** badge and a banner.
- A **Show updates** pop-up appears, and stays until you dismiss it, when a show:
  - moves from Running / TBD to **Ended** (TVmaze doesn't distinguish cancelled from concluded), or
  - gets an **air date for a new season**.
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
- **Backup**: **Export** saves a JSON copy; **Import** restores it. Do this now and then.

## Good to know

- **Data is stored only in this browser on this device.** It doesn't sync between devices, and clearing site data erases it. Export backups.
- The app needs a connection to refresh. Without one it opens from its cache and shows what it last had.
- Return dates depend on TVmaze having listed the next season's date. Until it does, a caught-up show stays hidden as "between seasons".
- The app relies on TVmaze's status wording ("Running", "To Be Determined", "Ended").

## Data sources

- Episodes and show info: [TVmaze](https://www.tvmaze.com) (CC BY-SA).
- Streaming availability: JustWatch, via [TMDB](https://www.themoviedb.org). This product uses the TMDB API but is not endorsed or certified by TMDB.
