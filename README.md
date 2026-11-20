# ReSteep website

The documentation site for [ReSteep](https://github.com/resteepMod/ReSteep), published at
<https://resteepmod.github.io/>. Built with [Hugo](https://gohugo.io) and the
[Hugo Book](https://github.com/alex-shpak/hugo-book) theme (a git submodule in `themes/hugo-book`, pinned to a release).

## Working on it

```
git clone --recurse-submodules https://github.com/resteepMod/resteepmod.github.io
cd resteepmod.github.io
hugo server            # http://localhost:1313/, reloads as you edit
```

You need Hugo 0.158 or newer (CI uses the version in `.github/workflows/pages.yml`).

- Pages are Markdown in `content/docs/<section>/`. Each has `title` and `weight` (its place in the menu) in its front
  matter and starts with a `# Heading`.
- Link to other pages by their file path, e.g. `[Mods](../mods/_index.md)` or `[Hosting](../hosting/admin.md#bans)`:
  Hugo Book checks these links and warns about broken ones (CI fails on warnings).
- Notes and warnings: GitHub's alerts (`> [!NOTE]`, `> [!TIP]`, `> [!IMPORTANT]`, `> [!WARNING]`, `> [!CAUTION]`).
  Tabs, details and more: [Hugo Book's shortcodes](https://github.com/alex-shpak/hugo-book#shortcodes).
- Colours and the landing page's style: `assets/styles/custom.css`. The landing page is `content/_index.md`.

The pages describe the released ReSteep for players, hosts and mod makers. The ReSteep repository's `docs/` stays the
detailed reference (every field and command); when something there changes for players, update the page here too.

## Publishing

Every push to `main` builds the site and deploys it to GitHub Pages (`.github/workflows/pages.yml`). The repository's
**Settings → Pages → Source** must be **GitHub Actions**.

To update the theme: `cd themes/hugo-book && git fetch --tags && git checkout <new tag>`, check the site with
`hugo server`, then commit the submodule.
