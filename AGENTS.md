# AGENTS.md

Agent-focused guide for working on this Slidev presentation repository.

## Project Overview

This repository contains the Slidev presentation for the FHNW bachelor thesis
**"Automated Kubernetes Workload Hardening Using a Functionality Oracle"**
by Mathias Petermann.

The deck uses the FHNW Slidev theme (`@peschmae/slidev-theme-fhnw`) and is
built with [Slidev](https://sli.dev). A GitHub Actions workflow automatically
exports the deck to PDF on push to `main`, pull requests, and manual triggers.

## Repository Structure

```text
.
├── .github/workflows/export-pdf.yml   # CI workflow for PDF export
├── components/                        # Custom Vue components (currently empty)
├── public/                            # Static assets
│   ├── FHNW_HSI_EN.png                # FHNW logo variant required by theme
│   ├── fhnw-logo.svg                  # FHNW logo required by theme
│   ├── swissuniversities.png          # swissuniversities logo required by theme
│   └── xkcd-1256-questions.png        # Comic used on final slide
├── slides.md                          # Main slide deck (single file)
├── package.json                       # Dependencies and npm scripts
├── package-lock.json                  # Lockfile
├── .gitignore                         # Ignore node_modules, dist, generated PDFs/PNGs
├── README.md                          # Human-readable setup guide
└── AGENTS.md                          # This file
```

## Getting Started

```bash
# Install dependencies
npm install

# Start the dev server with live reload
npm run dev

# Build static site to dist/
npm run build

# Export PDF locally (requires Playwright Chromium)
npm run export
```

## Working on Slides

- **Single-file deck:** All slides live in `slides.md`.
- **Slide separator:** Use `---` on its own line between slides.
- **Frontmatter per slide:** Put YAML frontmatter between the separator and the
  slide content, e.g.:

  ```markdown
  ---
  layout: section
  ---

  # Section Title
  ```

- **Layouts:** Prefer FHNW theme layouts:
  - `cover` — title slide
  - `section` — section divider
  - `end` — final slide
  - `default`, `center`, `two-cols` — standard Slidev layouts

- **Images:** Place assets in `public/` and reference them with root-relative
  paths, e.g. `![alt](/xkcd-1256-questions.png)`. Do not use relative paths like
  `./public/...`.

- **Tables and code blocks:** Standard Markdown works. Keep line lengths
  reasonable for reviewability.

- **Diagrams:** Mermaid diagrams can be embedded in fenced code blocks with the
  `mermaid` language identifier.

## Theme and Assets

- The FHNW theme is installed from its GitHub repository
  (`github:peschmae/slidev-theme-fhnw`) so no GitHub Packages token is needed.
- The theme expects `/fhnw-logo.svg` and `/swissuniversities.png` to exist in
  `public/`. Do not remove these files.
- New static assets should go into `public/`.

## CI / PDF Export

- Workflow: `.github/workflows/export-pdf.yml`
- Runs on: push to `main`, pull requests, `workflow_dispatch`.
- Steps: checkout → setup Node 22 → `npm ci` → install Playwright Chromium →
  `npm run export` → upload `slides-export.pdf` artifact.
- When editing the workflow, keep the artifact path in sync with the export
  filename produced by `slidev export` (default: `slides-export.pdf`).

## Conventions

- Keep the FHNW theme configuration in the global frontmatter at the top of
  `slides.md`.
- Preserve the `cover` layout frontmatter fields: `title`, `author`.
- Use `layout: section` for major topic breaks.
- Use the final slide for Q&A; the xkcd comic is referenced as
  `/xkcd-1256-questions.png`.
- Do not commit `node_modules/`, `dist/`, or generated PDF/PNG exports.
- Root-level generated PNGs are ignored via `/*.png`, while `public/*.png` is
  tracked.

## Common Tasks

| Task | Command |
| --- | --- |
| Preview locally | `npm run dev` |
| Build static site | `npm run build` |
| Export PDF locally | `npm run export` |
| Install Chromium for export | `npx playwright install chromium` |

## Gotchas

- If `npm install` fails with a 401 from `npm.pkg.github.com`, make sure no
  `.npmrc` is overriding the `@peschmae` scope to the GitHub Packages registry.
  The theme is intentionally installed from the git repository.
- The FHNW theme references logos with absolute root paths, so they must live
  in `public/`.
- Running `npm run export` for the first time requires a Playwright Chromium
  download (the CI workflow handles this with `npx playwright install --with-deps
  chromium`).

## License

MIT
