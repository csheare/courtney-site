# courtneyshearer.com — Hugo Site

A clean, minimal personal academic website built with Hugo.

## Quick Start

### Prerequisites
- [Hugo](https://gohugo.io/installation/) (extended edition recommended)
- Git

### Local Development

```bash
cd courtney-site
hugo server -D
# Open http://localhost:1313
```

### Deploying to GitHub Pages

1. Create a repo named `csheare.github.io` (or your username)
2. Push this folder to that repo
3. Add this GitHub Actions workflow at `.github/workflows/hugo.yml`:

```yaml
name: Deploy Hugo site
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: 'latest'
      - run: hugo --minify
      - uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

4. In your repo Settings → Pages → Source: select `gh-pages` branch

---

## Customizing Content

### Update Your Bio
Edit `layouts/index.html` — find the bio paragraph and update the text.

### Add a Profile Photo
Place your photo at `static/img/prof_pic.jpg`

### Add News Items
Edit `data/news.yaml`:
```yaml
- date: "Mar 2024"
  text: "Your news item here. Supports **markdown**."
```

### Add a Blog Post

```bash
hugo new content blog/my-post-title.md
```

Then edit the file — set `tags: ["science"]` or `tags: ["sewing"]` in the front matter.

**Front matter template:**
```yaml
---
title: "My Post Title"
date: 2024-03-01
tags: ["science"]   # or "sewing"
summary: "One sentence teaser shown on the blog index."
---

Your post content in Markdown here.
```

### Add a Research Entry

Create a file in `content/research/paper-slug.md`:
```yaml
---
title: "Full Paper Title"
date: 2024-01-01
venue: "NeurIPS 2024"
authors: "**Courtney A. Shearer**, Co-Author Name"
abstract: "One paragraph summary."
paper: "https://arxiv.org/abs/..."
code: "https://github.com/..."
---
```

### Update Your CV
Edit `content/cv.md` — uses HTML with the `.cv-entry` class for the two-column date/description layout.

### Update Publications
Edit `content/publications.md` — duplicate the `.research-item` div block for each paper.

---

## Design Tokens (colors, fonts)

All design variables are in `static/css/main.css` under `:root {}`:

```css
:root {
  --bg: #faf9f7;          /* page background */
  --text: #1a1a1a;        /* body text */
  --muted: #888;          /* labels, dates */
  --accent: #c46e3c;      /* rust orange — hover states, italic name */
  --border: #e8e4de;      /* dividers */
}
```

Change `--accent` to any color to shift the whole site's personality.

**Fonts used:**
- Body: `EB Garamond` (elegant serif for headings/names)
- UI: `DM Sans` (clean sans-serif for nav and body text)

Both load from Google Fonts — swap in `layouts/_default/baseof.html`.
