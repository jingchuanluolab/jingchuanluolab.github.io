# Content checklist

Every item below is a `[PLACEHOLDER]` in the HTML. Delete a line when it's done.
Find them all at any time: `grep -rno '\[[A-Z][^]]*\]' *.html`

## Blocking — nothing else should go live without these

- [ ] `[EMAIL]` — lab contact address. 22 occurrences: the footer of all 7 pages, plus
      team.html, join.html (×3), contact.html. One find-and-replace:
      `sed -i 's/\[EMAIL\]/you@yale.edu/g' *.html`
- [x] ~~`[FIRST NAME] Luo, PhD`~~ — now "Jingchuan Luo, PhD" (correct it if that is wrong)
- [ ] `[TITLE]` — team.html, e.g. "Assistant Professor"
- [x] ~~`Luo [INITIALS]`~~ — now "Luo J" in publications.html

## Home (index.html)

- [ ] **Photo credit for `assets/img/hero.jpg`.** The image comes from Yale's own
      communications photo library, so the right to use it on a Yale-affiliated site
      is not in question. What is still needed is the exact credit line they want,
      in writing, and confirmation that it carries over to `luolab.org` when the
      domain moves. Keep that email.
- [ ] Re-read the headline and the intro paragraph once in context — they are the only
      prose on the page and they're carrying the whole first impression.

## Research (research.html)

- [x] ~~`[FIGURE: mRNA targeting to mitochondria without an MTS]`~~ — now the lab
      vision diagram (`assets/img/lab-vision.jpg`). Reword the caption if you want.
- [x] ~~`[FIGURE: LOCL-TL workflow …]`~~ — now the figure from the Cell paper,
      cited and linked to doi.org/10.1016/j.cell.2025.08.002. Check that Cell's
      licence lets you reproduce your own figure on a lab site; for most journals
      authors retain that right, but it is worth a glance at the agreement.
- [ ] Prose is already written from your design — re-read it once for anything that
      changed since you drafted it

## Team (team.html)

- [ ] `[PORTRAIT]` — your photo
- [ ] `[SHORT BIO: …]` — 3–5 sentences
- [ ] Replace the three "Your name here" cards as people join (leave them up while
      recruiting — they read as openings, which is the point)

## Publications (publications.html)

- [ ] `[YOUR PUBMED URL]` — your PubMed author search link
- [ ] `[YOUR GOOGLE SCHOLAR URL]` — your Scholar profile
- [ ] `[YEAR]` / `[EARLIER YEAR]` section headings
- [ ] For each paper: `[PAPER TITLE]`, `[PAPER URL]`, `[Co-authors]`, `[Journal]`,
      `[Year]`, `[DOI URL]`, `[Theme tag]`
- [ ] `[Theme tag]` is the short left-column label (e.g. "Method", "Mitochondria",
      "Translation") — decide on 3–5 tags and use them consistently

## News & Fun (news.html)

- [ ] Two placeholder items: `[DATE]`, `[NEWS HEADLINE]`, `[PHOTO]`, and the body line
- [ ] A news page that hasn't been touched in two years looks worse than no news page.
      Either commit to posting a few times a year, or drop it from the nav until the
      lab is running and there's something to say.

## Join (join.html)

- [ ] `[ADD A LINE ON LAB CULTURE AND MENTORING.]` — the part applicants actually read
      twice. Worth writing yourself rather than reusing boilerplate.
- [ ] `[WHO YOU ARE LOOKING FOR: …]` — postdoc requirements
- [ ] `[PROGRAM 1]`, `[PROGRAM 2]` — which Yale PhD programs you can recruit from.
      Confirm with the department before publishing; it varies by appointment.
- [ ] `[Research technician roles and undergraduate research opportunities.]`
- [ ] `[YALE EQUAL OPPORTUNITY / NON-DISCRIMINATION STATEMENT]` — get the current
      official wording from Yale HR, don't paraphrase

## Contact (contact.html)

- [ ] `[BUILDING, ROOM]`, `[STREET ADDRESS]`, `[ZIP]` — you'll have these once your
      space is assigned
- [ ] `[MAP OR CAMPUS PHOTO]`

## Site-wide

- [ ] The new design dropped **Join Us** from the navigation bar. The page still
      exists and is linked from Team and Contact. While you're actively recruiting,
      consider putting it back in the nav — it's the page prospective postdocs look
      for first.
- [ ] Confirm "Department of Cell Biology, Yale School of Medicine" is the exact
      affiliation to use. The design uses "Yale School of Medicine" on the home and
      news pages and "Yale University" elsewhere; the site now says School of
      Medicine everywhere.
- [ ] `© 2027` in the footer — change to the current year when you launch
- [ ] Favicon (`assets/img/favicon.svg`) is a plain navy "L" — replace if you make a
      lab logo
