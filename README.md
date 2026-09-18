# KINETRIX LAUNCHER UPDATES

Official **release downloads** for the Kinetrix Launcher and the Kinetrix Client Minecraft mod (1.8.9).

> **Distribution only — no source code lives in this repository.**
> The source repositories are private. Everything the launcher auto-updater,
> the client-mod updater and the website download page need is published here
> as release assets.

## Latest downloads

| File | What it is |
|------|------------|
| `KinetrixLauncher-Setup-<version>.exe` | Full Windows installer for the Kinetrix Launcher (auto-updates itself + the client mod) |
| `kinetrix-<version>.jar` | Kinetrix Client mod jar — drop into `.minecraft/mods` (Forge 1.8.9) |
| `forge-1.8.9-11.15.1.2318-1.8.9-universal.jar` | Forge universal jar hosted for the launcher |
| `OptiFine_1.8.9_HD_U_M5.jar` | OptiFine hosted for the launcher |

## Direct links (always newest release)

- Launcher installer: `https://github.com/tombabu472-star/Kinetrix-Launcher-Updates/releases/latest/download/KinetrixLauncher-Setup-2.4.1.exe`
- Client mod: `https://github.com/tombabu472-star/Kinetrix-Launcher-Updates/releases/latest/download/kinetrix-2.9.11.jar`
- All releases: https://github.com/tombabu472-star/Kinetrix-Launcher-Updates/releases

## `latest.json` — the update manifest (IMPORTANT, release playbook)

`latest.json` in this repo is the **primary quota-free update source** for the
launcher's auto-updater and the client-mod updater (raw.githubusercontent.com
has no rate limit — the GitHub REST API is capped at 60 requests/hour per IP
and the `releases.atom` feed only lists the 10 newest entries, which is what
silently killed the auto-updater before).

**Every release (launcher OR client) MUST refresh `latest.json` in the same
push that mirrors the release assets here**, otherwise rate-limited installs
stop seeing the newest version:

```json
{
  "updated": "<ISO date>",
  "launcher": { "tag": "launcher-v<ver>", "version": "<ver>", "asset": "KinetrixLauncher-Setup-<ver>.exe",
                "size": <exact bytes>, "sha256": "<sha256 of the exe>", "notes": "<one-paragraph changelog>" },
  "client":   { "tag": "mod-v<ver>", "version": "<ver>", "asset": "kinetrix-<ver>.jar",
                "size": <exact bytes>, "sha256": "<sha256 of the jar>" }
}
```

- Only ever point an entry at a release that already EXISTS here.
- `size` must be the exact asset byte size and `sha256` the real digest —
  the launcher verifies both before installing anything.
- The launcher updater order: REST API (per_page=50, highest launcher release
  wins) → this manifest → atom-feed scrape. The client updater order:
  REST API (per_page=50, highest `kinetrix-*.jar` wins) → this manifest →
  atom-feed scrape.

## Website

https://kinetrixclient.vercel.app
