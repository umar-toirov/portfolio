# Muhammadumar Toirov · Portfolio

A personal portfolio built as two eras in one HTML file.

## What is this?

I'm a high-school student from Margilan, Uzbekistan. I build tools for learning and research how students use AI. This site is where that work lives.

It opens as **UmarOS 95**, a working desktop from 1996: windows you can drag and resize, a Start menu, Minesweeper, Paint, a chat bot and a floppy-disk helper called Disky. Install the "2026 update" and the same computer travels through time and becomes **UmarOS 2026**, a modern desktop in the style of today's computers. My photo and name sit in the middle of the right side, like the account picture on a sign-in screen, over a blue wallpaper made for the site (a chalkboard of what I think about is one click away in Settings). There's a taskbar, a Start menu, desktop icons and real windows: About Me, Files with all my projects and a Gallery of proof photos, my research as a PDF, Notes, Mail, a Terminal (try `help`), a Browser, Settings and Photos. The **Get to know me** button at the bottom left walks you through five steps: who I am, what I've built, what I research, how I think, and how to say hello.

In a hurry? Everything is also available as one scrolling page.

- Live site: https://umar-toirov.vercel.app (every visit starts in 1996)
- Share links: `/#2026` opens the desktop, `/#web` the web-page version

## Why 1996?

The retro desktop stands for experimentation and the history of personal computing: the curiosity that got me into programming. It's the hook. You can explore my projects, research and lab notes as files and windows.

## Why 2026?

The 2026 desktop is the substance: what I've built, what I'm researching, how I think, and where I want to go. It's organised as evidence, not a list of achievements. Every project shows the problem, what I built, and what happened.

## Design philosophy

**Evidence over claims.** No invented numbers, awards or users. Unverified details stay empty (and hidden) in the config until they're real. Work in progress is labelled as work in progress.

## Technical architecture

- **HTML, CSS, vanilla JavaScript, inline SVG.** No framework, no build step, no npm dependencies.
- **One file.** `index.html` holds the styles, the HTML shell and the scripts. The only external request is Google Fonts. The images in `img/` (my own photos, plus a wallpaper and a chalkboard made for the site) and my resume PDF sit next to it.
- **One content object.** Everything about me lives in the `ME` object at the top of the script. Both eras render from it, so one edit updates the desktop and the website.
- **Safe rendering.** All content passes through an `esc()` helper before it reaches the page.
- **Isolated eras.** 2026 styles are scoped under `#os26` (desktop) and `#modern` (web page), so the retro and modern visual languages never leak into each other.
- **Two views, one source.** The 2026 desktop windows and the web page are built by the same small render functions.

Why not React? This is a static, interactive single page. Plain JavaScript keeps it tiny, fast, easy to host anywhere and easy to read with View Source.

## Accessibility

- Keyboard support throughout: Tab, Enter, arrow keys and Escape work on icons, windows, menus, tabs, cards, the dock and search (Ctrl+K).
- Visible focus outlines, a skip link, labelled icon buttons and semantic sections.
- `prefers-reduced-motion` is respected: no time-travel animation, no window animations, no scroll reveals, no auto screensaver.
- Phone layout: windows go full screen, the dock stays at the bottom, and the web page has a menu button.

## Development

Open `index.html` in a browser. That's it.

Before committing, check the script parses:

```bash
node -e "const h=require('fs').readFileSync('index.html','utf8');new Function(h.split('<script>')[1].split('</script>')[0]);console.log('SYNTAX_OK')"
```

See `AGENTS.md` for the file layout, how to add content, and the testing checklist.

Built with AI coding assistants as collaborators. Given that my research is about honest and dishonest uses of AI, it felt right to say so.
