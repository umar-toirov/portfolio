# Muhammadumar Toirov · Portfolio

A personal portfolio built as two eras in one HTML file.

## What is this?

I'm a high-school student from Margilan, Uzbekistan. I build tools for learning and research how students use AI. This site is where that work lives.

It opens as **UmarOS 95**, a working desktop from 1996: windows you can drag and resize, a Start menu, Minesweeper, Paint, a chat bot and a floppy-disk helper called Disky. Install the "2026 update" and the computer travels through time to a modern website.

Direct link to the modern version: `index.html#2026`.

## Why 1996?

The retro desktop stands for experimentation and the history of personal computing: the curiosity that got me into programming. It's the hook. You can explore my projects, research and lab notes as files and windows.

## Why 2026?

The modern site is the substance: what I've built, what I'm researching, how I think, and where I want to go. It's organised as evidence, not a list of achievements. Every project shows the problem, what I built, and what happened.

## Design philosophy

**Evidence over claims.** No invented numbers, awards or users. Unverified details stay empty (and hidden) in the config until they're real. Work in progress is labelled as work in progress.

## Technical architecture

- **HTML, CSS, vanilla JavaScript, inline SVG.** No framework, no build step, no npm dependencies.
- **One file.** `index.html` holds the styles, the HTML shell and the scripts. The only external request is Google Fonts.
- **One content object.** Everything about me lives in the `ME` object at the top of the script. Both eras render from it, so one edit updates the desktop and the website.
- **Safe rendering.** All content passes through an `esc()` helper before it reaches the page.
- **Isolated eras.** Every 2026 style is scoped under `#modern`, so the two visual languages never leak into each other.

Why not React? This is a static, interactive single page. Plain JavaScript keeps it tiny, fast, easy to host anywhere and easy to read with View Source.

## Accessibility

- Keyboard support throughout: Tab, Enter and Escape work on icons, windows, the Start menu (with arrow keys), cards and the case-study drawer.
- Visible focus outlines, a skip link, labelled icon buttons and semantic sections.
- `prefers-reduced-motion` is respected: no time-travel animation, no scroll reveals, no auto screensaver.
- Phone layout: windows go full screen, icons open with one tap, and the 2026 site has a menu button.

## Development

Open `index.html` in a browser. That's it.

Before committing, check the script parses:

```bash
node -e "const h=require('fs').readFileSync('index.html','utf8');new Function(h.split('<script>')[1].split('</script>')[0]);console.log('SYNTAX_OK')"
```

See `AGENTS.md` for the file layout, how to add content, and the testing checklist.

Built with AI coding assistants as collaborators. Given that my research is about honest and dishonest uses of AI, it felt right to say so.
