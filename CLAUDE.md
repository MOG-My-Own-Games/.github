# MOG organisation profile - Agent Guide

The organisation's profile README (`profile/README.md`) and the images it shows (`res/screenshots/`).

## Never commit or push without being directly asked

Do not run `git commit` or `git push` unless the user explicitly asks for that action in that turn.

## Retaking the screenshots

The README shows these files; keep the names, so the README needs no edit:

| File | What it shows |
| --- | --- |
| `client-game-list.png` | the client's library (1316x797) |
| `client-game-details.png` | the client's page of One Must Fall: 2097 (1316x797) |
| `server-game-list.png` | the web UI library (1403x807) |
| `server-game-overview.png` | a game with hero, logo, icon and videos, window 1403x1010 (Twinsen's LBA2) |
| `server-install.png` | the Install tab while an installer runs: an **animated PNG**, three frames |
| `server-proton.png` | Settings > Install defaults, scrolled to Proton / Wine builds |
| `server-scraper.png` | the scrape dialog (Return to Monkey Island) |
| `server-saves.png` | Files > Saves (see below: sample data) |

### Where to run it

The agent's sandbox cannot reach the user's real setup. Run the capture scripts on the host with
`flatpak-spawn --host env QT_QPA_PLATFORM=wayland python3 <script>`; the host has Python 3 with PySide6
(and Qt WebEngine) and the user's own client config (`~/.config/mog-client/config.json`: server address, user
and password) and library. Work in `~/.cache/mog-shots/` (the sandbox and the host both see it), put the PNGs
in `out/`, and delete the whole folder when finished, but only **after** the images have been copied into the
repo and any animation has been built (the frames are gone with it).

- **Client**: import `mog_client` from `~/gits/MOG/MOG-Client` (so uncommitted work shows), build `App()` and
  `MainWindow(app)`, call `app.refresh()`, wait until `len(win.covers) >= len(app.games)`, then
  `win.grab().save(...)`. Neutralise `win.saves.check_all` and `win.settle_steam` first: a screenshot must not
  sync saves or touch Steam. Do not capture Settings > Server (it shows the address and user).
- **Server**: `QWebEngineView` with an off-the-record `QWebEngineProfile`. **Keep the profile in a variable**: a
  temporary one is destroyed at once and the process segfaults (exit 139). Sign in by filling `#login-user` and
  `#login-pass` from the config and submitting `#login-form`, then drive the page with `location.hash`
  (`game/<id>`, `settings/install`), the tab buttons and the page's own JS functions. The server serves its
  own frontend, so a screenshot shows whatever the server currently runs.

### Rules

- **No sensitive data**: no machine name, no IP address or host, no user other than `admin`. After capturing,
  run `strings -n 4 file.png | grep -iE "<host>|<ip>|<machine name>"` for each file, and look at every image.
  Device names on the Saves panel are replaced in the DOM before the shot (use `desktop`). The noVNC status bar
  of the installer display says `Connected ... to <container id>:100` in the first moment: do not use frames
  that show it.
- **Read-only against the server**: never press Scrape (it rewrites the game's metadata and artwork). Build the
  scrape dialog from `GET /api/games/<id>/media/candidates` with `renderMediaChoices` instead, and open the
  modal without the POST.
- **Install shot**: it needs a real install. Use a small game with one installer (Jazz Jackrabbit Collection,
  id 15), click Install in the Install tab, capture frames every ~2 s while the display runs (about 30 s with
  Auto mode on), then `POST /api/games/<id>/install/cancel` and `DELETE /api/games/<id>/install` (the install
  cache) and check `GET /api/games/<id>/install` is 404. Build the APNG with Pillow from three frames (language
  dialog, installing, installed successfully), `duration=[2200, 2600, 3200]`, `loop=0`, and save it as
  `server-install.png`.
- **Saves shot**: the server may hold no saves. Then fill the panel through the page's `renderSavesPanel()` with
  sample versions of a device called `desktop` and say so to the user; never upload saves just for a picture.
- A game that has been removed from the server (check `GET /api/games`) cannot be shot: pick another with the
  same features (hero, logo, icon, videos) and tell the user.
- Write texts in English, without em-dashes.
