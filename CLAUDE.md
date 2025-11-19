# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an academic personal website built with Jekyll and hosted on GitHub Pages. It is based on the [Academic Pages](https://github.com/academicpages/academicpages.github.io) template, which is a fork of the Minimal Mistakes Jekyll theme.

The site showcases academic work including publications, blog posts, talks, teaching materials, and portfolio items.

## Development Commands

### Local Development

Run the site locally with live reload:
```bash
bundle exec jekyll serve
```

Or use the development config:
```bash
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```

Note: There's a typo in the README - the correct command is `bundle exec jekyll serve` (not `liveserve`).

### Setup

First-time setup after cloning:
```bash
bundle clean
bundle install
```

If you encounter errors during `bundle install`, delete `Gemfile.lock` and try again.

### Dependency Management

The site uses `github-pages` gem which manages Jekyll and plugins. Ruby dependencies are managed via Bundler.

## Site Architecture

### Content Collections

Jekyll collections are the core organizational structure:

- **`_pages/`**: Static pages (About, CV, etc.) - rendered at root level via `permalink` front matter
- **`_posts/`**: Blog posts - accessible via `/year-archive/`
- **`_publications/`**: Research publications
- **`_talks/`**: Conference talks and presentations
- **`_teaching/`**: Teaching experience and courses
- **`_portfolio/`**: Portfolio items and projects

Each collection has specific front matter defaults defined in `_config.yml` (lines 192-245) that control layout, author profile visibility, and sharing options.

### Layout System

Custom layouts in `_layouts/`:
- `default.html`: Base layout with header/footer
- `single.html`: Single page/post layout
- `archive.html`: Collection listing pages
- `talk.html`: Specialized layout for talks
- `compress.html`: HTML minification wrapper

### Includes and Components

Modular components in `_includes/`:
- `author-profile.html`: Sidebar with author information
- `archive-single.html`: Individual item in collection listings
- `archive-single-cv.html`: CV-specific item formatting
- `comments.html` & `comments-providers/`: Comment system integration (Staticman, Disqus, etc.)
- `analytics.html` & `analytics-providers/`: Analytics integration

### Styling

SCSS architecture in `_sass/`:
- Component styles: `_base.scss`, `_masthead.scss`, `_sidebar.scss`, `_page.scss`, etc.
- Vendor libraries: Font Awesome, Susy grid system, Magnific Popup, Breakpoint
- Variables and configuration in `_sass/_variables.scss`

Compiled to `assets/css/main.scss` with compression enabled.

### Navigation

Site navigation configured in `_data/navigation.yml`. Currently displays:
- Publications
- Blog Posts (year-archive)
- CV (links to `/files/CV.pdf`)

### Author Data

Author information in `_config.yml` (lines 82-116) includes:
- Bio details (name, avatar, location)
- Social media links (GitHub: Kevincklhhh, LinkedIn, email: kailaic@umich.edu)
- Academic profiles (Google Scholar, ORCID, etc.)

## Key Configuration

### Site Configuration (`_config.yml`)

Important settings:
- **URL**: `https://kevincklhhh.github.io`
- **Repository**: `kevincklhhh/kevincklhhh.github.io`
- **Timezone**: America/Los_Angeles
- **Markdown**: kramdown with GFM input
- **Plugins**: jekyll-paginate, jekyll-sitemap, jekyll-gist, jekyll-feed, jekyll-redirect-from

### Front Matter

All content files use YAML front matter. Common fields:
- `title`: Page/post title
- `permalink`: Custom URL path
- `excerpt`: Short description
- `collection`: Which collection the file belongs to
- `layout`: Template to use
- `date`: Publication date (for posts/publications)

Example from `_pages/about.md`:
```yaml
---
permalink: /
title: "About me"
excerpt: "About me"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---
```

## Content Generation Tools

### Markdown Generators

Python/Jupyter tools in `markdown_generator/` to bulk-create markdown files from TSV data:

- `publications.py` / `publications.ipynb`: Generate publication pages from structured data
- `talks.py` / `talks.ipynb`: Generate talk pages from structured data
- `pubsFromBib.py` / `PubsFromBib.ipynb`: Import publications from BibTeX files

These are useful when adding multiple items at once instead of creating individual markdown files.

### Talk Map

`talkmap.py` / `talkmap.ipynb` generates an interactive map (`talkmap/map.html`) showing geographic locations of talks using Leaflet.js.

## File Organization

### Static Assets

- **`files/`**: PDFs, documents (e.g., CV.pdf)
- **`images/`**: Images, profile photos (e.g., profile.png)
- **`assets/`**: Compiled CSS, JavaScript, fonts

### Comments

User comments stored as YAML files in `_data/comments/{post-slug}/comment-{timestamp}.yml` when using Staticman comment system.

## GitHub Pages Specifics

- Site is published from the `master` branch
- Uses `github-pages` gem to ensure local environment matches GitHub Pages
- Some Jekyll plugins may not work on GitHub Pages - check the whitelist in `_config.yml` (lines 268-273)
- Future posts are enabled (`future: true` in config), so posts with future dates will be published

## Common Workflows

### Adding a New Publication

1. Create a new markdown file in `_publications/` with filename pattern `YYYY-MM-DD-title.md`
2. Add front matter with title, excerpt, date, venue, paperurl, citation
3. Or use `markdown_generator/publications.py` to generate from TSV

### Adding a Blog Post

1. Create markdown file in `_posts/` with filename `YYYY-MM-DD-title.md`
2. Add front matter with title, date, permalink, tags
3. Content written in Markdown below front matter

### Updating the CV

Replace `/files/CV.pdf` with the updated PDF. The navigation link points directly to this file.

### Modifying Site Navigation

Edit `_data/navigation.yml` to add/remove/reorder navigation items.

### Customizing Appearance

- Colors, fonts, spacing: `_sass/_variables.scss`
- Layout modifications: `_layouts/` and `_includes/`
- Per-page customization: Use front matter to override defaults
