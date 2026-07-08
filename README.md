![image Alt]([https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035501.png?raw=true](https://github.com/gigative/GigativeEromeDownloader/blob/main/Logo_transparent.png?raw=true))


![image Alt](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035501.png?raw=true)
![image Alt](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035527.png?raw=true)
![image Alt](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035549.png?raw=true)
![image Alt](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035608.png?raw=true)
![image Alt](https://github.com/gigative/GigativeEromeDownloader/blob/main/Screenshot%202026-07-08%20035631.png?raw=true)

<div align="center">
Gigative Erome Downloader

A fast, themeable desktop downloader for Erome profiles and albums — built with Electron.

Windows x64 · Electron 33 · 9 languages · 15 themes

github.com/gigative/GigativeEromeDownloader

</div>

✨ Features 



🔍 Smart Analyze Engine 

Accepts either a profile URL or a direct album URL, with automatic normalization (adds https:// and www.).
Scans profiles page by page until exhausted, with an optional cap on the number of albums (All / 10 / 25 / 50).
A hidden scraper runs inside a real, invisible Chromium window and reads the live, resolved DOM after actual rendering — so it captures lazy-loaded media regardless of the attribute used (data-src, data-original, …) and even CSS background images.
Auto-scrolls to trigger lazy loading and auto-dismisses consent / age-gate overlays.
A second regex layer over the raw HTML catches URLs that exist only as plain strings, merged and deduplicated with the DOM results.
Smart "More posts" exclusion — the boundary is found structurally in the DOM, so suggested-album media never leaks into the current album.






📥 Powerful Downloading 


Downloads selected albums into per-album subfolders with Windows-safe filenames.
Concurrent downloads — a pool of 4 parallel connections per album for markedly faster large albums.
Automatic retry (up to 2 extra attempts with backoff) to ride out transient network blips.
Media-type filter: All / Images only / Videos only.
Skip existing — files already on disk aren't re-downloaded.
Follows redirects, per-request timeout, and partial files are cleaned up on failure.
Accurate progress bar (computed over total files, not albums) with live done / failed / skipped / bytes counters, a live log, and a Stop button.







🗂 Album Management 


Rich album cards: thumbnail, title, URL, image/video counts, size, live status, and an in-card progress bar.
Hotlink-protection fix injects a proper Referer + real-browser User-Agent so thumbnails actually render.
Select All / Deselect All, plus a live thumbnail size slider (60–512 px).
Right-click menu: ⬇ Download this album · 📦 Download as ZIP · 📋 Copy URL · 🌐 Open in Browser.
✕ button on each card removes an album from the list (nothing on disk is touched).
Expand arrow ▸/▾ on each album opens a panel listing every file inside it; files already on disk show a ✓ with their size and a 📂 button to reveal them in Explorer.







📋 Queue

Add selected albums to an independent, deduplicated queue with a live counter badge.
Remove single items, clear all, or download the whole queue in one click.





📜 History 

A log of every download session: title, file count, size, timestamp, and outcome.
Stats panel (sessions · files · total size · successes) and an instant compact search.
Open the session folder, remove a single entry from the app, or clear all.




📁 Files Library 

A per-file registry of everything downloaded: name, album, size, time, and a type icon.
Instant search by file name or album.
📂 Open File Location — reveals the file in Explorer, selected.
🗜 Compress to ZIP — zips a single file next to itself; the original stays intact.
✕ Remove from App — removes only the app entry; the file stays on your disk.
Full right-click menu, with re-downloads updating entries instead of duplicating them.





💾 Automatic Session Persistence 

Everything is saved automatically and restored on relaunch: history, files library, queue, analyzed albums (including media URLs — no re-analysis needed), theme, language, save folder, and all settings.
Writes are debounced and atomic (temp file + rename), so a crash mid-save can never corrupt the session.





📦 Archiving (ZIP) 

Optionally bundle a session's albums into one timestamped archive.
A hand-written streaming ZIP engine never loads a whole file into memory (256 KB chunks) — no crashes on huge videos.
Optional delete originals after zipping with strict safety rails: nothing is removed until the ZIP is verified, and only that session's album folders are ever touched.




🔒 App Lock 

Optional PIN lock shown on a full-screen overlay every time the app opens.
Disabling requires the current PIN; only the PIN's SHA-256 hash is stored — never the PIN itself.





🔄 Automatic Updates 

Checks GitHub Releases in the background, downloads updates automatically, and installs on the next quit.
Live status in the About tab and a one-click restart & install when an update is ready.





📋 Clipboard Auto-Detect 

Detects site links in the clipboard on launch and on window focus, offering one-click analysis.





🎨 Interface & Customization 

15 full themes (Light, Dark, Midnight, Dark Black, Carbon, Metal, Wood, Pink, Purple, Blue, Forest, Rose Gold, Red, Green, Teal) with live mini-previews.
9 languages: English, Arabic (full RTL), French, German, Spanish, Chinese, Japanese, Italian, Russian.
Frameless custom window with drag, custom controls, and a status bar.
Native folder picker, optional proxy (HTTP / SOCKS5 / SOCKS4), and helpful empty states throughout.





🖥 Requirements


Windows 10 / 11 (x64)
No dependencies for end users — the installer bundles everything.





📦 Installation

Download the latest installer or portable build from the Releases page.

Default install location:

C:\Program Files (x86)\Gigative\Gigative Erome Downloader


🛠 Build from source

npm install
npm start          # run in dev
npm run build      # build Windows installer + portable


<div align="center">
GIGATIVE ING · github.com/gigative/GigativeEromeDownloader

</div>
