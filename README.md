![image Alt]([https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035501.png?raw=true))
![image Alt]([image URL](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035527.png?raw=true))
![image Alt]([image URL](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035549.png?raw=true))
![image Alt]([image URL](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035608.png?raw=true))
![image Alt]([image URL](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035631.png?raw=true))

1) Analyze Engine


Accepts a profile URL or a direct album URL, with automatic URL normalization (adds https:// and www.).
Scans profiles page by page until exhausted, with an optional max albums cap (All / 10 / 25 / 50).
Hidden scraper running in a real (invisible) Chromium window: reads the live, resolved DOM after actual rendering, so it captures lazy-loaded media regardless of attribute (data-src, data-original, …) and even CSS background images.
Auto-scrolls the page several times to trigger lazy loading, and auto-dismisses consent/age overlays if present.
A second regex extraction layer over the raw HTML catches URLs that only exist as plain strings, merged with DOM results and deduplicated.
Smart "More posts" exclusion: the boundary is located structurally in the DOM (not by URL substrings), so suggested-album media never leaks into the current album.
Album title and cover pulled from og:title / og:image meta tags.


2) Album List


Album cards show: thumbnail, title, URL, image count 🖼, video count 🎬, size 💾, and status (⏳ pending / ⟳ downloading / ✅ done / ❌ failed) with an in-card progress bar.
Hotlink-protection fix: the app injects a proper Referer + real-browser User-Agent on thumbnail requests so they render instead of silently 403-ing.
Toggle selection by click or checkbox, plus Select All / Deselect All.
Thumbnail size slider (60–512 px), applied live.
Album right-click menu: ⬇ Download this album only · 📦 Download as ZIP (downloads the album and packs it straight into one archive even if the global ZIP option is off — a one-off override that never deletes originals) · 📋 Copy URL · 🌐 Open in Browser.
✕ button on every card (opposite the thumbnail): removes the album from the download list only — nothing on disk is touched.
Expand arrow ▸/▾ per album (v0.8.1): toggles a panel under the card listing every file inside the album with its name and type icon (🖼/🎬). Files already on disk show a ✓ with their size and a 📂 button that reveals them in Explorer; albums whose media hasn't been analyzed yet show an explanatory hint.


3) Downloading


Downloads selected albums into per-album subfolders (filenames sanitized for Windows).
Concurrent downloads — a pool of 4 parallel connections per album; markedly faster on large albums while staying gentle on the server.
Automatic retry (up to 2 extra attempts with backoff) to ride out transient network blips.
Media-type filter: All / Images only / Videos only.
Skip existing: files already on disk are not re-downloaded (they're counted and still registered in the Files library).
Follows redirects (301/302), 60-second per-request timeout, partial files deleted on failure.
Accurate overall progress bar (computed over total files, not albums), with live counters: ✓ done / ✗ failed / ⏭ skipped / 💾 bytes.
Live log listing each file the moment it completes, with size; ⏹ Stop button.
Smart diagnostics when no media is found (private album? login required? region-locked?).


4) Queue


Add selected albums to an independent queue (deduplicated), with a live counter badge on the tab.
Remove single items or clear all; one button downloads the entire queue.


5) History


Log of every download session: title, file count, size, timestamp, and outcome (✅/❌).
Stats panel: sessions, total files, total size, successes.
Instant search over history (stats always reflect the full history) — via a compact, tidy corner field in the header next to the Clear button, expanding slightly on focus (v0.8.1).
📂 open the session's folder (files open in Explorer with the file itself selected), ✕ remove the entry from the app only, 🗑 clear all.
v0.8.1 fix: the open button used to fail silently because the Windows path was inlined into onclick, so backslashes were eaten as JS escape sequences — it now passes an index and reads the path from state, with a clear error message if the path no longer exists.


6) 📥 Files Library (new in v0.8)


A dedicated tab registering every downloaded (or skipped-as-existing) file: name, album, size, time, with a type icon (🎬 video / 🖼 image / 📦 archive / 📄 other) and a counter badge on the tab.
Instant search by file name or album name — using the same compact corner search field as History (v0.8.1).
📂 Open File Location: opens Explorer with the file itself selected; shows a warning if the file no longer exists on disk.
🗜 Compress to ZIP: compresses that ONE file into filename.zip next to it (auto-numbered if the name is taken). The original file is untouched, and the resulting ZIP is added to the library automatically.
✕ Remove from App: removes the entry from the app's list only — the file stays on disk — with a permanent explanatory note at the top of the tab.
Full right-click menu: Open File Location · Compress to ZIP · 📋 Copy Path · Remove from App.
Re-downloading a file updates its entry instead of duplicating it; capped at 1,000 entries for performance.


7) 💾 Automatic Session Persistence (new in v0.8)


Everything is saved automatically and restored on relaunch: history, files library, queue, analyzed albums (including their media URLs, so no re-analysis is needed), theme, language, save folder, media type, max albums, skip-existing, ZIP options, proxy settings, and thumbnail size.
Saves are debounced: rapid changes during a download collapse into a single disk write instead of hundreds.
Atomic writes: state is written to a temp file then renamed, so a crash mid-save can never corrupt the session file.
A transient "downloading" status is never persisted — it comes back as "pending" on next launch.


8) Archiving (ZIP)


Create ZIP after download bundles the session's albums into one timestamped archive.
Hand-written streaming ZIP engine: never loads a whole file into memory (256 KB chunks) — no crashes on huge videos; STORED mode since media is already compressed.
Delete originals after zipping with strict safety rails: nothing is deleted until the ZIP is verified to exist and be non-empty; only this session's album folders are removed (never the base save folder itself), with an extra path check that refuses anything suspicious.
Turning ZIP off automatically turns off the dependent delete option so it can never stay silently active.


9) Clipboard


Auto-detects site links in the clipboard on launch and whenever the window regains focus, showing a "📋 Link detected — click to use" hint bar that starts analysis in one click.


10) 🔒 App Lock (new in v0.8.1)


New Settings section: a "Lock app on startup" toggle with a PIN field (4+ characters) and a Save button.
Every time the app opens, a full-screen lock overlay (in the user's own theme) covers everything and can only be passed with the correct PIN — with a shake animation on wrong input and Enter-key support.
Disabling the lock requires entering the current PIN first — it can't be switched off with a single click.
Storage safety: the PIN itself is never stored — only its SHA-256 hash inside the session file.


11) UI & Customization


15 full themes (Light, Dark, Midnight, Dark Black, Carbon, Metal, Wood, Pink, Purple, Blue, Forest, Rose Gold, Red, Green, Teal) with live mini-previews per theme and instant application via CSS variables.
9 languages: English, Arabic (full RTL layout), French, German, Spanish, Chinese, Japanese, Italian, Russian — covering all buttons, menus, right-click menus, and status messages.
Frameless custom window: drag from the top bar, custom minimize/maximize/close buttons, bottom status bar (state, album count, queue count, version).
Analysis spinner overlay and helpful empty states on every tab.


12) Extra Settings


Proxy: enable/disable, proxy URL, proxy type.
Update checker against GitHub, showing the new version when available.
Save-folder selection via native dialog or direct typing.
