# lvl-refs

Public reference material for LVL Motion sensors and apps: user manuals, FAQs,
hardware guides, LED light patterns, and sensor placement guides.

This repository is the source for the published documentation site. The content
is plain Markdown so it renders on GitHub as-is today and can move to a richer
docs site (Starlight) later without rewriting anything.

## Documentation site (GitHub Pages)

Once Pages is enabled (see below), the site is published at:

**https://lvlmotion.github.io/lvl-refs/**

Individual guides:

- LED light patterns: https://lvlmotion.github.io/lvl-refs/led-patterns
- Sensor placement guide: https://lvlmotion.github.io/lvl-refs/sensor-placement

Pushes to `main` rebuild the site automatically, live in about a minute.

## Repository layout

```
lvl-refs/
  README.md              this file
  docs/                  published content (Pages serves this folder)
    _config.yml          site title and theme
    index.md             site landing page
    led-patterns.md      what each LED colour and pattern means
    sensor-placement.md  where to place each sensor and why
    assets/              images (add as needed)
```

## Adding or editing a guide

1. Add or edit a Markdown file in `docs/`. Give it a short front matter block at
   the top:

   ```
   ---
   title: Your Page Title
   ---
   ```

2. Put any images in `docs/assets/` and link them with a relative path.
3. Commit and push to `main`. The site rebuilds in about a minute.

## Keeping content portable

Write plain Markdown and keep the front matter to a `title` line. Both the current
GitHub Pages setup and a future Starlight site read the same files, so this content
carries over with no rework. Avoid tool-specific syntax so the migration stays a
simple copy.
