# Etch Gaming — Landing Page Handoff

Context for picking this up in Claude Code. Paste this whole file into the
chat when you start the session, or just point Claude Code at this folder.

## What this is

A single-page static site for **Etch Gaming**, Aaron's laser-cut tabletop
gaming accessories business (tokens, dice trays, deck boxes, custom
engraving), sold on Etsy: https://www.etsy.com/shop/EtchGaming

The file `index.html` in this folder is the finished, ready-to-deploy page.
No build step — it's plain HTML/CSS with Google Fonts loaded via CDN link
tags. No JS framework, no dependencies to install.

## Design direction

Styled to match Aaron's existing site **harlw.com** — an industrial
"specification sheet" / dossier aesthetic:

- Near-black background (`#0a0a0a`), off-white text (`#e9e6df`), orange
  accent `#FF5F1F` (same accent as harlw.com, for brand consistency)
- Monospace type (JetBrains Mono) for labels/data, Space Grotesk (bold) for
  display headlines
- Motifs: serial numbers, pulsing "STATUS: LASER_ONLINE" indicator, scrolling
  ticker marquees, spec-sheet data grids, file-reference rows for the product
  catalog, terminal-style contact panel
- Reference: fetch `https://harlw.com` to see the sibling site if design
  consistency needs double-checking later

## Outstanding items (not yet resolved)

1. **Contact email is a placeholder** — `hello@etchgaming.com` in the
   `#contact` section (`mailto:` link). Confirm Aaron's real contact email
   and swap it in.
2. **Product photos not yet integrated.** Project assets are available
   at `/mnt/project/` in the claude.ai environment (not present in this
   Claude Code session unless copied over):
   - `etchheader.jpg` — wide banner collage, includes ETCH logo mark centered
   - `header_02.jpg` — angled tabletop scene (cards, dice, tray, tokens)
   - `Asset_13x.png` — small asset (actually JPEG despite extension, verify
     before use)
   - `Etch_Gaming__Logo_WonB.png` — logo lockup (also actually JPEG)
   - `menu_beer.png` — likely irrelevant leftover asset from a different
     project, probably skip
   - **Known gotcha:** several of these `.png`-named files are actually JPEG
     format internally — check with `file <name>` before assuming format.
   - The current page uses an inline SVG redraw of the logo mark (circle +
     inverted triangle + laser sparks) rather than embedding the real photo
     assets, since the header images were too large/bulky to inline as
     base64 and there was no reliable way to host them at a public URL from
     the claude.ai chat environment. In Claude Code, this constraint doesn't
     apply — you can just copy the real files into an `/images` folder and
     reference them normally, or use a real `<img>` for the catalog section
     using `header_02.jpg` (the tabletop product shot) as a nice fit for the
     "Catalog" section, or as a hero background.

## Deployment (this is the main ask)

Aaron wants this live on Netlify. He has a Netlify account already connected
as an MCP connector in claude.ai, but that connector's tools couldn't push a
raw static file without a publicly-hosted URL to fetch from — which the chat
environment couldn't reliably provide. Claude Code doesn't have this
limitation since it has direct CLI access.

Suggested flow:

```bash
# from this folder
npm install -g netlify-cli   # if not already installed
netlify login                 # links to Aaron's Netlify account
netlify init                  # or: netlify link, if a site already exists
netlify deploy --prod         # ships index.html live
```

If Aaron already created a site via Netlify Drop (app.netlify.com/drop) in
the meantime, use `netlify link` to attach to that existing site rather than
creating a new one — check before assuming a fresh site is wanted.

## Notes / principles carried over

- The harlw.com aesthetic is Aaron's established design language and should
  be applied consistently to future projects tied to his personal brand.
- Large header images are too bulky to embed as base64 in artifacts; that
  constraint is specific to the claude.ai chat/artifact environment, not to
  Claude Code.
