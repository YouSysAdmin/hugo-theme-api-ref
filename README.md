# API-REF — Hugo API documentation theme

A monospace, "datasheet"-style Hugo theme for API reference documentation.

## Features

- **Light / dark theme** — follows the OS preference, with a manual toggle
  persisted in `localStorage`.
- **Versioned docs** — document any number of API versions under
  `content/docs/<version>/`. The masthead renders a version selector that jumps
  to the same page in the chosen version; non-latest versions show a warning
  banner linking to the latest.
- **Per-version masthead metadata** — each version sets its own `status` and
  `baseURL` in front matter; the topbar follows the version you're browsing.
- **Changelog section** — entries grouped by month with tags, authors, a "New"
  badge for recent entries, and older/newer navigation.
- **Endpoint shortcodes** — method/path bars with an auth-required lock badge.
- **Per-page TOC** — "ON THIS PAGE" list from `<h2>`/`##` headings.
- **SEO / social meta** — canonical URL, Open Graph, Twitter cards, and
  Schema.org tags on every page. Set a default preview image with
  `images = ["og-image.png"]` in `[params]` (override per page via `images`
  front matter).

## Requirements

- [Hugo](https://gohugo.io/installation/) ≥ 0.150
- [Go](https://go.dev/dl/) — only when installing the theme as a Hugo Module

## Installation

### As a Hugo Module (recommended)

Turn your site into a Hugo Module (once) and import the theme:

```bash
hugo mod init github.com/<you>/<your-site>
```

```toml
# hugo.toml
[module]
  [[module.imports]]
    path = "github.com/YouSysAdmin/hugo-theme-api-ref"
```

Then fetch it (and later update with the same command):

```bash
hugo mod get -u github.com/YouSysAdmin/hugo-theme-api-ref
```

### As a git submodule / clone

```bash
git submodule add https://github.com/YouSysAdmin/hugo-theme-api-ref themes/api-ref
```

```toml
# hugo.toml
theme = "api-ref"
```

## Run this repo

Demo content ships inside the theme as `exampleSite`, wired to the
theme via a module replacement, so it runs from the checkout directly:

```bash
hugo server -s exampleSite
```

## Layout

```
  hugo.toml                       # Hugo config
  content/
    _index.md                     # home / overview
    showcase.md                   # single page
  docs/
    _index.md                     # version index (lists all API versions)
    v1/                           # one section per API version
      _index.md                   # status, baseURL, latest?, weight
      authentication.md …
    v2/
  changelog/
    _index.md
    2026/01-01-first.md …         # one file per changelog entry
```

## Sidebar order
1. API docs
2. Single pages
3. Changelog

## API versions

Each version is a section under `content/docs/`. Its `_index.md` front matter
drives the masthead and the version selector:

```yaml
---
title: "v2.0.0" # label shown in the selector
weight: 10 # order in the selector / version index (latest first)
latest: true # exactly one version should set this
status: "STABLE" # masthead STATUS cell while browsing this version
baseURL: "https://api.example.org/v2" # masthead BASE URL cell
---
```

Every page of a version without `latest: true` renders a notice banner with a
link to the same page in the latest version. To ship a new version, copy the
section (e.g. `docs/v2/` → `docs/v3/`), move `latest: true` to the new
`_index.md`, and adjust `status`/`baseURL`/`weight`.

Endpoint pages are ordered in the sidebar by their `weight` front matter.

## Authoring endpoints

Use the `endpoint` shortcode for the method/path bar, then a normal Markdown
table for parameters and a fenced block for the example:

```markdown
{{< endpoint method="POST" path="/v2/users" auth="required" />}}

| Parameter | In   | Type   | Required | Description     |
| --------- | ---- | ------ | -------- | --------------- |
| `email`   | body | string | yes      | Must be unique. |
```

The paired form adds an attached note under the bar:

```markdown
{{< endpoint method="GET" path="/v2/users" auth="required" />}}
Cursor pagination replaces page numbers, pass `cursor` from the previous response.
{{< /endpoint >}}
```

`{{< http "DELETE" />}}` renders a standalone method badge inline.

## Changelog entries

One file per entry under `content/changelog/` (any subfolder layout works —
entries are grouped by month from their `date`):

```yaml
---
title: "Machine-readable error codes"
description: "Shown on the changelog index."
date: 2026-07-10
tags: ["errors", "breaking"]
authors:
  - name: YouSysAdmin # map form: linked, optional image
    link: https://github.com/YouSysAdmin
  - "API Platform Team" # or a plain string
---
```

Entries newer than 30 days get a "New" badge on the index.

## Customizing

- **Colors / spacing / font** — edit the `:root` tokens at the top of
  `assets/css/main.css`. The theme bundles **[Space Mono](https://fonts.google.com/specimen/Space+Mono)** (Regular, Italic,
  Bold, BoldItalic WOFF2 in `static/fonts/`), falling back to system monospace
  fonts. To swap the face, replace the files, adjust the `@font-face` blocks at
  the top of `main.css`, and update the `--mono` token.
- **Masthead fields** — `[params]` in `hugo.toml` (`document`, `org`,
  `description`, plus `status`/`baseURL` fallbacks). `version` is only shown
  when the site has no versioned docs sections.
- **Sprocket holes** — set `sprocketHoles = false` in `[params]` to drop the
  tractor-feed margin decoration.
- **Section numbers** — auto-generated from `<h2>` via a CSS counter.
- **Per-page table of contents** — the "ON THIS PAGE" list shows by default on
  any page with `<h2>`+ headings. Set `toc: false` in a page's front matter to
  hide it there.
