# Paul Titus — 3D Portfolio

An interactive, WebGL portfolio experience: a fully Three.js-rendered workspace that boots up like a 2000-era machine, lets the camera glide into a hand-modeled desk scene, and zooms into the CRT monitor — where an OS-style page presents my profile, education, projects, skills, and contact links.

This is a **content-signed fork of [henryjeff/portfolio-website](https://github.com/henryjeff/portfolio-website)** by Henry Heffernan (MIT licensed). The original 3D environment, camera choreography, shaders, audio and boot sequence are preserved; the personal content, page metadata, contact backend and the in-monitor OS page have been replaced with Paul Titus's information.

## Stack

- **Three.js + TypeScript** (bundler: webpack) — the 3D intro scene
- **React** — HUD: BIOS loading screen, mute / free-cam toggles, typed name overlay
- **Express + Nodemailer** — production server (`server/index.ts`) and `/api/send-email`
- **OS page** — dependency-free HTML/CSS/JS at [`static/os/index.html`](static/os/index.html), served at `os/index.html` in both dev and prod

## Getting started

```bash
# Install dependencies
npm i

# Run the local dev server
npm run dev
```

To build and serve production:

```bash
# Build into public/
npm run build

# Serve the build with express
npm start   # http://localhost:8080
```

The site is desktop-first (WebGL experience) and shows a warning on small screens, exactly like the original design.

## Customizing your content

| What | Where |
|---|---|
| Name / role typed over the 3D scene | `src/Application/UI/components/InfoOverlay.tsx` |
| BIOS boot text | `src/Application/UI/components/LoadingScreen.tsx` |
| OS page content (about, education, projects, skills, contact) | `static/os/index.html` |
| Profile picture | `static/os/assets/profile.jpg` — currently Paul's public GitHub avatar; replace the file with a personal square photo to swap it |
| Page metadata / social cards | `src/index.html` (set absolute `og:url` / `og:image` after deploying) |
| Contact form backend | `server/index.ts` (needs `FOLIO_EMAIL` + `FOLIO_PASSWORD` env vars; the OS page uses `mailto:` and profile links meanwhile) |
| Favicon set | `static/images/` (voxel computer icon, shared with the 3D scene) |

The camera stays interactive inside the monitor because the OS page mirrors the original's `postMessage` mousemove / keydown / keyup bridge (`MonitorScreen.ts` consumes those messages).

## Credits & license

- Original design & 3D scene: **Henry Heffernan** — [portfolio-website](https://github.com/henryjeff/portfolio-website), [portfolio-inner-site](https://github.com/henryjeff/portfolio-inner-site)
- [`LICENSE.md`](LICENSE.md) keeps Henry Heffernan's copyright notice, as the MIT license requires. All modifications here regard personal content and linking only.
