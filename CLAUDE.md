# Kinza demo

Client demo for Kinza (كينزا), a Saudi soft drink brand. Static site, no build step, no dependencies.
Four versions of the same content sit side by side so the client can pick one. Only version 4 is live work.

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
- `v4/index.html` is version 4, the visual-led option. Rebuilt as one system on 2026-09-07, then rebuilt again the
  same evening to Marina's call and yoyoyo.ai. Order: hero, ticker, still-life band, ticker, pattern wall, ticker,
  typography, ticker, can strip, people, statement, footer.
  - Hero, no copy: one can turning through the ten flavors. Each flavor is a 7 s clip of Ahmad's 360 render laid on
    that flavor's own colour (`assets/spin/<flavor>.mp4`), masked so its edges feather into the ground. All clips
    share one phase clock, so the can keeps turning through each cut. The hero darkens to navy as it scrolls away.
  - Still-life band sits straight on both tickers with no white gap, figures 44svh.
  - Pattern wall: nine flavor patterns, 3 x 3, one screen, before the typography section.
  - Typography: the client's real brand lines, one at a time, sized to fit the chapter. Stand-in for their film.
  - Can strip: ten turntable stills at 9:16 on grey, no label row and no flavor names. Hover or tap fills the tile
    with the flavor pattern; the strip holds 5 s after a tap and shows the effect once on its own when it arrives.
  - People: three columns of 4:5 portraits sliding past each other in a 100svh window, two columns on a phone.
  - Statement: "The fastest growing Saudi beverage brand in the world", then a footer ending on a navy row of white
    social icons.
  Tokens and rules sit in the comment at the top of its style tag. Sharp corners everywhere, one 12 px gutter.
  Chapters fill the screen on desktop and take their content's height on a phone. Header is logo plus hamburger
  opening a full-screen navy menu.
- `assets/` holds the ten can renders as `can-<flavor>.png` with an `-ar.png` Arabic face for each (versions 1 to 3
  only now), the two slim 250 ml renders, the logo files, the Saudi Made mark, `assets/life/` for the Instagram
  stills, three client Instagram posters (`Instagram Kinzabev*.jpg`), the vertical reel `Kinzabev Video.mp4`
  (version 3) and `assets/group/` with the group product shots from the client's Keynote.
  Version 4 uses `assets/spin/<flavor>.mp4` (the turning can, 542 x 720, on the flavor's colour),
  `assets/can360/<flavor>-en.webp` and `-ar.webp` (480 x 800 stills with real transparency, the tiles and the
  reduced-motion hero), `assets/still/` (Marina's six still-life shots at 1400 px), `assets/pattern/` (nine flavor
  patterns: her seven plus diet cola and lemon zero cropped from the brand elements deck) and
  `assets/people-real/` (her twelve lifestyle shots, 900 x 1020).
  `assets/slim-ar/` holds her seven slim Arabic-face renders on grey, unused. `assets/people/` (the six other-brand
  mood references) is off git as of 2026-09-07; the files stay on this machine only.
- `.claude/handoff.md` is the running session log. It is gitignored, so it stays on this machine only.

## Brand rules

- Versions 1 to 3: the only colours are blue `#314da0`, navy `#0b277a`, pink `#e8235a` and paper `#e9e7dc`. Two
  exceptions: the flavor rail in version 2, where each panel takes its own can's colour, and the version 3 hero,
  which cycles the can palette from the client's Pantone sheet (the `FL` array at the top of the v3 script) plus the
  flavor patterns on the flipped rail cards. Everything else in v3 is blue, navy and paper, and every heading is
  paper. Adib's rule after the first v3 round: one heading colour, no accent words, no colour blocks.
- Version 4 is the client's own "colourful, visual-led" brief, so its hero, typography section, pattern wall and
  flavor tiles use the Pantone palette on purpose. Marina asked for pure white `#ffffff` section backgrounds with
  blue copy on 2026-09-07, so v4 has a `--white` token. Its navy is Reflex Blue `#001489`, the guideline's own
  primary, not the `#0b277a` the other versions use: Ahmad's renders sit on Reflex Blue and the old navy read wrong
  next to them. Its can tiles sit on `--grey #ededed`, the ground under Marina's own can renders, on her note.
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
and images that failed to load. `node .claude/scripts/verify.js <dir>` runs all five and writes the screenshots;
`node .claude/scripts/scrolltest.js` checks the can strip.

The dev server is `.claude/scripts/serve.py` on port 8791 (`.claude/launch.json`, entry `kinza-static`). Do not go
back to `python -m http.server`: it answers a Range request (a browser asking for one slice of a file) with the whole
file, so a browser cannot seek a video, and the hero clips silently refuse to line up on the same rotation. GitHub
Pages does answer ranges, so that bug appears only on the local server.

Headless Chromium decodes video far slower than real time, so it cannot confirm anything about playback speed or
timing. For that, launch Playwright with `headless: false`. The built-in browser pane pauses animation while hidden,
so it cannot confirm motion either.

## Open

- Two client films are still missing for v4 and both have a slot waiting in the page: the hero can-flip film (drop it
  into `.spin` as `<video class="spin__film">`) and the typography film (drop it into `#pop` as
  `<video class="pop__film">`). Marina asked for the sizes twice on 2026-09-06 and again on the call. Answer:
  1920 x 1080 and 1080 x 1920, MP4 H.264, no audio, seamless loop, under 8 MB each.
- Marina and a designer rework the still-life shots Monday morning: geometric still life in rectangles, some on
  coloured grounds. Swap the new files into `assets/still/` under the same names, at about 1400 px wide.
- Soda water has no flavor pattern. Asked Marina for it at 1262 x 1921, like the other nine. Until it lands, tapping
  the soda tile shows a drawn stand-in and the pattern wall runs on the other nine.
- Marina liked a colour on yoyoyo.ai "for the footer" on the 2026-09-07 call and it was not identifiable from the
  transcript; their footer is transparent over the page ground. The footer is white with a navy icon row until she
  names it.
- The Arabic for "Dare to try at your fullest" and "Spark of Brilliance" in the typography section is a first pass.
  Marina should type the wording she wants.
- Build a real 3D can from the label artwork the client sent. The flat version is rasterised at `.claude/label300-1.png`.
- Confirm with the client whether Kinza is a registered Saudi Made programme member. The pages show the official mark
  and claim nothing beyond it.
- The Instagram stills in `assets/life/` are 640 pixels wide, the largest the public profile serves. Ask the client for
  the originals before this goes anywhere real.
- The v3 full-bleed bands use the three Instagram posters and the reel poster as placeholders. Asked the client for
  four to six landscape lifestyle photos, 2400 px wide or more, with a can in frame, one per statement.
- The client asked for white headings on v3; it uses paper `#e9e7dc`, a one-line change if they insist.
