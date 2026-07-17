# lvl-refs

Public reference site for LVL Motion sensors and apps (user manuals, FAQs,
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
    index.md           landing page; auto-lists all guides
    *.md               one guide per file
    assets/            images, grouped per guide
```

## Theme and navigation

- Theme is [just-the-docs](https://just-the-docs.github.io/just-the-docs/)
  loaded through `remote_theme` — no vendored theme files, no Gemfile.
- The sidebar nav is generated automatically from every page that has a
  `title` in its front matter, ordered by `nav_order`.
- The landing page (`index.md`) additionally auto-lists all guides with their
  `description` via a Liquid loop over `site.pages` — there is no hand-written
  guide list to maintain anywhere.

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
