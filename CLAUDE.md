# Kinza

Static website with no build step or package dependencies. Read README.md for the current folder map.

V5 is the current client site. V1 to V4 are earlier options, and V6 is an experimental option. Preserve the existing page URLs when editing shared assets.

Website assets are grouped by purpose in assets/. Original briefs, client files, chat archives and reference material live in source-materials/ in the main local checkout. That folder is ignored by Git and must remain local.

Historical design notes are in docs/design-history.md. Their descriptions and paths reflect earlier versions, not the current folder layout.

GitHub Pages publishes main. Stage only the intended files and check affected versions in English and Arabic, at desktop and mobile widths, plus reduced motion. For asset moves, verify all media loads and file contents are unchanged. For video playback checks, use a headed browser.

Local tooling and session notes remain in .claude/. The range-capable preview server is .claude/scripts/serve.py.
