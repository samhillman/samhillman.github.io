# samhillman.github.io

Personal site for Sam Hillman, built with [Quarto](https://quarto.org) and published to
GitHub Pages.

## Local preview

Open the project in RStudio and run:

```bash
quarto preview
```

This serves the site at <http://localhost:4200> and live-reloads as you edit `.qmd` files.

## Publishing

Pushing to `master` triggers the `Quarto Publish` GitHub Action, which renders the site and
deploys it to the `gh-pages` branch. No manual render step is needed.

GitHub Pages serves from the `gh-pages` branch (Settings → Pages → Source).

### If the `gh-pages` branch is ever lost

The publish action fails if the branch doesn't already exist, and `quarto publish gh-pages
--no-prompt` won't create it — so recreate it with an empty commit first:

```bash
git branch gh-pages $(git commit-tree $(git hash-object -t tree /dev/null) -m "Init gh-pages")
git push origin gh-pages
```

Any R code in pages uses `freeze: auto` — re-render locally (`quarto render`) and commit the
`_freeze/` directory when R code changes, so CI never needs R installed.

## Structure

| Path | Purpose |
|---|---|
| `_quarto.yml` | Site config: navbar, SEO metadata, theme, `llms-txt` |
| `index.qmd` | Home page (bio, links, Person JSON-LD) |
| `publications.qmd` | Hand-curated publication list |
| `articles/` | Articles listing plus one directory per article |
| `cv.qmd` | CV page (HTML only — no PDF download) |
| `styles.scss` | Minimal theme overrides on top of `cosmo` |
| `robots.txt` | Allows all crawlers, points to the sitemap |

## Adding an article

Create `articles/<slug>/index.qmd` with `title`, `description`, `date`, and `categories` in
the front matter. It appears on the listing page automatically. Set `draft: true` to keep it
unpublished while writing.
