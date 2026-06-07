# flowmatos website

The marketing site for [flowmatos.com](https://flowmatos.com) — a pre-seed AI agent
platform for enterprise marketing workflow automation.

## Stack

- **Plain static HTML.** Every page is a self-contained `.html` file with inline CSS.
  No framework, no bundler, no build step.
- **Fonts:** Oxanium (display), Plus Jakarta Sans (body), JetBrains Mono (labels/code),
  loaded from Google Fonts.
- **Hosting:** Netlify, continuous deployment from this repository.
- **Forms:** Netlify Forms (early access, design partner, newsletter) — detected
  automatically from the form markup at deploy time.
- **Analytics:** Google Analytics (`G-N1VFZCN4S3`).

## There is no build

This is intentional. Files are served exactly as they sit in the repo.

- **Build command:** _(leave blank)_
- **Publish directory:** `.` (repository root)

If a Netlify deploy ever renders a blank page or 404s, the publish directory is the
first setting to check.

## Repository layout

```
.
├── index.html                  # Home
├── about.html
├── blog.html                   # Blog index (post cards live here)
├── blog-*.html                 # Individual blog posts
├── signalmint.html             # Product pages
├── campaignmint.html
├── reachmint.html
├── accountlens.html
├── sitemap.xml
├── robots.txt
└── og/                         # Open Graph preview images, one per page
```

## Workflow: edit → commit → push

Every push to the default branch triggers an automatic Netlify build and deploy.
Only changed files are uploaded; the rest of the site is untouched.

```bash
git clone https://github.com/hirenvp301/flowmatosweb.git
cd flowmatosweb

# make your edits ...

git add .
git commit -m "Describe the change"
git push
```

You can also edit directly in the GitHub web UI (Add file → Upload files, or the
pencil/edit button on any file) — same result, no local clone needed.

## Publishing a new blog post — checklist

1. Create `blog-<slug>.html` at the repo root. Start from an existing post to keep
   the nav, brand tokens, share bar, FAQ, and footer consistent.
2. Set the canonical URL, OG/Twitter meta, and Article + FAQPage JSON-LD to match
   the new slug and publish date.
3. Add a matching Open Graph image at `og/blog-<slug>.png`.
4. Add a post card to the `posts-grid` in `blog.html` (newest first), with
   appropriate `data-tags` so it picks up the tag filters.
5. Add a `<url>` entry for the post in `sitemap.xml`, and bump the `/blog`
   `lastmod` date.
6. Commit and push.

## Brand tokens

| Token        | Value     |
|--------------|-----------|
| Background   | `#050918` |
| Surface      | `#0D1428` |
| Border       | `#1A2A45` |
| Cyan         | `#00C8F8` |
| Violet       | `#6B21FF` |
| Amber        | `#FF5C35` |
| Text         | `#E8EEFF` |
| Muted        | `#6B7A99` |

Gradient: `linear-gradient(135deg, #00C8F8, #6B21FF)`

## Rollback

Every deploy is kept as a versioned snapshot in the Netlify **Deploys** tab. To revert,
publish a previous deploy — or `git revert` the offending commit and push.
