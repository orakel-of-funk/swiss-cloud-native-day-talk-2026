# Swiss Cloud Native Day 2026

Presentation slides for the Swiss Cloud Native Day 2026, built with [Slidev](https://sli.dev) and the [FHNW theme](https://github.com/peschmae/slidev-theme-fhnw).

## Getting Started

```bash
# Install dependencies
npm install

# Start the dev server
npm run dev

# Build static slides
npm run build

# Export to PDF locally
npm run export
```

## Automated PDF export

The workflow `.github/workflows/export-pdf.yml` runs on every push to `main`, on pull requests, and on demand via `workflow_dispatch`. It installs dependencies, downloads Playwright Chromium, exports the deck to PDF, and uploads `slides-export.pdf` as a build artifact.

## Project Structure

```text
.
├── components/      # Custom Vue components
├── public/          # Static assets (FHNW logos, etc.)
├── slides.md        # Main slide deck
├── package.json
└── .gitignore
```

## Theme Usage

The FHNW theme is configured in the frontmatter of `slides.md`:

```yaml
---
theme: '@peschmae/slidev-theme-fhnw'
layout: cover
title: Swiss Cloud Native Day 2026
author: Your Name
---
```

Available layouts from the FHNW theme include `cover`, `section`, `end`, and the built-in Slidev layouts (`default`, `center`, `two-cols`, ...).

The theme is installed directly from its GitHub repository so no GitHub Packages authentication token is required. The required public assets (`fhnw-logo.svg`, `swissuniversities.png`, and `FHNW_HSI_EN.png`) are included in the `public/` folder.

## License

MIT
