# To Valhalla

> I live, I die, I live again.

A browser-based multi-system emulator. Bring thine own cartridges. No server, no hosted ROMs, all blood kept in thy browser's vault.

Live at: `https://ride-eternal.github.io/to-vallhalla/`

## What this is

A static GitHub Pages site running [EmulatorJS](https://emulatorjs.org/) against ROMs you load from your own device. Files are stored in IndexedDB on your machine only — nothing uploaded anywhere.

## Supported steeds

Arcade (MAME / FBNeo), NES, SNES, N64, Game Boy / Color, GBA, DS, Sega Genesis, Master System, Game Gear, 32X, Sega CD, PlayStation (PSX), Atari 2600, Atari 7800, TurboGrafx-16.

## Files

| File | Purpose |
|---|---|
| `index.html` | The Garage — library + steed picker + ROM loader |
| `play.html` | The Rig — emulator runner |
| `robots.txt` | Tells search engines to skip the site |
| `.nojekyll` | Tells GitHub Pages to skip Jekyll processing |
| `README.md` | This file |

No build step. No package manager. Pure HTML/CSS/JS + EmulatorJS from CDN.

## Deploying

1. Push these files to the root of `ride-eternal/to-vallhalla` on the default branch (`main`).
2. **Settings → Pages → Deploy from a branch → main / (root) → Save**
3. Wait ~60 seconds. Visit `https://ride-eternal.github.io/to-vallhalla/`.

## Keeping it unlisted

GitHub Pages has no official "unlisted" state. Sites served from Pages are publicly reachable by URL regardless of whether the source repo is public or private. True private-with-auth Pages exists only on GitHub Enterprise Cloud. Practical options, in order of effort:

**1. Repo private (requires GitHub Pro or higher, ~$4/mo)**
Settings → General → Danger Zone → Change visibility → Make private. The code is hidden; the site URL still works. Free-tier accounts cannot publish Pages from a private repo.

**2. Discourage indexing (done — already in these files)**
Both HTML files include `<meta name="robots" content="noindex, nofollow">`. The `robots.txt` blocks all crawlers. Search engines generally won't index a site without inbound links anyway, but this makes it explicit.

**3. Don't link the URL anywhere**
Leave the GitHub repo description blank (or set it to something uninformative). Don't put the URL in your profile bio, other repo READMEs, or posts. The URL is deterministic (`username.github.io/reponame`) so anyone who guesses your username + repo name can find it. The repo name being unusual helps — `to-vallhalla` is better than `emulator` or `games`.

**4. Actual auth (if you want someone locked out, not just hidden)**
GitHub Pages can't do this on any plan below Enterprise Cloud. Alternatives:
- **Cloudflare Pages + Cloudflare Access** — redeploy the same files to Cloudflare Pages, attach Access with email OTP or an allowed-email list. Free tier covers this.
- **Vercel with password protection** — paid plan, one-click password gate.
- **Tailscale + any static server** — run something like `caddy` on a personal machine, expose via Tailscale. Only your tailnet devices can view.

For a personal arcade page, options 1–3 combined are usually enough.

## How ROM storage works

When you load a ROM, it's saved to IndexedDB under the `valhalla` database on your device. The ROM never leaves your browser. Rough quotas:

- Chrome / Edge desktop: typically ~60% of free disk
- Firefox: ~10% of disk
- Safari: ~1 GB, prompts for more

Clearing site data for this origin wipes the garage.

## BIOS

Some cores need BIOS on first launch. EmulatorJS will prompt:

- **PlayStation (PSX)**: SCPH-xxxx BIOS
- **Sega CD**: MegaCD BIOS
- **Nintendo DS**: firmware + BIOS

Supply your own, the same way you supply ROMs.

## Tekken 3 specifically

You asked about this in chat — worth repeating here. Tekken 3 arcade runs on Namco System 12, which the EmulatorJS arcade core (MAME 2003-Plus) does **not** support. The playable path is the **PlayStation port** — pick PlayStation from the steed menu and load the Tekken 3 BIN/CUE or CHD. Runs smoothly.

## Arcade romset note

EmulatorJS's arcade core is MAME 2003-Plus. Romsets from modern MAME builds often won't boot. If a ZIP doesn't load, you either need a 2003-Plus-compatible set or a game covered by FBNeo.

## Adding or changing systems

Two places to edit:

- `index.html`: the `SYSTEMS` array near the top of the `<script>` block
- `play.html`: the `SYS_MAP` object near the top of the `<script>` block

Both keyed by EmulatorJS core name. Full core list: https://emulatorjs.org/docs/systems

## Tech

- EmulatorJS stable channel from CDN
- Vanilla HTML / CSS / JS, zero dependencies
- IndexedDB for local ROM storage
- Static, client-side only

## Legal

This project hosts no ROMs and distributes no copyrighted software. What you load into your browser from your own device is entirely your affair.

---

*Oh what a day. What a lovely day.*
