# lvl-refs

Public reference site for LEVEL Motion sensors and apps (user manuals, FAQs,
hardware guides). Published via GitHub Pages at
https://lvlmotion.github.io/lvl-refs/ — pushes to `main` rebuild the live site
in about a minute, so treat every push as a production deploy.

`README.md` is deliberately minimal: it is the public landing card for the
repo, aimed at end users, not contributors. Keep contributor/maintainer notes
here, not there.

## Layout

```
lvl-refs/
  README.md            public landing card (title + site URL only)
  CLAUDE.md            this file — contributor conventions
  docs/                published content (Pages serves this folder)
    _config.yml        site config (just-the-docs via remote_theme)
    index.md           landing page: quick links + guides grouped by product
    *.md               one guide per file
    assets/            images, grouped per guide
```

## Theme and navigation

- Theme is [just-the-docs](https://just-the-docs.github.io/just-the-docs/)
  loaded through `remote_theme` — no vendored theme files, no Gemfile.
- Colors use a custom "level" scheme (`color_scheme: level` in `_config.yml`,
  defined in `docs/_sass/color_schemes/level.scss`): a dark base with the app's
  teal-green accents, sampled from the LEVEL Sensor app. A local `_sass` file
  overrides the remote theme's, so this works without vendoring the theme.
- The sidebar nav is generated automatically from every page that has a
  `title` in its front matter, ordered by `nav_order`.
- The landing page (`index.md`) is a hand-written table of contents: quick links,
  then the guides grouped by product (Hardware: LEVEL Inez and LEVEL Hub;
  LEVEL Collector for Android; LEVEL Collector for Windows). **When you add a
  guide, also add a line for it under the right group in `index.md`.**
  Specifications live on their own page, `sensors-and-apps.md`.

## Adding or editing a guide

1. Add or edit a Markdown file in `docs/` with this front matter:

   ```
   ---
   title: Your Page Title
   description: one-line summary shown in the landing-page list
   nav_order: <position in the sidebar>
   ---
   ```

2. Put images in `docs/assets/<guide-name>/` and reference them with relative
   paths. Screenshots are annotated with a red box around the tap target
   (8px stroke, #FF3B30, drawn at original resolution).
3. Write for an end user holding the phone, not for a developer. Plain
   language, no internal code names, no repository or variable names.

## Keeping content portable

Write plain Markdown; keep front matter to `title`, `description`, and
`nav_order`. A future migration (e.g. Starlight) should be able to read the
same files with no rework, so avoid theme-specific syntax in page bodies
(theme-specific behavior belongs in `_config.yml` and front matter only).

## Verifying changes

There is no local build set up. Verify by pushing and checking the live site
(the Pages build takes about a minute; the CDN caches pages for up to 10
minutes — hard refresh or add a throwaway query string to bypass).
