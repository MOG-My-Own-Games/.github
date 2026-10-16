# Credits

MOG is made of two projects, MOG-Server and MOG-Client. This file lists what they use from others. Each project keeps its own license (`LICENSE`), and MOG-Server also has a `NOTICE.md` that marks the files adapted from RomM.

## Code adapted from other projects

- **RomM** (AGPL-3.0-or-later), https://github.com/rommapp/romm. Parts of the install sandbox, the database session code, the HowLongToBeat provider and the IceWM preferences in MOG-Server come from RomM. Each adapted file has a `# Adapted from RomM` header. Details in [MOG-Server/NOTICE.md](MOG-Server/NOTICE.md).

## Data and online services

- **Ludusavi manifest** (MIT), https://github.com/mtkennerly/ludusavi-manifest. MOG-Server downloads this YAML file to know where games keep their save files. It is not bundled with MOG; it is fetched at startup and cached locally. The Ludusavi program itself is not used.
- **SteamGridDB**, https://www.steamgriddb.com. Game artwork (covers, heroes, logos, icons).
- **IGDB** (by Twitch), https://www.igdb.com. Game metadata and artwork, used as the fallback to SteamGridDB.
- **HowLongToBeat**, https://howlongtobeat.com. Completion times.
- **GE-Proton** (GloriousEggroll), https://github.com/GloriousEggroll/proton-ge-custom. MOG-Client downloads it at runtime from its GitHub releases; it is not bundled.

## Bundled files

- **Proton (Proton-CachyOS build)**, in `MOG-Server/data/proton/cachyos-latest/`. Copyright (c) 2018-2022 Valve Corporation, under the BSD-3-Clause license included in that folder.
- **Kenney Interface Sounds**, https://kenney.nl/assets/interface-sounds. Menu sounds in MOG-Client. CC0 1.0.
- **Kenney Input Prompts 1.5**, https://kenney.nl/assets/input-prompts. Controller and keyboard icons in MOG-Client. CC0 1.0.

## Python libraries

MOG-Server:

| Library | License |
|---|---|
| FastAPI | MIT |
| Uvicorn | BSD-3-Clause |
| SQLAlchemy | MIT |
| Alembic | MIT |
| bcrypt | Apache-2.0 |
| HTTPX | BSD-3-Clause |
| aiohttp | Apache-2.0 AND MIT |
| PyYAML | MIT |
| Pillow | MIT-CMU (HPND) |
| python-dotenv | BSD-3-Clause |
| MCP Python SDK | MIT |
| pytest (dev only) | MIT |

MOG-Client:

| Library | License |
|---|---|
| PySide6 (Qt for Python) | LGPL-3.0 / GPL-2.0 / GPL-3.0 (Qt) |
| PyInstaller (build only) | GPL-2.0-or-later with a special exception for built programs |
| certifi (build only) | MPL-2.0 |
| HTTPX, Pillow, MCP, pytest (dev) | see above |

## System software in the MOG-Server Docker image

Installed from Debian packages (see `MOG-Server/docker/Dockerfile`). Each keeps its own license.

- Wine, the Windows compatibility layer for running installers (https://www.winehq.org)
- 7-Zip, official build, for archives and disc images (https://www.7-zip.org)
- Xvfb, x11vnc, websockify, noVNC: virtual display streamed to the browser (https://novnc.com)
- IceWM and picom: window manager and compositor for the installer display
- bubblewrap: sandbox for the installer process (https://github.com/containers/bubblewrap)
- Tesseract OCR: text recognition for the experimental automatic install mode (https://github.com/tesseract-ocr/tesseract)
- xdotool: presses buttons in installer windows
- GTK 2 and its engines: needed by GOG's Linux installers

## Tools MOG-Client calls on the user's machine

These are not bundled; MOG-Client uses them if they are installed: umu-launcher (`umu-run`), Faugus Launcher, Winetricks, Wine, Flatpak, Steam, and GIO from GNOME.

---

If you find a credit missing or wrong, please open an issue at https://github.com/MOG-My-Own-Games/MOG-Client/issues.
