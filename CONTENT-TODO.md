# Content checklist

Every item below is a `[PLACEHOLDER]` in the HTML. Delete a line when it's done.
Find them all at any time: `grep -rno '\[[A-Z][^]]*\]' *.html`

## Blocking — nothing else should go live without these

- [ ] `[EMAIL]` — lab contact address. Appears in the footer of all 6 pages, plus
      team.html, join.html (×2), contact.html. One find-and-replace:
      `sed -i 's/\[EMAIL\]/you@yale.edu/g' *.html`
- [ ] `[FIRST NAME] Luo, PhD` and `[TITLE]` — team.html
- [ ] `Luo [INITIALS]` — publications.html, the bolded author name

## Home (index.html)

- [ ] Three recent publications — `[PAPER TITLE]`, `[AUTHORS…]`, `[Journal]`, `[Year]`
- [ ] `[HERO FIGURE: …]` — the one image that will define the site. A LOCL-TL schematic
      or a striking micrograph. Worth commissioning or making properly.
- [ ] Check the 2027 recruiting banner still reads right once you've started

## Research (research.html)

- [ ] `[FIGURE: mRNA targeting to mitochondria without an MTS]`
- [ ] `[FIGURE: LOCL-TL workflow …]`
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

- [ ] Confirm "Department of Cell Biology" is the exact departmental name to use
- [ ] `© 2027` in the footer — change to the current year when you launch
- [ ] Favicon (`assets/img/favicon.svg`) is a plain navy "L" — replace if you make a
      lab logo
