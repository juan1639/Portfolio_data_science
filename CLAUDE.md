# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A personal data science / AI portfolio website built with **Quarto** (static site). All site content is written in **Spanish**; keep new content and commit messages in Spanish to match.

## Commands

```bash
quarto preview          # local dev server with live reload
quarto render           # build the whole site into docs/
quarto render about.qmd # render a single page
pip install -r requirements.txt   # Python deps needed to render the notebook
```

There are no tests or linters.

## Architecture

- `_quarto.yml` defines the site: `output-dir: docs`, an explicit `render:` list (only files listed there are built), navbar, and the cosmo theme + `styles.css`.
- **`docs/` is committed build output** (presumably served via GitHub Pages). After changing any `.qmd`, `.ipynb`, `styles.css`, image or `_quarto.yml`, run `quarto render` and commit the regenerated `docs/` along with the source; never hand-edit files in `docs/`.
- `proyectos.qmd` is a Quarto **listing** that auto-builds a grid from `proyectos/*.qmd`. Each project page needs front matter `title`, `description`, `categories`, `image` (path `../img/...`) and `order` (controls sort position). Adding a project = adding a new file in `proyectos/` plus its image in `img/`.
- `img/` is the source for images (copied to `docs/img/` via `resources: img/*`).
- `bank_marketing_pipe.ipynb` is rendered as its own page and linked from `proyectos/marketing-bancario.qmd`. It reads `bank-full.csv`, which is **not** in the repo, so rendering relies on the outputs already stored in the notebook — don't strip them. Quarto's `.ipynb` rendering does not re-execute by default.
- Files not in the `render:` list (`mlops_project.qmd` is an old template draft, `final_project_bf_juan_eguia_v2.ipynb`) are not part of the site. `novale*` files are gitignored scratch/obsolete files; ignore them.
