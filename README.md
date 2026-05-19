# felixpleiva.github.io

Personal academic website of **Félix P. Leiva** — built with [Quarto](https://quarto.org) and deployed automatically to GitHub Pages.

Live at: <https://felixpleiva.github.io>

> **Workflow note.** This README assumes you use [GitHub Desktop](https://desktop.github.com/) to manage Git — no terminal `git` commands needed. For a longer step-by-step walkthrough (including how to write blog posts in R), see [`GUIDE.Rmd`](GUIDE.Rmd).

---

## What you need installed

1. [GitHub Desktop](https://desktop.github.com/) — for syncing your changes.
2. [Quarto](https://quarto.org/docs/get-started/) (version 1.5+) — to preview the site locally.
3. A text editor — RStudio, VS Code, or anything you like.
4. *(Optional)* [R](https://cran.r-project.org/) and RStudio if you want to run code in blog posts.

---

## First-time setup with GitHub Desktop

You only do this once.

### 1. Create the repository on GitHub

1. Go to <https://github.com/new>.
2. **Repository name:** `felixpleiva.github.io` (this exact name is required).
3. **Visibility:** Public.
4. **Do not** check "Initialize this repository with a README" — leave the box empty.
5. Click *Create repository*.

### 2. Put the project files into a local folder

1. Unzip `xxxxxxx.zip` somewhere you can find it (e.g. `Documents/xxxxxx-site/`).

### 3. Add the folder to GitHub Desktop

1. Open **GitHub Desktop**.
2. *File → Add local repository…* → choose the unzipped `felixpleiva-site` folder.
3. GitHub Desktop will say *"This directory does not appear to be a Git repository"*. Click **create a repository** in that message.
4. In the dialog: leave the defaults, click **Create Repository**.

### 4. Publish it to GitHub

1. In the top bar, click **Publish repository**.
2. **Uncheck** "Keep this code private" (must be public for free GitHub Pages).
3. **Name:** make sure it says `felixpleiva.github.io`.
4. Click **Publish Repository**.

### 5. Turn on GitHub Pages

1. On <https://github.com/your_repoyour_repo/your_repo.github.io>, go to **Settings → Pages**.
2. Under *Build and deployment → Source*, choose **Deploy from a branch**.
3. Set *Branch* to `gh-pages` and folder to `/ (root)`. Click **Save**.

> The `gh-pages` branch doesn't exist yet — it will be created automatically by the GitHub Action the first time it runs.

### 6. Allow the GitHub Action to write to the repo

1. **Settings → Actions → General**.
2. Scroll to *Workflow permissions* → select **Read and write permissions**.
3. Click **Save**.

### 7. Trigger the first deploy

In GitHub Desktop:

1. Open the file `_quarto.yml` in your editor, add or remove a space, save.
2. Back in GitHub Desktop you'll see the change → write a summary like *"Initial deploy"* → click **Commit to main**.
3. Click **Push origin** at the top.

Go to the **Actions** tab on GitHub. You'll see the `publish.yml` workflow running. After ~2 minutes:

- Visit **<https://felixpleiva.github.io>**.
- The site is live.

> If it loads without styles the very first time, wait 2–5 minutes and refresh with Ctrl+F5 (Windows) or Cmd+Shift+R (Mac).

---

## Day-to-day workflow with GitHub Desktop

Every time you want to update the site:

1. Open the project folder in your editor.
2. *(Optional but recommended)* Open a terminal **inside that folder** and run:
   ```
   quarto preview
   ```
   This opens <http://localhost:4200> with auto-reload while you edit.
3. Edit any `.qmd` file (Home, Publications, Projects…) or `assets/custom.scss`.
4. Save.
5. In **GitHub Desktop**:
   - You'll see all your changes listed in the left panel.
   - Write a short summary at the bottom (e.g. *"Add 2026 paper"*).
   - Click **Commit to main**.
   - Click **Push origin** at the top.
6. The GitHub Action runs automatically. In ~2 minutes the live site is updated.

That's it — no terminal Git commands needed.

---

## How deployment works

Pushing to `main` triggers `.github/workflows/publish.yml`, which:

1. Sets up Quarto on a fresh Ubuntu runner.
2. Runs `quarto render`.
3. Publishes the rendered `_site/` folder to the `gh-pages` branch.

GitHub Pages serves whatever is on `gh-pages`. You configure it once (step 5 above) and never touch it again.

---

## Project layout

```
felixpleiva-site/
├── _quarto.yml                 # Site config (navbar, footer, theme)
├── index.qmd                   # Home / About
├── publications.qmd            # Selected publications
├── projects.qmd                # Research themes
├── teaching.qmd                # Workshops, courses, supervision
├── blog.qmd                    # Blog index (auto-listing)
├── cv.qmd                      # Embedded PDF viewer
├── posts/                      # One folder per blog post
│   └── 2026-04-tdt-curves-brms/
│       ├── index.qmd
│       └── thumbnail.png
├── images/                     # Profile photo, logos
├── files/
│   └── cv.pdf                  # ← replace with your real CV
├── assets/
│   ├── custom.scss             # Theme overrides (sage palette)
│   └── styles.css              # Extra CSS utilities
├── _extensions/                # Quarto extensions (FontAwesome, Iconify)
├── .github/workflows/publish.yml   # CI/CD
├── README.md                   # This file
└── GUIDE.Rmd                   # Full editing guide (knit in RStudio)
```

---

## Adding a new blog post

1. Inside `posts/`, create a new folder, e.g. `posts/2026-06-my-new-post/`.
2. Create a file inside called `index.qmd` with this front-matter:

   ```yaml
   ---
   title: "Post title"
   description: "One-sentence summary"
   author: "Félix P. Leiva"
   date: "2026-06-15"
   categories: [R, ggplot2]
   image: thumbnail.png
   format:
     html:
       code-fold: false
       code-tools: true
       code-block-bg: true
       code-block-border-left: "#5f7d63"
   execute:
     warning: false
     message: false
   ---
   ```

3. Write the post in Markdown below the front-matter. R code chunks use:

   ````
   ```{r}
   library(ggplot2)
   ggplot(mtcars, aes(mpg, wt)) + geom_point()
   ```
   ````

4. *(Optional)* Save a `thumbnail.png` in the same folder for the listing card.
5. Preview with `quarto preview`.
6. **Commit and push from GitHub Desktop** — the post appears on `/blog` automatically.

See `GUIDE.Rmd` for a longer R-focused walkthrough.

---

## Editing common sections

| Want to change… | Edit this file |
|---|---|
| Bio, photo, social icons, Interests, Education | `index.qmd` |
| List of publications | `publications.qmd` |
| Research themes / project cards | `projects.qmd` |
| Workshops, courses, supervision | `teaching.qmd` |
| CV PDF shown on the CV page | replace `files/cv.pdf` |
| Navbar items, site title, footer | `_quarto.yml` |
| Colors, fonts, spacing | `assets/custom.scss` |

Detailed examples for each are in `GUIDE.Rmd`.

---

## Custom domain (later)

When you want to switch from `felixpleiva.github.io` to your own domain (e.g. `felixleiva.com`):

1. Buy the domain from a registrar (Cloudflare, Namecheap, Porkbun…).
2. Create a file at the repo root called `CNAME` containing only your domain, e.g. `felixleiva.com`.
3. At your registrar, add these DNS records:

   | Type  | Name | Value                  |
   | ----- | ---- | ---------------------- |
   | A     | @    | 185.199.108.153        |
   | A     | @    | 185.199.109.153        |
   | A     | @    | 185.199.110.153        |
   | A     | @    | 185.199.111.153        |
   | CNAME | www  | felixpleiva.github.io. |

4. In **GitHub Settings → Pages**, enter your domain under *Custom domain* and tick *Enforce HTTPS* once the certificate is issued (usually within minutes).
5. Update `site-url:` in `_quarto.yml` to the new URL.
6. Commit and push from GitHub Desktop.

---

## Troubleshooting

| Symptom | What to check |
|---|---|
| Site loads without styles right after first deploy | Wait 2–5 minutes, refresh with Ctrl+F5 / Cmd+Shift+R |
| GitHub Action fails with *Permission denied* | Settings → Actions → General → Workflow permissions = **Read and write** |
| Action passes but site shows 404 | Settings → Pages → Branch must be `gh-pages` |
| CV page shows a blank gray box | `files/cv.pdf` is missing or empty — replace it |
| FontAwesome icons missing | The `_extensions/` folder must be committed — verify it's in GitHub Desktop |
| GitHub Desktop says *"Cannot push, fetch first"* | Click **Fetch origin** at the top, then **Pull**, then **Push** again |
| `quarto preview` won't start | Another preview is already running on port 4200 — close the previous terminal or run `quarto preview --port 4321` |

---

## License

All site content is licensed under [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
Configuration code (Quarto / SCSS) is MIT.
