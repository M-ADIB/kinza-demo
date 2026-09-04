# Kinza demo

Client demo for Kinza (كينزا), a Saudi soft drink brand. Static site, no build step, no dependencies.
Three versions of the same content sit side by side so the client can pick one.

## Live and deploy

- Version 1, classic: https://m-adib.github.io/kinza-demo/
- Version 2, lifestyle: https://m-adib.github.io/kinza-demo/v2/
- Version 3, copy-led: https://m-adib.github.io/kinza-demo/v3/
- Version 4, visual-led: https://m-adib.github.io/kinza-demo/v4/
- GitHub Pages. Pushing to `main` deploys it. Commit straight to main, no pull requests.

## Files

- `index.html` is version 1. The whole page lives in that one file, styles and script included.
- `v2/index.html` is version 2, built the same way, reading its images from `../assets/`.
- `v3/index.html` is version 3, built from the client's Keynote brief (`~/Downloads/KINZA landing-page.key`) and then
  reworked to Adib's feedback: split hero (copy left, spinning can right), full-bleed statement bands in the Poppi
  style, two image rails where a tap flips a picture into its flavor pattern, the vertical reel, Saudi Made, links.
- `v4/index.html` is version 4, the visual-led option from the client's 2026-09-05 direction: can-flip hero with no
  copy, one product photo strip, pop-style statement section, tap-a-can flavor row, thin moving copy strips, one
  lifestyle strip. Every visual is a placeholder for an asset the client's team will supply (listed under Open).
- `assets/` holds the ten can renders as `can-<flavor>.png` with an `-ar.png` Arabic face for each, the two slim
  250 ml renders, the logo files, the Saudi Made mark, `assets/life/` for the Instagram stills, three client
  Instagram posters (`Instagram Kinzabev*.jpg`), the vertical reel `Kinzabev Video.mp4` (version 3) and
  `assets/group/` with four group product shots pulled from the client's Keynote (version 4 placeholders).
- `.claude/handoff.md` is the running session log. It is gitignored, so it stays on this machine only.

## Brand rules

- The only colours are blue `#314da0`, navy `#0b277a`, pink `#e8235a` and paper `#e9e7dc`. Two exceptions: the flavor
  rail in version 2, where each panel takes its own can's colour, and the version 3 hero, which cycles the can palette
  from the client's Pantone sheet (the `FL` array at the top of the v3 script) plus the flavor patterns on the flipped
  rail cards. Everything else in v3 is blue, navy and paper, and every heading is paper. Adib's rule after the first
  v3 round: one heading colour, no accent words, no colour blocks. Version 4 is the client's own "colourful,
  visual-led" brief, so its hero, pop section and flavor row use the Pantone palette on purpose.
- The brand name is never typed as text. The `.wm` class paints the logo image instead. In version 3 `.wm` is a CSS
  mask filled with `currentColor`, so the wordmark takes any colour.
- Headings: Anton, uppercase, `letter-spacing: .02em`, `line-height: 1.02` (Arabic: Cairo 900, line-height 1.28). Adib
  flagged tighter settings as broken, keep these.
- Cans animate on their own. No cursor interaction on them until a real 3D model exists, and no parallax on text.
- Fonts are Anton for display, Outfit for interface, Cairo for Arabic.
- One heading system per page. Version 1 uses `.sec-head`, versions 2 and 3 use `.eyebrow` above an `h2`.

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

- Client assets still to come for v4: hero can-flip video, animated pop typography video, group product
  photography, flavor patterns and graphics, tailor-made lifestyle photography. The client asked for white headings
  on v3; it uses paper `#e9e7dc`, a one-line change if they insist on pure white.

- Build a real 3D can from the label artwork the client sent. The flat version is rasterised at `.claude/label300-1.png`.
- Confirm with the client whether Kinza is a registered Saudi Made programme member. The pages show the official mark
  and claim nothing beyond it.
- The Instagram stills in `assets/life/` are 640 pixels wide, the largest the public profile serves. Ask the client for
  the originals before this goes anywhere real.
- The v3 full-bleed bands use the three Instagram posters and the reel poster as placeholders. Asked the client for
  four to six landscape lifestyle photos, 2400 px wide or more, with a can in frame, one per statement.
