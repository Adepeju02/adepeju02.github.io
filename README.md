# Morenikeji "PJ" Adeleke — Cybersecurity Portfolio

Portfolio site built with Jekyll and the Minimal Mistakes theme, deployed via GitHub Pages.

## Quickstart

The site lives in the `docs/` folder.

### Local development
```bash
cd docs
bundle install
bundle exec jekyll serve
```
Then open http://localhost:4000

### Deploying to GitHub Pages
1. Push the repo to GitHub
2. Go to Settings → Pages → Source → select `main` branch, `/docs` folder
3. Your site will be live at `https://adepeju02.github.io`

## Customise

### Fill in your details
- `docs/_config.yml` — update LinkedIn URL, email, GitHub username, site URL
- `docs/_pages/contact.md` — replace `YOUR_FORM_ID` with your [Formspree](https://formspree.io) form ID
- `docs/_pages/resume.md` — fill in `[X]` metric placeholders and employment dates
- `docs/_pages/projects.md` — fill in `[X]` placeholders with real metrics
- `docs/assets/` — add your actual resume PDF as `Adeleke_Morenikeji_Cybersecurity_Resume.pdf`

### Add project screenshots
Drop screenshots (1200×675px PNG recommended) into `docs/assets/images/projects/`.
See `docs/assets/images/projects/README.md` for the full list of filenames.

### Add a write-up / blog post
Create a new file in `docs/_posts/` named `YYYY-MM-DD-title.md` with this front matter:
```yaml
---
title: "Your Write-up Title"
categories:
  - writeups
tags:
  - penetration-testing
  - SIEM
---
```

## Site structure

```
docs/
├── _config.yml          # Theme, author, SEO, navigation
├── _data/
│   └── navigation.yml   # Top navigation menu
├── _pages/
│   ├── about.md
│   ├── contact.md
│   ├── projects.md
│   └── resume.md
├── assets/
│   ├── css/
│   │   └── style.scss   # Custom overrides
│   └── images/
│       ├── avatar.png
│       └── projects/    # Drop screenshots here
├── index.md             # Home page
└── Gemfile
```
