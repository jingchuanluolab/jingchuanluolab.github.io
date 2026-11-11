# Next steps: from this folder to a live lab website

Written 2026-11-11. The site in this folder is complete and working — what remains is
filling in your content, putting it on GitHub, and pointing a domain at it.

---

## Step 0 — look at it first (2 minutes)

```bash
cd path/to/lab_website && python3 -m http.server 8000
```

Open <http://localhost:8000>, click through all six pages, resize the window down to
phone width. If you're on the cluster over SSH, tunnel it:
`ssh -L 8000:localhost:8000 <you>@<cluster>` and open the same URL on your laptop.

Nothing is installed and nothing needs to be. This is plain HTML and CSS — no Node, no
Jekyll, no conda environment. If we later add something that needs packages (a
publication-list generator, image optimisation), that's when we make the conda env.

---

## Step 1 — fill in your content (the slow part, do it first)

Everything in `[SQUARE BRACKETS]` is a placeholder. `CONTENT-TODO.md` is the checklist.
List them all at any time with:

```bash
grep -rno '\[[A-Z][^]]*\]' *.html
```

The two that block everything else are **your email address** and **your name as it
should appear**. The figures can wait; grey dashed boxes look deliberate, half-finished
prose does not.

A note on timing: you start in 2027, and a site that says "recruiting for 2027" with
three empty member slots is exactly right to put up *now*. Prospective postdocs and
grad students search for new labs a year ahead. Getting it live early is worth more
than getting it perfect.

---

## Step 2 — put it on GitHub

The site lives under the GitHub account **`jingchuanluolab`**, created 2026-11-11 as a
dedicated lab account rather than a personal one. The repo is named
`jingchuanluolab.github.io` — account name + `.github.io` — which is what makes GitHub
serve it at the root of the domain and keeps every link in the site simple.

```bash
cd path/to/lab_website
gh repo create jingchuanluolab/jingchuanluolab.github.io --public --source=. --remote=origin --push
```

Then turn on Pages: **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.
Within a minute the site is live at `https://jingchuanluolab.github.io`.

> The repo must be **public** for free GitHub Pages. That's fine — it's a public
> website. Just don't commit anything you wouldn't put on the web (unpublished
> figures, draft manuscripts, personal addresses).

### Authenticating gh

The browser device-code flow (`gh auth login --web`) is awkward from the cluster. Use a
token instead:

1. Create one at <https://github.com/settings/tokens/new?scopes=repo,read:org&description=luolab-website>
   — classic token, scopes **`repo`** and **`read:org`**. `repo` does the real work
   (create, push, Pages); `read:org` is required by the `gh` CLI itself at login time
   and is checked even when you belong to no organisations. Omitting it fails with
   `error validating token: missing required scope 'read:org'`.

   Already made a token without it? You do not need a new one — go to
   <https://github.com/settings/tokens>, click the token, tick `read:org`, and press
   **Update token**. The value stays the same.
2. Log in without the token touching disk or scrollback:

```bash
read -rs -p "Token: " T; echo; printf '%s' "$T" | gh auth login --hostname github.com --git-protocol https --with-token; unset T
```

If the token expires, repeat both steps — nothing else changes.

### Adding lab members later

A single account is fine while you are the only one editing. Do **not** share its
password around as the lab grows; that is both against GitHub's terms and a real
security problem. Two clean options when you get there:

- **Convert the account to an organisation** (Settings → Access → *Convert to
  organization*). Repos and the Pages site carry over, and you then add members as
  named collaborators with their own accounts. You need a second personal account to
  act as owner.
- **Keep it a user account** and add collaborators to the repo individually under
  Settings → Collaborators.


---

## Step 3 — buy a domain

**Recommended name:** `luolab.org`. `.org` is the long-standing academic default, it's
cheap (~$12/year), and it won't look dated in ten years. Check availability for
`luolab.org`, `luo-lab.org`, `luolab.science`, `luolab.bio` (`.bio` runs ~$60–90/year,
which is a lot for a vanity TLD). Avoid `.io` — the TLD's future is genuinely uncertain.

**Recommended registrar:** [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/).
It sells domains at wholesale cost with no markup and no renewal-price jump, includes
WHOIS privacy free, and its DNS is the fastest and easiest to configure. The one catch
is that you must use Cloudflare's nameservers, which is what you want anyway.

[Porkbun](https://porkbun.com) is a fine alternative with a friendlier UI.
**Avoid** Squarespace Domains (what Google Domains became) and GoDaddy — both upsell
heavily and renew expensive.

Pay for 5 years up front if you can expense it, and **turn on auto-renew**. The single
most common way a lab website dies is a lapsed domain.

### Who should own it

Register it in your own name with your Yale email, and pay from a lab or startup fund
if allowed. Do *not* let it sit in a departmental IT account you can't access — if you
move institutions, the domain moves with you. That portability is the whole reason to
buy one rather than just using the `yale.edu` page the department will give you. Use
both: the Yale page for institutional presence, your own domain as the canonical link
you put on papers and talks.

---

## Step 4 — point the domain at GitHub Pages

Current GitHub Pages addresses (verified against GitHub's docs on 2026-11-11 — if this
is more than a year old, re-check [the docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)):

In your registrar's DNS panel, on the apex (`@`, meaning `luolab.org` itself):

| Type | Name | Value |
|------|------|-------|
| A    | @    | 185.199.108.153 |
| A    | @    | 185.199.109.153 |
| A    | @    | 185.199.110.153 |
| A    | @    | 185.199.111.153 |
| AAAA | @    | 2606:50c0:8000::153 |
| AAAA | @    | 2606:50c0:8001::153 |
| AAAA | @    | 2606:50c0:8002::153 |
| AAAA | @    | 2606:50c0:8003::153 |
| CNAME | www | jingchuanluolab.github.io |

On Cloudflare specifically: set each of these to **DNS only** (grey cloud), not
proxied — the orange cloud interferes with GitHub issuing your certificate. You can
turn proxying on later once HTTPS is working.

Then, in the repo:

```bash
echo "luolab.org" > CNAME
git add CNAME && git commit -m "Add custom domain" && git push
```

And in **Settings → Pages → Custom domain**, enter `luolab.org` and save. Wait for the
DNS check to pass (minutes to a few hours), then tick **Enforce HTTPS**. GitHub issues
a free Let's Encrypt certificate automatically.

Verify when you think it's done:

```bash
dig luolab.org +noall +answer -t A
curl -sI https://luolab.org | head -1
```

---

## Step 5 — the small things that matter later

- **Add your lab members as collaborators** on the repo once they arrive. Teaching a
  first-year grad student to edit one HTML block and push is a 20-minute conversation,
  and then you're not the bottleneck for every update.
- **Google Scholar + ORCID links** on the publications page — fill those in, they're
  how people verify you're the Luo they're looking for.
- **A news or blog section** is the one thing most new labs add within a year. Easy to
  bolt on: copy a page, add a nav link.
- **Don't add analytics** unless you actually want them. If you do, Plausible or
  GoatCounter are privacy-respecting and don't need a cookie banner; Google Analytics
  in the EU does.
- **Back-up is automatic** — that's a side benefit of GitHub. Every version of every
  page is in the history.

---

## Alternative route: Netlify (no GitHub account)

If you want the site on a real URL today without the GitHub account, token and 2FA
dance, use Netlify instead. `luolab-site.zip` in this folder is the deployable bundle
(the six pages, 404, stylesheet, favicon and robots.txt — no git history, no internal
notes).

1. Go to <https://app.netlify.com/drop>
2. Drag `luolab-site.zip` onto the page
3. It is live in about thirty seconds at a random address like
   `wandering-lumen-8f2a1c.netlify.app`

**The catch, and it matters:** a site dropped anonymously is deleted if you do not
*claim* it, and the claim window is short — reported as one hour. Claiming means
signing up. So "no account" really means "no account for the first hour".

The upside is that the Netlify signup is far lighter than GitHub's: an email address
and a password, no mandatory two-factor, no personal access tokens, no CLI. Claim the
site as soon as it is live and you are done.

Once claimed you can:

- rename the site to something sane (`luolab.netlify.app`) in **Site settings → Change
  site name**
- attach `luolab.org` under **Domain management → Add a domain**; Netlify issues the
  HTTPS certificate automatically
- redeploy by dragging a new zip onto the site's Deploys tab

**What you give up versus GitHub:** version history, the ability to add lab members as
editors, and a site that can be handed to a student in 2029 without handing over your
password. Updating means regenerating and re-dragging a zip rather than editing a file
in place. For a six-page site that changes a few times a year, that is a defensible
trade — just know you are making it.

You can move to GitHub later without redoing any of this work. The files are the same
files, and `CNAME`/DNS is the only part that changes.

---

## Why plain HTML and not Jekyll/Hugo/Astro

For a six-page lab site edited a few times a quarter, a static-site generator costs
more than it saves: a toolchain to install, a config to learn, a build that breaks when
a dependency moves, and a barrier for any lab member who wants to fix a typo. The one
thing you give up is a shared header — the nav block is copy-pasted into each of the
six pages, so adding a seventh page means editing six files. That's a rare, two-minute
cost against never having to debug a build.

If the site ever outgrows this (a news feed with dozens of posts, a publication list
you want generated from a `.bib` file), the HTML and CSS here port into Astro or 11ty
almost unchanged, and that's the moment to make a conda or npm environment.
