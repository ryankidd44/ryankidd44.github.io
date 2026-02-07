# Ryan Kidd - Personal Site

A clean, minimalist personal website built with Jekyll.

## Migration from Jekyll Now

To update your existing site with this new design:

### Quick Method (recommended)

1. **Backup your current repo** (just in case)
   ```bash
   git clone https://github.com/ryankidd44/ryankidd44.github.io.git ryankidd-backup
   ```

2. **Replace/add these files:**

   | File/Folder | Action |
   |-------------|--------|
   | `_layouts/default.html` | Replace |
   | `_layouts/post.html` | Replace |
   | `_layouts/page.html` | Add (new) |
   | `assets/css/main.css` | Add (new folder + file) |
   | `_data/` folder | Add (new) |
   | `index.html` | Replace |
   | `about.md` | Replace (keep your content) |
   | `talks.html` | Add |
   | `publications.html` | Add |
   | `notes.html` | Add |
   | `contact.html` | Add |
   | `_config.yml` | Update (merge with yours) |

3. **Delete old style files:**
   - `style.scss`
   - `_sass/` folder (the old one)

4. **Update `_config.yml`** with your actual info:
   - email
   - twitter_username
   - lesswrong_username
   - linkedin_username

5. **Populate the data files** in `_data/`:
   - `featured.yml` - Homepage featured items
   - `talks.yml` - Your talks and podcasts
   - `publications.yml` - Your papers and essays
   - `notes.yml` - Quick posts, tweets, FB posts
   - `positions.yml` - Board/advisory positions

6. **Commit and push:**
   ```bash
   git add .
   git commit -m "Redesign site"
   git push
   ```

Your site will rebuild automatically on GitHub Pages.

---

## File Structure

```
├── _config.yml          # Site configuration
├── _data/
│   ├── featured.yml     # Homepage featured items
│   ├── talks.yml        # Talks & presentations
│   ├── publications.yml # Papers & essays
│   ├── notes.yml        # Quick posts & tweets
│   └── positions.yml    # Board/advisory roles
├── _layouts/
│   ├── default.html     # Base layout
│   ├── post.html        # Blog post layout
│   └── page.html        # Static page layout
├── _posts/              # Your blog posts (keep existing)
├── assets/
│   └── css/
│       └── main.css     # All styles
├── images/              # Your images (keep existing)
├── index.html           # Homepage
├── about.md             # About page
├── talks.html           # Talks page
├── publications.html    # Publications page
├── notes.html           # Notes page
└── contact.html         # Contact page
```

---

## Adding Content

### Blog Posts (in `_posts/`)

Create markdown files like `2024-01-15-post-title.md`:

```markdown
---
layout: post
title: "Your Post Title"
description: "Brief description for previews"
category: publication  # or 'note' for shorter posts
tags:
  - AI Safety
  - Field Building
---

Your content here...
```

### External Publications (in `_data/publications.yml`)

```yaml
- title: "Your Paper Title"
  date: "2024"
  url: "https://lesswrong.com/..."
  description: "Brief description."
  source: "LessWrong"
  tags:
    - "AI Safety"
```

### Talks (in `_data/talks.yml`)

```yaml
- title: "Podcast/Talk Title"
  date: "2024"
  url: "https://..."
  description: "Brief description."
  type: "Podcast"
  tags:
    - "Field Building"
```

---

## Customization

### Colors

Edit the CSS variables in `assets/css/main.css`:

```css
:root {
    --accent: #b44d2d;        /* Main accent color */
    --bg-primary: #faf9f7;    /* Background */
    /* ... */
}
```

### Fonts

Change the Google Fonts import in `_layouts/default.html` and update `--font-serif` / `--font-sans` in the CSS.

---

## Local Development

```bash
gem install bundler jekyll
bundle install
bundle exec jekyll serve
```

Visit `http://localhost:4000`
