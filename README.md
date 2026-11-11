# Luo Lab website

Static website for the Luo Lab, Department of Cell Biology, Yale University (founded 2027).

Built from the Claude Design canvas *"Luo Lab Website"*. Plain HTML + one CSS file —
**no build step, no dependencies, no framework.** Edit a file, commit, push; GitHub Pages
publishes it within a minute.

## Files

```
index.html           Home
research.html        Research  (anchors: #mechanism #function #diversity #engineering)
team.html            Team
publications.html    Publications
join.html            Join the lab
contact.html         Contact
404.html             Not-found page
assets/css/style.css The whole stylesheet — all colours and type live in :root at the top
assets/img/          Figures, portraits, favicon
assets/pdf/          PDFs of papers, if you want to host them
.nojekyll            Tells GitHub Pages to serve the files as-is
CNAME                Your custom domain (create this when you buy one)
```

## Preview locally

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>. No install needed — `http.server` ships with Python.

## Editing

**Change the colour scheme.** Edit `--accent` at the top of `assets/css/style.css`.
The design ships four options: `#0B3C6F` navy (current), `#1B5E4B` green,
`#7A1F2B` wine, `#2F3B52` slate. One line changes every page.

**Add a paper.** Copy a `<div class="pub">…</div>` block in `publications.html`
and fill it in. Newest year first.

**Add a lab member.** Copy a `<div class="member">…</div>` block in `team.html`,
drop their photo in `assets/img/`, and point the `<img>` at it.

**Replace a figure placeholder.** Each grey dashed box is
`<div class="ph ph--hero">[HERO FIGURE: …]</div>`. Swap it for:

```html
<figure class="fig">
  <img src="assets/img/locl-tl.png" alt="Describe the figure for screen readers">
  <figcaption>LOCL-TL labels organelle-proximal ribosomes in living cells.</figcaption>
</figure>
```

**Add a page.** Copy `contact.html`, change the content, and add the link to the
`<nav>` block in all six pages (the nav is duplicated per page — that's the one
cost of having no build step).

## Placeholders still to fill

Everything in `[SQUARE BRACKETS]` is a placeholder. Find them all with:

```bash
grep -rno '\[[A-Z][^]]*\]' *.html
```

See `CONTENT-TODO.md` for the checklist.

## Deployment

GitHub Pages, served from the `main` branch. See `NEXT_STEPS.md`.
