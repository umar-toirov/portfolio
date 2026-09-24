# AGENTS.md

Guide for coding agents working on this portfolio site. Read it fully before editing.

## What this project is

The university-admissions portfolio of Muhammadumar Muhammadtoirov (public name Muhammadumar Toirov), a high-school student from Margilan, Uzbekistan interested in AI, computer science, education and research. It is a single static page, `index.html`, with two "eras":

1. **1996 desktop**: a retro OS called **UmarOS 95** with a boot screen, desktop icons, draggable/resizable windows, taskbar, Start menu, mini-apps (Minesweeper, Paint, Chat), screensaver, joke crash screen and a helper character, Disky.
2. **2026 site**: a modern dark one-page website (big type, lime accent, aurora glow, scroll reveals, case-study drawer, a light "paper" research section). Visitors reach it through an in-desktop "update" that plays a time-travel animation, or directly via the `#2026` URL hash.

The retro desktop is the hook; the 2026 site is the substance. The site must pass the "30-second test": a reader should quickly learn who he is, what he cares about, what he has built and researched, how it connects, and what's next.

The concept is inspired by robbyyeager.com. **All code, text and graphics here are original.** See "Hard rules".

## Hard rules

- **Do not copy from robbyyeager.com** or any other site: no source code, CSS, copy/text, images, logos or audio.
- **No third-party characters or trademarks.** The helper is an original floppy-disk character ("Disky"), drawn as inline SVG. Never Clippy or any other mascot. No Microsoft/Windows logos or product names; the OS is "UmarOS" (`ME.osName`).
- **Never fabricate.** No invented achievements, statistics, users, awards, dates, quotes or impact. If something is unverified, leave the field empty (render functions hide empty fields) and list it in the `CONTENT_TO_VERIFY` comment at the top of the script. No SAT score unless the owner supplies the final official one.
- **Voice:** a high-school student. "I built / I tested / I noticed / I'm exploring", not corporate or adult-professional. Avoid "passionate", "innovative", "revolutionary", "cutting-edge", "world-class". Aspirations are framed as aspirations.
- **Keep it a single self-contained file** unless the owner asks otherwise. No build step, no framework, no npm dependencies. Only external requests: Google Fonts (VT323, Pixelify Sans, Inter, Archivo).
- **Content lives in the `ME` config object only.** Exception: the static SEO tags in `<head>` (title, description, Open Graph, Twitter), because crawlers don't run JS. Keep them in sync with `ME`.
- **Escape all config text** with `esc()` (or `acc()`, which escapes and turns `*word*` into an accent) when interpolating into HTML.
- **Wrap browser storage** through `store.get` / `store.set`.
- Film references are banned in the warp: keep 142 MPH and 3.60 GW, captions "Spinning up the timeline…", gauges SPEED / POWER.

## File layout

```
portfolio/
├── index.html   # everything: CSS, HTML shell, JS
├── README.md    # public-facing project description
└── AGENTS.md    # this file
```

Optional assets the owner may add later: `resume.pdf` (set `ME.resumeUrl`) and project screenshots such as `img/habitzone.jpg` (set a project's `image`).

Inside `index.html`, in order (search for these names; line numbers drift):

| Part | What it holds |
|---|---|
| `<head>` | Static SEO tags, inline SVG favicon, Google Fonts. |
| `<style>` first half | Retro desktop styles: bevels `.out` / `.in` / `.btn`, windows `.win`, taskbar, Start menu, overlays, helper, Minesweeper, Paint, chat. Mobile breakpoint `max-width:700px`. Note: bare element rules here (`fieldset`, `p`, `h2`, `a`, `label`) are global, so reset them under `#modern` if a 2026 component uses those elements. |
| `<style>` after `UPDATE → 2026` | Update balloon, installer, `#warp`, and the 2026 site. **Every 2026 rule is scoped under `#modern`** (or `#mcase`, `#back96`, which live inside it). Breakpoint `max-width:860px`. |
| HTML body | Static shells: `#boot`, `#desk` with `#icons`, `#helper`, `#start`, `#taskbar`, overlays, `#balloon`, `#warp`, empty `#modern`. OS name text is filled in by JS from `ME.osName`. |
| `CONTENT_TO_VERIFY` comment | Owner TODO list of unverified facts and drafted reflections. Not rendered. |
| `ME` | **The content config** (see below). |
| helpers | `$`, `esc`, `acc`, `plain`, `mobile`, `store`, `EXT`, `LINKS`, `GH`, `CASE_FIELDS`. |
| `APPS` / `START` | Desktop window registry and Start menu items (`"-"` = separator). |
| `openApp`, `focusWin`, `closeWin`, `drag` | Window manager. |
| `INIT`, `openCase`, `initChat`, `initMines`, `initPaint`, `setWall` | Desktop app logic. |
| `system`, `startSaver`, `wake`, `helper`, `boot` | System actions, screensaver (90 s idle), Disky, boot. |
| `initUpdate`, `updateBalloon`, `timeTravel` | Update installer and warp. |
| `buildModern`, `scrollToSection`, `openMCase`, `closeMCase`, `enter2026`, `back96` | The 2026 site, built once from `ME` on first entry. |
| end of script | `boot` wrapped to show the update balloon; `#2026` hash skips to the modern site. |

## The `ME` object

| Field | Used for |
|---|---|
| `name`, `publicName`, `shortName`, `osName`, `role`, `seoTitle` | Identity, titles, OS branding. |
| `headline`, `lede`, `stage`, `location`, `glance` | 2026 hero and its "at a glance" strip. `*word*` in `headline` becomes lime. |
| `email`, `links`, `alsoOnWeb`, `resumeUrl` | Contact. Empty `email` → contact points to GitHub and the 1996 mail form is replaced by links. Empty link `url`s are filtered out. |
| `aboutTitle`, `aboutLead`, `about`, `now`, `goal`, `directions`, `directionNote`, `skills`, `academics` | About section, Notepad, resume. `skills` groups use honest levels ("Built with", "Explored"). |
| `principles` | "How I think" (3 items). |
| `projects` | Cards, case studies, Selected Work folder, chat bot. |
| `research` | Research section, RESEARCH.DOC window, scenario rater. |
| `journey`, `lab`, `fail`, `beyond`, `additional` | Timeline, Lab, "What didn't work", "Beyond the screen". |
| `site` | System Properties window (stack, why no framework, how it was made). |
| `helperTips`, `bin`, `wallpapers` | Disky tips (`{text, open, button}`), Recycle Bin, wallpapers. |

## How to do common tasks

**Change content:** edit `ME` only. Both eras read from it.

**Add a project:** append to `ME.projects` with a unique `id`, `icon` (1996 emoji), `mark` (short text shown large on the 2026 card), `title`, `tagline`, `status`, `year`, `role`, `tech[]`, `keys[]` (chat-bot keywords), `image`, `card: {problem, build, evidence}`, the case-study fields `problem, question, hypothesis, build, experiment, result, reflection, next`, and `links[]`. All are optional except `id`/`title`/`card`; empty ones are hidden. `anchor: "m-..."` makes the card scroll to a section instead of opening a drawer (used by the research card). The first project is the wide featured card.

**Add a desktop window/app:**
1. Add to `APPS`: `key: { icon, title, label?, w, h, desk?, render: () => "<html>" }`. `desk: true` adds a desktop icon. An entry with `url` instead of `render` opens that link in a new tab (used by GitHub).
2. `render` output usually starts with `.menubar` (optional) and a `.body` element (`.body.pad`, `.body.in`).
3. Behaviour goes in `INIT.key = el => {...}`. Query inside `el`, not `document`.
4. Add `["key", "icon", "Label"]` to `START` to list it in the Start menu.
5. Any element with `data-open="key"` opens that app. `data-jump="m-section"` on a 1996 element time-travels and lands on that 2026 section.

**Add a system action:** add the key to the list at the top of `openApp` and handle it in `system()`.

**Add a 2026 section:** add markup in the `main` template in `buildModern()`, with `id="m-something"` and a heading made by `sec()` (it adds the `id="m-something-h"` used by `aria-labelledby`). Add it to `NAV` if it belongs in the header. Anchors use `href="#m-..."`; a delegated handler scrolls the `#modern` container. Add class `rv` for scroll reveal. Styles go under `#modern` in the 2026 CSS block.

## Layering (z-index)

| z-index | Layer |
|---|---|
| 100+ | Desktop windows, raised on focus via `Z` |
| 4000 | Helper (Disky) |
| 5000 | Taskbar |
| 5500 | Update balloon |
| 6000 | Start menu |
| 8000 | `#shutdown`, `#bsod`, `#saver` |
| 9000 | `#modern`, with internal layers 0–60 |
| 9500 | `#warp` |
| 9999 | `#boot` |

## Behaviour details worth knowing

- **Mobile (≤700px):** windows full-screen, no drag/resize, icons open on one tap, Disky hidden. 2026 (≤860px): single-column layout and a Menu button for the nav.
- **Reduced motion:** no auto screensaver, warp skipped, no reveals or hero word animation, no drawer slide.
- **Keyboard:** Enter opens icons and menu items; arrow keys/Home/End move through the Start menu; Escape closes the Start menu, the focused window, the case drawer or the mobile menu. While the 2026 site is shown, the desktop is `inert`; while the drawer is open, the rest of `#modern` is `inert` and focus returns to the card on close.
- **Persistence (`store`):** `noWelcome`, `wall`, `era` (written, not used to auto-restore).
- **Easter eggs:** clicking the clock 7 times shows the joke crash screen; 90 s idle starts the starfield.
- **Research scenario rater** is local only: nothing is stored or sent. It shows the qualitative early pattern from `research.patternText`, never numbers.
- **Contact** uses `mailto:` only. A real form backend (e.g. Formspree) must be discussed with the owner first.

## Testing

There is no test suite. Before finishing any change:

1. **Syntax check:**
   ```bash
   node -e "const h=require('fs').readFileSync('index.html','utf8');new Function(h.split('<script>')[1].split('</script>')[0]);console.log('SYNTAX_OK')"
   ```
2. **Screenshot both eras** with headless Edge (save in a scratch folder, not the project):
   ```bash
   EDGE="/c/Program Files (x86)/Microsoft/Edge/Application/msedge.exe"
   "$EDGE" --headless=new --disable-gpu --hide-scrollbars --window-size=1400,900 --virtual-time-budget=12000 --screenshot="$TMP/1996.png" "file:///C:/Users/Muhammadumar/portfolio/index.html"
   "$EDGE" --headless=new --disable-gpu --hide-scrollbars --window-size=1400,900 --virtual-time-budget=5000  --screenshot="$TMP/2026.png" "file:///C:/Users/Muhammadumar/portfolio/index.html#2026"
   ```
3. **Pitfalls:**
   - Headless Edge won't render narrower than about 500px. For phone width, screenshot a scratch page containing `<iframe style="width:390px;height:844px">` pointing at the site.
   - `#modern` scrolls internally, so a tall window won't show lower sections. Make a scratch copy that injects a script (after load) to add `seen` to all `.rv` elements and set `#modern`'s `scrollTop`, plus `*{transition:none!important;animation:none!important}`. Insert it before the **last** `</body>`.
   - `--force-prefers-reduced-motion` tests reduced motion.
   - Never leave test injections in `index.html`.
4. Check 390×844, 768×1024, 1366×768 and 1440×900 when touching layout.

## Style conventions

- Plain ES2020+ JS, no modules, 2-space indent, template-literal rendering.
- Desktop UI uses bevel classes and the Tahoma/`--ui` stack; no modern styling on the 1996 side, no retro styling in `#modern`.
- Accessibility basics: buttons for clickable things, `aria-label` on icon-only buttons, Enter/Space on custom controls, visible focus.

## Open items / owner TODO

See the `CONTENT_TO_VERIFY` comment at the top of the script for the full list. The main ones: email, LinkedIn, resume PDF, exact dates, project roles and outcomes, research sample size and final results, screenshots, and review of drafted reflections. Hosting and domain are not set up; confirm with the owner before deploying anything.
