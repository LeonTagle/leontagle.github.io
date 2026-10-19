# Personal website: context

Notes for maintaining this site. Last updated 2026-10-19.

## What this is

A single-page academic website for León Tagle Le Blanc: name on top, short bio
on the left, photo on the right. Under the bio come a CV line, a contact line
and two lists of work ("Works in Progress", "Other Writings"). The layout
follows the minimal one-card style common on economists' personal pages.

The page is one static file, `index.html`, with no build step. It is meant to
be hosted on GitHub Pages at `https://leontagle.github.io/`.

## Files

| Path | What it is |
|---|---|
| `index.html` | The page |
| `picture/profile-web.jpg` | 4:5, 960×1200 photo (the page trims the top in CSS, see Design) |
| `picture/profile.jpg` | Full-resolution original photo, kept locally; in `.gitignore`, so not published |
| `cv/CV.pdf` | CV, linked from the bio |
| `slides/flyouts.pdf` | Slides, "The Effects of Initial Placement" (with Caleb Brobst) |
| `slides/spillovers.pdf` | Slides, "Does Worker Mobility Mediate Knowledge Spillovers?" |
| `CONTEXT.md` | This file |
| `.gitignore` | Keeps `.DS_Store` and `picture/profile.jpg` out of the repository |

Every file in this folder is public once pushed, at the same path after the
domain. Paths are case-sensitive (`cv/CV.pdf`). Anything that should not be
public must stay out of the folder, or be listed in `.gitignore`, before it is
committed: removing a file later does not remove it from the repository
history.

## Page content

- **Bio.** Predoctoral research fellow at the Stanford Institute for Economic
  Policy Research (SIEPR), working with Professor José Ignacio Cuesta (linked to
  his site).
- **Interests and degrees.** Industrial organization and labor economics, with
  a focus on the empirics of technological change, growth and industry
  dynamics. B.A. and M.A. in Economics, Pontificia Universidad Católica de
  Chile.
- **CV line**, its own paragraph.
- **Contact line**, its own paragraph: the Stanford address written out as
  "[*at*]" and "[*dot*]", plain text rather than a link, in the dark gray
  `--soft`.
- **Works in Progress:** Initial Placement (with Caleb Brobst, linked to his
  SIEPR page; `[slides]`) and Worker Mobility (`[slides]`).
- **Other Writings:** the M.A. thesis, with `[updated version]` and `[original]`
  (`https://repositorio.uc.cl/handle/11534/89611`). `[updated version]` is a
  placeholder: link-coloured (`.placeholder`) but not a link, until the updated
  thesis PDF is added.
- **Abstracts.** Each work has an "Abstract" dropdown as its third row.

## To do

- Add the updated thesis PDF (e.g. in a new `papers/` folder) and turn the
  `[updated version]` placeholder into a link.
- Accessibility: the "*second*" link sits inside the nameplate SVG, which is
  `aria-hidden`, so screen readers skip it while keyboard focus can still land
  on it.

## Publishing

- GitHub Pages from a public repository named `leontagle.github.io` (all
  lowercase), branch `main`, served from the repository root.
- `.gitignore` already excludes `.DS_Store` and the full-resolution photo.
- Updating the site: edit, commit, push. The live page updates within a minute
  or two.
- A custom domain can be attached later with a `CNAME` file and DNS records,
  without changing any other file.

## Design

- **Fonts** (Google Fonts): name in Frank Ruhl Libre 900 (was Crimson Pro 900), body in Source Serif 4,
  labels under the name in Instrument Sans (regular and true italic), section
  headings in Inter 500.
- **Colours:** links `#2f6b3a`; dark gray `--soft` `#5c5c57` for section
  headings, the second row of each work, the "Abstract" label and the email;
  annotation gray `--annot` `#c9c9c9`.
- **Annotation gray history:** `#c6c6c6` → `#d2d2d2` (too light) → `#cccccc` →
  `#c9c9c9` (current). Adjust in small steps.
- **Layout:** two columns on desktop (text, 285px photo), one column under
  680px with the photo first at 228px.
- **Photo:** the frame is `aspect-ratio: 4 / 4.7` with `object-position:
  bottom`, which trims 6% off the top of the 4:5 file.
- **Section headings:** 13px uppercase, with a rule above and 14px of space
  below.
- **Each work is three rows:** title in bold (600) at 15.5px, plain text and
  not a link; second row at 15.5px in `--soft` with the coauthor ("with",
  lowercase) and links as bracketed buttons such as `[slides]`; third row an
  "Abstract" `<details>` dropdown whose text is 14.5px and indented 16px to
  line up with the word "Abstract".

### The nameplate

The name is an inline SVG inside the `<h1>`, with a visually hidden text copy
for screen readers. Braces under each part of the name are labelled "first
name", "family name" and "*second* family name :O", and an arrow points to the
gap between the first and family names, labelled "no middle name ;)".

- Everything is in viewBox units; the name is 88 units tall at baseline `y=96`.
- Word widths were measured in the browser for Frank Ruhl Libre 900 at 88 units
  and are locked with `textLength`: León 204, Tagle 222, Le Blanc 347.5. (For
  Crimson Pro they were 193, 214.5, 331; keeping those with a wider font
  squeezes the letters.) If the
  font or size changes, re-measure with `getComputedTextLength()`.
- Horizontal layout: 20 side margin, **52** between León and Tagle, **32**
  between Tagle and Le Blanc. viewBox width is 897.5.
- Braces are clean geometric paths, not hand-drawn: top at `y=116`, corner
  radius 11 wide by 9 tall. The middle brace is 24 wide with radius 5.5.
- Labels sit at `y=154` at 17 units, about 12.7px on screen at desktop width.
  Under 680px the unit size grows smoothly with a `clamp()` (17 up to 28 units
  at 375px, with a matching downward shift), so the labels stay at roughly
  12.5px and ease to 11px on a phone.
- "*second*" links to `https://en.wikipedia.org/wiki/Spanish_naming_customs`.
  It keeps the annotation gray and underlines on hover.
- The SVG's `max-width` (669px) is tied to the viewBox width so the name stays
  the same size when spacing changes: `max-width ≈ 0.7455 × viewBox width`.

Spacing tried so far (León–Tagle gap / Tagle–Le Blanc gap): 78 / 40 too loose;
50 / 30 too tight; 64 / 35 and 57 / 32 still slightly loose; 52 / 32 current.

## Previewing

Serve the folder locally and open `http://localhost:8791`:

```bash
python3 -m http.server 8791 --bind 127.0.0.1
```

Run it from this folder. Opening `index.html` straight from disk also works in
most browsers.
