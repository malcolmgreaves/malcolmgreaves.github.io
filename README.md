# malcolmgreaves.github.io

Personal website, built with [Jekyll](https://jekyllrb.com/) and hosted for free
on [GitHub Pages](https://pages.github.com/). It uses the
[midnight](https://github.com/pages-themes/midnight) theme with a custom layout
that adds site-wide navigation.

## Site structure

```
_config.yml          Site settings + the navigation menu (the `nav:` list)
_layouts/
  default.html       Page shell: midnight theme + nav bar
  post.html          Layout for blog posts
_posts/              Blog posts (YYYY-MM-DD-title.md)
index.md             Home page          → /
about.md             About page         → /about
projects.md          Projects page      → /projects
blog.md              Blog post listing  → /blog
links.md             Hosted files/links → /links
```

To add, rename, or reorder menu items, edit the `nav:` list in `_config.yml` —
the layout renders the menu from that data, so you don't touch any HTML.

## Local development

### Prerequisites

This project pins its Ruby version in `.tool-versions` and uses
[mise](https://mise.jdx.dev/) to manage it — the same way `uv` or `pyenv` manage
Python versions. One-time machine setup:

```bash
brew install mise
echo 'eval "$(mise activate zsh)"' >> ~/.zshrc   # restart your shell afterwards
```

Then, from this project directory:

```bash
mise install    # installs the pinned Ruby (reads .tool-versions)
```

mise auto-switches to the pinned Ruby whenever you `cd` into the project, so
there's no env to manually activate or deactivate. Bundler ships with Ruby, so
nothing else needs installing — `./dev setup` handles the gems.

> **Mental model (coming from Python):** `mise` ≈ `uv`'s Python-version
> management, the `Gemfile`/`Gemfile.lock` ≈ `pyproject.toml`/`uv.lock`, and
> Bundler installing into `./vendor/bundle` ≈ the project's virtualenv. `bundle
> exec <cmd>` ≈ running a command inside the activated venv.

> **Not using mise?** Any tool that reads `.tool-versions` works (e.g. `asdf`),
> or just install Ruby 3.3 yourself (`brew install ruby@3.3`).

### Quickstart

```bash
./dev setup     # install dependencies (one-time)
./dev serve     # build + serve at http://127.0.0.1:4000 with live reload
```

`serve` rebuilds automatically as you edit and refreshes the browser.

### The `dev` script

`./dev <command>` manages the full lifecycle:

| Command | Description |
|---------|-------------|
| `setup`  | Install Ruby gems into `./vendor/bundle` (one-time) |
| `serve`  | Build and serve locally with live reload |
| `build`  | Build the static site into `./_site` (production mode) |
| `clean`  | Remove generated files and caches |
| `doctor` | Check that Ruby, Bundler, and gems are available |
| `help`   | Show usage |

`serve`, `build`, and `clean` will run `setup` automatically if dependencies
aren't installed yet.

## Adding content

### A blog post

Create a file in `_posts/` named `YYYY-MM-DD-title.md`:

```markdown
---
layout: post
title: "My First Post"
date: 2026-06-24
---

Post content here.
```

It appears on `/blog` automatically, newest first.

### A new page

Create a Markdown file in the project root with front matter:

```markdown
---
layout: default
title: Talks
permalink: /talks
---

## Talks
```

Then add it to the `nav:` list in `_config.yml` if you want it in the menu.

## Deployment

GitHub Pages builds and deploys automatically on every push to `main` — there's
no separate deploy step. The local toolchain (via the `github-pages` gem in the
`Gemfile`) matches GitHub's build environment, so a successful `./dev build`
locally reflects what gets published.
