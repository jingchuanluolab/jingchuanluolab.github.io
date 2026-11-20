# Luo Lab website

Static website for the Luo Lab, Department of Cell Biology, Yale School of Medicine
(founded 2027).

**Live at <https://jingchuanluolab.github.io>** — deployed from `main` by GitHub Pages
on every push. A custom domain (`luolab.org`) is not attached yet; see `NEXT_STEPS.md`.

Built from the Claude Design canvas *"Luo Lab Website"*. Plain HTML + one CSS file —
**no build step, no dependencies, no framework.** Edit a file, commit, push; GitHub Pages
publishes it within a minute.

## Files

```
index.html           Home — full-bleed photo hero, intro paragraph, three buttons
research.html        Research  (anchors: #mechanism #function #diversity #engineering)
team.html            Team
publications.html    Publications
news.html            News & Fun
join.html            Join the lab  (reached from Team and Contact, not from the nav)
contact.html         Contact
404.html             Not-found page
assets/css/style.css The whole stylesheet — all colours and type live in :root at the top
assets/img/hero.jpg  Home-page hero photo (2000px wide, ~470 KB)
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
The design ships four options: `#000066` deep navy (current), `#1B5E4B` green,
`#7A1F2B` wine, `#2F3B52` slate. One line changes the header bar, every link, every
button and every accent rule on all seven pages.

**Replace the hero photo.** Drop a new image at `assets/img/hero.jpg` (landscape,
~2000px wide, under about 500 KB). Nothing else needs changing. The text sits at the
bottom centre over a soft dark gradient, so pick an image whose lower third is not
busy. To nudge which part of the photo stays visible, change `background-position`
on `.hero-photo` — `center 70%` means "70% of the way down".

**Add a news item.** Copy one `<article class="news-item">…</article>` block in
`news.html` and put it at the *top* of the list. Newest first.

**Add a paper.** Copy a `<div class="pub">…</div>` block in `publications.html`
and fill it in. Newest year first.

**Add a lab member.** Copy a `<div class="member">…</div>` block in `team.html`,
drop their photo in `assets/img/`, and point the `<img>` at it.

**Replace a figure placeholder.** Each grey dashed box is
`<div class="ph ph--tall">[FIGURE: …]</div>`. Swap it for:

```html
<figure class="fig">
  <img src="assets/img/locl-tl.png" alt="Describe the figure for screen readers">
  <figcaption>LOCL-TL labels organelle-proximal ribosomes in living cells.</figcaption>
</figure>
```

**Add a page.** Copy `contact.html`, change the content, and add the link to the
`<nav>` block in all eight files including `404.html` (the nav is duplicated per
page — that's the one cost of having no build step).

## Placeholders still to fill

Everything in `[SQUARE BRACKETS]` is a placeholder. Find them all with:

```bash
grep -rno '\[[A-Z][^]]*\]' *.html
```

See `CONTENT-TODO.md` for the checklist.

## Deployment

GitHub Pages, from the `main` branch of this repo. Push and it republishes — usually
under a minute, occasionally a few. No build step and no Actions workflow: GitHub
serves the files as they are, which is what the empty `.nojekyll` file guarantees.

```bash
git add -A
git commit -m "Update publications"
git push
```

### When you change the stylesheet

GitHub serves every file with `cache-control: max-age=600`, so a browser can keep
showing an old `style.css` for ten minutes even after a hard reload of the page.
To force it, bump the number in the `<link>` tag on every page:

```bash
sed -i 's/style\.css?v=[0-9]*/style.css?v=8/' *.html
```

The query string changes the URL, so no cache can match the old copy. Do this
whenever a CSS change needs to be visible immediately.

To check a deploy landed:

```bash
curl -sI https://jingchuanluolab.github.io | head -1
```
