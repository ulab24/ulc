# ulc fonts

Two font families, drawn by ulab24 from scratch. Releases tagged `fonts-X.Y` carry them as a zip (`ulc-fonts-X.Y.zip`) with `otf/`, `ttf/`, `web/` (woff2), `licenses/` and `INSTALL.txt`.

**ulc Hand**: a handwriting font for notes and sketches, Regular and Bold, Latin-1 and common punctuation.

**ulc Mono**: a coding font.
- 8 weights, Thin to ExtraBold, each with an italic (italic is a slanted version of the upright design).
- **ulc Mono NL**: the same without ligatures.
- Wide coverage: Latin including Vietnamese, Greek, Cyrillic, maths, arrows and shapes, APL, control pictures, box drawing, block elements, braille, and 41 icons for terminals and status lines (private-use block U+F8000 and up).
- About 135 programming ligatures (arrows, comparisons, `//`, `/*`, `<!--` and more). Each is drawn across the cells it replaces, so text stays on its grid. Turn them off with `font-variant-ligatures: none` or the OpenType `calt` setting, or use ulc Mono NL.
- Features: dotted and plain zero (`zero`, `ss01`, `ss02`), `case`, superscripts and subscripts, fractions, ordinals, accents on any letter.
- Exact cell edges: every glyph is 600/1000 em wide, the line is 1.3 em, and box drawing and blocks fill the whole line, so frames and bars join without gaps. Leave your terminal's line-height adjustment at 0.

**Nerd Font builds** (`ulc-fonts-nerd-*-X.Y.zip`, when attached to a release): ulc Mono patched with the Nerd Fonts icon sets, in the usual three variants: Nerd Font, Nerd Font Mono (icons fit one cell; pick this for terminals) and Nerd Font Propo. The icons keep their own licences ([notice](licenses/nerd-fonts-icons-NOTICE.txt)).

## Install

macOS: open an `.otf` and click Install Font. Linux: copy `otf/*.otf` to `~/.local/share/fonts/` and run `fc-cache -f`. Windows: right-click a `.ttf` and choose Install. Web: use the `.woff2` files, only to display your own pages (see the licence).

In a terminal, set the font to `ulc Mono` (or `ulc Mono NL`). Pick a weight by its family name, for example `ulc Mono Light` or `ulc Mono SemiBold`.

## Check the download

Same as the library: `gpg --verify checksums.txt.asc checksums.txt` with [ulab24-release-key.asc](ulab24-release-key.asc), then `sha256sum -c checksums.txt`.

## Licence

[ulab24 Font Licence 1.0](licenses/ulab24-Font-Licence-1.0.txt): you may install and use the fonts for personal and commercial work and publish what you make with them. You may not resell, share the font files, modify them, or ship them inside an app you distribute without written permission.
