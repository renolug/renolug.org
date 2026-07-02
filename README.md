# renolug.org

Website for the **Reno Linux Users Group (RLUG)**, built with
[Hugo](https://gohugo.io) and deployed to Cloudflare Pages.

## Requirements

- [Hugo **extended**](https://gohugo.io/installation/) — v0.161.x or newer
  (the extended edition is required for the CSS pipeline).

## Local development

```sh
hugo server
```

Then open <http://localhost:1313>. The server live-reloads on changes.

To include future-dated or draft content while previewing:

```sh
hugo server -D -F
```

## Build

```sh
hugo --gc --minify
```

Output is written to `public/` (git-ignored).

## Project layout

```
content/            Markdown pages (home, meetings, about, contact, resources)
layouts/            Custom, self-contained theme (no external theme dependency)
  _default/         baseof, single, list templates
  partials/         head, header, footer, sponsors
  shortcodes/       {{< sponsors >}}
assets/css/         main.css (processed via Hugo Pipes)
data/sponsors.toml  Sponsor list that drives the sponsor grid
static/             Files copied verbatim (CNAME, favicon, images)
  img/sponsors/     Sponsor logos
.github/workflows/  CI that builds and deploys to GitHub Pages
```

## Common edits

- **Add a sponsor:** add a `[[sponsor]]` block to `data/sponsors.toml` and drop
  the logo in `static/img/sponsors/`. Use `tier = "primary"` to render it
  larger. No template changes needed.
- **Update meeting details:** edit `content/meetings.md`.
- **Change contact/social links:** edit the `[params.links]` section in
  `hugo.toml`.
- **Add a nav item:** add a `[[menus.main]]` block in `hugo.toml`.

## Deployment

The site is hosted on [Cloudflare Pages](https://pages.cloudflare.com/).
Every push to `main` triggers `.github/workflows/deploy.yml`, which builds the
site with Hugo and deploys the `public/` output to the Cloudflare Pages project
`renolug` via [wrangler](https://developers.cloudflare.com/workers/wrangler/).
Pull requests get preview deployments automatically.

To deploy manually from your machine:

```sh
hugo --gc --minify
npx wrangler pages deploy public --project-name=renolug
```
