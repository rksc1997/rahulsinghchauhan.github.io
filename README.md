# rksc1997.github.io

Source for the personal academic website of Rahul Singh Chauhan — <https://rksc1997.github.io>

Built with [Hugo](https://gohugo.io) (extended) using custom layouts, no external theme. Pushing
to `main` triggers `.github/workflows/deploy.yml`, which builds the site and publishes it to
GitHub Pages.

**To change content, see [UPDATING.md](UPDATING.md).** It covers adding papers, teaching, awards,
and talks without needing to install anything.

## Layout of the repository

```
hugo.yaml                    site config: name, title, email, tagline, menu, credit toggles
content/_index.md            homepage bio
data/papers.yaml             working papers, work in progress, publications
data/teaching.yaml           teaching history
data/awards.yaml             fellowships, grants, awards
data/talks.yaml              presentations, grouped by paper
layouts/index.html           homepage template — renders every section
layouts/partials/paper.html  renders one entry from data/papers.yaml
layouts/_default/            page shell and generic single/list templates
assets/css/style.css         all styling
static/files/                cv.pdf and paper PDFs
static/images/photo.jpg      headshot
static/favicon*              favicons
```

Sections with no data are omitted from the page automatically.

## Building locally

Requires Hugo extended.

```bash
hugo server
```

Then open <http://localhost:1313>. To reproduce the production build:

```bash
hugo --gc --minify
```

## GitHub Pages setup

One-time, in the repository: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
