# Deploying the Clean Data Labs landing page

**Status (America/Denver, 10 Nov 2026):** This site is published at https://clean-data-labs-org.github.io/ from the public repo `clean-data-labs-org/clean-data-labs-org.github.io`, `main` branch, site root. The steps below are what was used, and how to update or republish later.


The site is a static folder: `index.html`, `404.html`, `robots.txt`, `.nojekyll`, and `assets/`. No build step, no environment variables, no forms, no third-party scripts.

**Live URL (once published):** https://clean-data-labs-org.github.io/

Do not point this page at a `cleandatalabs.com` domain. That domain is not claimed here.

## Recommended: GitHub Pages under clean-data-labs-org

Create a public repo named `clean-data-labs-org.github.io` in the `clean-data-labs-org` organization. GitHub serves that repo at `https://clean-data-labs-org.github.io/`.

From this `landing/` directory, after reviewing the page:

```bash
# Create the repo (skip if it already exists)
gh repo create clean-data-labs-org/clean-data-labs-org.github.io --public

# First push
git init
git checkout -b main
git add index.html 404.html robots.txt README.md DEPLOY.md .nojekyll assets
git commit -m "Add Clean Data Labs landing page"
git remote add origin https://github.com/clean-data-labs-org/clean-data-labs-org.github.io.git
git push -u origin main

# Enable Pages from main, site root
gh api -X POST repos/clean-data-labs-org/clean-data-labs-org.github.io/pages \
  -f 'source[branch]=main' -f 'source[path]=/'
```

If the repo already exists, just push to `main`.

Pages usually goes live within a minute or two. Confirm with:

```bash
curl -sI https://clean-data-labs-org.github.io/
curl -s https://clean-data-labs-org.github.io/ | grep -F "See the SAM.gov opportunities that fit you, hand-checked."
```

A first-time Pages enable can take a little longer and may return 404 until DNS and the Pages build finish. Wait and retry. The site is ready when the response is HTTP 200 and the homepage HTML includes the headline.

To update later, edit files and `git push origin main`. Do not push this site into `samgov-opportunities-mcp`.

## Alternatives

If GitHub Pages cannot be used, these are equivalent free static hosts. Upload this same folder (keep `index.html` at the root).

### Netlify

1. Sign in at [netlify.com](https://www.netlify.com/) (the Clean Data Labs GitHub org can be connected, or the folder can be dragged onto the “deploy manually” drop zone).
2. Create a new site from this repo, or drop the `landing/` folder.
3. Set the publish directory to the folder that contains `index.html` (the repo root, if this repo is used).
4. The default URL will look like `https://<site-name>.netlify.app`. That is fine for a first publish; do not attach a `cleandatalabs.com` domain.

### Cloudflare Pages

1. Sign in at [Cloudflare Pages](https://pages.cloudflare.com/) and create a project.
2. Connect the `clean-data-labs-org/clean-data-labs-org.github.io` repo, or upload the `landing/` folder.
3. Build command: leave empty. Output directory: `/` (or the folder that contains `index.html`).
4. The default URL will look like `https://<project>.pages.dev`.

## After it is live

- Open the homepage and a `?r=test-a` URL in a browser. The “Request a free sample” links should become `mailto:...` with subject `Free sample request [r=test-a]`.
- Check the page on a phone-width screen.
- LinkedIn and X profile links in the footer should resolve.
