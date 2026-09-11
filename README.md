# Personal site — Rizky Wahyu Kristiawan

Single-page professional site. **ERP & System Consultant.**

No build step, no framework, no dependencies. One HTML file plus three assets.

```
index.html                                 the whole site (HTML + CSS + JS)
assets/
  Rizky_Wahyu_Kristiawan_CV.pdf            what the Download CV buttons serve
  og-cover.png                             1200x630 link-preview image
  favicon.svg                              browser tab mark
README.md
```

---

# Hosting it on GitHub Pages

Free, no credit card, and your URL becomes `https://USERNAME.github.io`.

## Step 1 — Name the repository correctly

This is the part people get wrong. If you want the clean URL
`https://USERNAME.github.io` (no `/portfolio` on the end), the repository must be
named **exactly** `USERNAME.github.io`, using your own GitHub username.

So if your username is `rizkywk`, the repo name is `rizkywk.github.io`.

On GitHub: **New repository** → set that name → **Public** (Pages needs public on the
free plan) → do **not** tick "Add a README", since this folder already has one →
**Create repository**.

## Step 2 — Upload the files

**The easy way, no terminal:** on the empty repo page click
**uploading an existing file**. Drag in `index.html`, `README.md`, **and the `assets`
folder itself** — don't open the folder and drag the three files loose, or the paths
break and your CV button 404s. Write "initial site" in the commit box and click
**Commit changes**.

**With git:**

```bash
cd path/to/this/folder
git init
git add .
git commit -m "initial site"
git branch -M main
git remote add origin https://github.com/USERNAME/USERNAME.github.io.git
git push -u origin main
```

## Step 3 — Turn on Pages

In the repository: **Settings** → **Pages** (left sidebar) → under
*Build and deployment*, set **Source: Deploy from a branch**, **Branch: main**,
**Folder: / (root)** → **Save**.

## Step 4 — Wait, then check

First deploy takes 1–3 minutes. Watch the **Actions** tab — a green tick means it
shipped. Then open `https://USERNAME.github.io`.

If you see a 404, give it another two minutes and hard-refresh
(`Ctrl+Shift+R`, or `Cmd+Shift+R` on Mac). GitHub caches aggressively.

## Updating it later

Edit the file, commit, push. The site redeploys itself in about a minute.

```bash
git add .
git commit -m "update case study outcomes"
git push
```

No terminal? Click any file in the repo, hit the pencil icon, edit, commit.

## Optional — your own domain

Buy a domain, then in **Settings → Pages → Custom domain** enter it and save. At your
registrar, add these DNS records:

| Type  | Name | Value                |
|-------|------|----------------------|
| A     | @    | `185.199.108.153`    |
| A     | @    | `185.199.109.153`    |
| A     | @    | `185.199.110.153`    |
| A     | @    | `185.199.111.153`    |
| CNAME | www  | `USERNAME.github.io` |

DNS takes up to 24 hours. Once it resolves, tick **Enforce HTTPS** on the same page.

---

# Before you share the link — three things

**1. Set the real URL.** `index.html` has `https://example.com/` in two places: the
`<link rel="canonical">` tag and `<meta property="og:url">`. Replace both with your
actual Pages URL. Link previews on LinkedIn and WhatsApp read the absolute path from
these, so a wrong value means no preview image.

**2. Fill the five `[Add project outcome]` placeholders.** Search `index.html` for
`class="todo"`. They are deliberately empty — nothing was invented. Fill them only with
results you can defend in an interview. If a project has no clean metric, describe the
end state instead ("went live and the client's IT team took over after handover")
rather than reaching for a number.

**3. Keep the CV filename.** When you update your CV, export to PDF and overwrite
`assets/Rizky_Wahyu_Kristiawan_CV.pdf`. Same name, and every download button keeps
working.

---

# Changing the positioning title

Currently **ERP & System Consultant**. If you later target infrastructure or cloud
roles, search `index.html` for that string — it appears in five places (page title,
og:title, navbar, hero, footer). Change all five so the page stays consistent, and
regenerate the OG image if you want the preview to match.

---

# Optional — linking client names to LinkedIn

The nine client names are plain text on purpose; no URLs were guessed. To link one,
find and verify the company's real LinkedIn page, then:

```html
<h3 class="cx__name">
  <a href="https://www.linkedin.com/company/VERIFIED-SLUG" target="_blank" rel="noopener">
    YKK AP Indonesia
  </a>
</h3>
```

Add to the stylesheet so the links stay quiet:

```css
.cx__name a{ color:inherit; text-decoration:none; border-bottom:1px solid var(--rule); }
.cx__name a:hover{ color:var(--accent); border-bottom-color:var(--accent); }
```

---

# Content rule

Everything on the page comes from the CV. No invented clients, projects, metrics,
durations, titles, or outcomes. Hold anything you add later to the same rule — the
credibility of the whole page rests on every specific claim being checkable.

# How it's built

- **Fonts** — Newsreader (display) and IBM Plex Sans (everything else), from Google
  Fonts. To self-host, download both and swap the `<link>` for `@font-face` rules.
- **The column grid** — faint vertical hairlines fixed behind the content, the measure
  the layout is set against. Hidden below 900px, where there isn't room for it.
- **Dark band** — the work section redefines the colour tokens locally, so every
  component inside it adapts without a second set of rules.
- **Motion** — one load sequence on the hero; everything else answers a click.
  `prefers-reduced-motion` disables all of it.
- **Accessibility** — skip link, real buttons and links, visible focus rings, the case
  study list is an ARIA disclosure pattern, the carousel takes arrow keys, the mobile
  menu closes on Escape.
- **Print** — printing expands every case study, drops the navigation, and turns the
  dark band light so it doesn't burn a cartridge.
