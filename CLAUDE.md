# Kinza demo

Client demo for Kinza (كينزا), a Saudi soft drink brand. Static site, no build step, no dependencies.
Two versions of the same content sit side by side so the client can pick one.

## Live and deploy

- Version 1, classic: https://m-adib.github.io/kinza-demo/
- Version 2, lifestyle: https://m-adib.github.io/kinza-demo/v2/
- GitHub Pages. Pushing to `main` deploys it. Commit straight to main, no pull requests.

## Files

- `index.html` is version 1. The whole page lives in that one file, styles and script included.
- `v2/index.html` is version 2, built the same way, reading its images from `../assets/`.
- `assets/` holds the ten can renders as `can-<flavor>.png` with an `-ar.png` Arabic face for each, the two slim
  250 ml renders, the logo files, the Saudi Made mark, and `assets/life/` for the Instagram stills.
- `.claude/handoff.md` is the running session log. It is gitignored, so it stays on this machine only.

## Brand rules

- The only colours are blue `#314da0`, navy `#0b277a`, pink `#e8235a` and paper `#e9e7dc`. One exception: the flavor
  rail in version 2, where each panel takes its own can's colour.
- The brand name is never typed as text. The `.wm` class paints the logo image instead.
- Cans animate on their own. No cursor interaction on them until a real 3D model exists, and no parallax on text.
- Fonts are Anton for display, Outfit for interface, Cairo for Arabic.
- One heading system per page. Version 1 uses `.sec-head`, version 2 uses `.eyebrow` above an `h2`.

## Languages

Both pages switch language in place rather than loading a second URL. A `T` dictionary in the script holds every
string, `?lang=ar` forces a language, and the choice is remembered in the browser. Arabic sets the page direction to
right-to-left and swaps every can image to its Arabic face.

## Verifying a change

There is no test suite. Check work with Playwright headless Chromium, borrowed from
`/Users/madibbaroudi/Desktop/Webcraftr/Products/shabab-dashboard (Tanafus)/node_modules/playwright`.

Run five passes every time: English desktop, Arabic desktop, English mobile, Arabic mobile, and reduced motion (the
setting where a visitor asks their operating system to cut animation). Look for console errors, horizontal overflow
and images that failed to load. The built-in browser pane pauses animation while hidden, so it cannot confirm motion.

The dev server config is `.claude/launch.json`, entry `kinza-static`, python http.server on port 8791.

## Open

- Build a real 3D can from the label artwork the client sent. The flat version is rasterised at `.claude/label300-1.png`.
- Confirm with the client whether Kinza is a registered Saudi Made programme member. The pages show the official mark
  and claim nothing beyond it.
- The Instagram stills in `assets/life/` are 640 pixels wide, the largest the public profile serves. Ask the client for
  the originals before this goes anywhere real.
