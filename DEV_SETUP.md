# Dev Environment Setup — reillyverse.au

This is a [Hugo](https://gohugo.io/) static site using the [hugo-scroll](https://github.com/zjedi/hugo-scroll) theme (loaded as a git submodule). It is deployed automatically to [reillyverse.au](https://reillyverse.au) via Netlify on every push to `main`.

---

## Prerequisites

| Tool | Version | Install |
|------|---------|---------|
| Hugo (extended) | Latest | `brew install hugo` |
| Git | Any modern | pre-installed on macOS |

> **Extended** edition is required because the theme uses SCSS. Verify you have the right edition with `hugo version` — the output should include `extended`.

---

## 1. Clone with submodules

The theme lives in `themes/hugo-scroll` as a git submodule. You must initialise it after cloning, otherwise Hugo will fail to build.

```bash
git clone https://github.com/ter942/reillyverse.au.git
cd reillyverse.au
git submodule update --init --recursive
```

If you already cloned without `--recursive`, run the submodule command from inside the repo directory.

---

## 2. Start the dev server

```bash
hugo server -D
```

- `-D` includes draft content so you can preview unpublished pages.
- The site will be available at `http://localhost:1313` and live-reloads on file changes.

---

## 3. Project structure

```
reillyverse.au/
├── hugo.toml              # Site config (base URL, theme, languages, params)
├── content/
│   ├── en/                # English content
│   │   └── homepage/      # Homepage sections (about, services, contact, etc.)
│   └── jp/                # Japanese content (同上)
├── assets/                # Favicon and other processed assets
├── static/                # Images and unprocessed static files
├── themes/
│   └── hugo-scroll/       # Theme (git submodule — do not edit directly)
├── public/                # Build output (generated, not committed)
└── resources/             # Hugo's image cache (generated, not committed)
```

---

## 4. Adding or editing content

All content is written in Markdown. The homepage is built from individual section files inside `content/en/homepage/` (and `content/jp/homepage/` for Japanese).

To add a new homepage section, create a `.md` file in the appropriate `homepage/` directory. Refer to existing files like `opener.md` or `about-me.md` for the front matter format used by the hugo-scroll theme.

---

## 5. Building for production

```bash
hugo
```

Output is written to `public/`. This is handled automatically by Netlify — you don't need to run this manually unless you want to inspect the build output locally.

---

## 6. Deployment

Netlify watches the `main` branch. Any push triggers a build and deploy automatically — no manual steps required. There is no `netlify.toml` in the repo, so the build command (`hugo`) and publish directory (`public`) must be configured in the Netlify dashboard.

---

## Troubleshooting

**"Error: module not found" or blank theme**
Run `git submodule update --init --recursive` — the theme submodule wasn't initialised.

**Hugo version error about SCSS**
Make sure you installed the **extended** edition. On Homebrew, `brew install hugo` installs extended by default. Confirm with `hugo version`.

**Port already in use**
Run `hugo server -D -p 1314` to use a different port.
