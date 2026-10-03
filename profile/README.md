<img src="../res/Mog-mascotte.png" height="300px">

# MOG - My Own Games

**Keep and comfortably reinstall the PC game library you're entitled to.**

Ownership of software you've paid for is getting harder to exercise: storefronts shut down, DRM servers go
dark, and a working installer from ten years ago can be genuinely difficult to get running again. MOG is a
self-hosted way to keep that problem solved once: point it at a folder of installers, and it will scan,
fetch metadata, and install any of them into a clean, isolated environment, on demand, the same way a
storefront client would.

MOG is for DRM-free games, games you own a legitimate copy of, and installers
you are otherwise entitled to run. It happens to be installer-format-agnostic (it drives whatever installer
technology a title uses, generically), but it does not seek out, catalog, or promote any particular source
of software.

## How it fits together

- **[MOG-Server](https://github.com/MOG-My-Own-Games/MOG-Server)** - the self-hosted piece. Scans your
  library folders, fetches metadata (IGDB, SteamGridDB), and runs installers server-side inside a sandboxed
  Wine/Proton environment with a VNC view, so you can install (or stream-install) a game without needing a
  Windows machine or doing it by hand on every client.
- **[MOG-Client](https://github.com/MOG-My-Own-Games/MOG-Client)** - We provide a simple GUi and CLI client that talks to a MOG-Server. Is available for Linux and Windows, however we encourage the developers to integrate MOG as a game provider in their related softwares.

## Where this came from

MOG began as a feature proposal for [RomM](https://github.com/rommapp/romm), a FOSS ROM manager, which
didn't take the feature into its own scope. MOG is a clean fork of that idea into its own project under its
own name - it shares no branding with RomM and isn't affiliated with it, though some server-side code is
adapted from RomM's AGPLv3-licensed source (credited in `NOTICE.md` in that repo, as the license requires).

## Getting started

See each repo's own README for setup (`docker compose up` for the server, `pip install` for the CLI).

## License

MOG-Server is AGPLv3. MOG-Client is GPLv3. See each repo for details.
