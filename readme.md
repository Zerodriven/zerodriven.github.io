# Zerodriven Website

This repository contains the source for the jasonbenedetti.co.uk static site built with Jekyll.

## Project Overview

A content-first static website generated with Jekyll. Source content (Markdown, Liquid templates, SCSS, and assets) live in this repository. Jekyll compiles those sources into static files under `_site/` which are then deployed to a static hosting provider.

## Architecture

- Source: Markdown (.md), Liquid templates (.html/.liquid), SCSS and assets in the repository.
- Build: Jekyll reads `_config.yml`, templates and content, outputs a static site into `_site/`.
- Serve: Local preview via Jekyll's server.
- Deploy: Upload the contents of `_site/` to the chosen host (GitHub Pages, Netlify, S3, etc.).

### Flow
1. Edit content or templates in the repo.
2. Build with Jekyll to validate generation.
3. Deploy generated `_site/`.

## Tech stack

- Ruby
- Bundler (gem dependency manager)
- Jekyll (static site generator)
- Liquid (templating)
- SCSS/CSS, plain JavaScript

## Requirements

- Ruby (2.7+ recommended)
- Bundler
- A local terminal (PowerShell recommended on Windows)

Install dependencies:

```powershell
gem install bundler
bundle install
```

## Build & Serve (local)

Use Bundler to ensure consistent gem versions. The project expects `bundle exec` to be used when running Jekyll commands.

- Build the site (generate static files in `_site/`):

```bash
bundle exec jekyll build
```

- Serve locally with live-reload (recommended for development):

```bash
bundle exec jekyll serve
```

Note: Explicitly using `bundle exec jekyll build` / `bundle exec jekyll serve` ensures the gems defined in the Gemfile/Gemfile.lock are used.

## Directory layout (common)

- _config.yml — Jekyll configuration
- _posts/ — blog posts
- _layouts/ — page/layout templates
- _includes/ — reusable template partials
- assets/ — images, styles, scripts
- _site/ — generated output (do not commit)

## Deployment

1. Run `bundle exec jekyll build` to generate `_site/`.
2. Deploy `_site/` contents to your host.

Examples:
- GitHub Pages: configure GitHub Pages settings or use a publishing branch
- Netlify: set build command `bundle exec jekyll build` and publish directory `_site`

## Contributing

- Follow existing template and content patterns.
- Test changes locally with `bundle exec jekyll serve` before opening PRs.
- Update Gemfile and Gemfile.lock when adding or changing gems.

## Troubleshooting

- If pages fail to build, run `bundle exec jekyll build --trace` for detailed errors.
- Ensure `bundle install` completes successfully after Gemfile changes.

## License & Contact

See repository license file or contact the maintainers for more details.
