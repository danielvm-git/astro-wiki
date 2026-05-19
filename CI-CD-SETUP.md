# CI/CD Setup Guide

The GitHub Actions workflow is ready. The project builds cleanly (35 pages, ~700ms).
The only blocker is GitHub authentication — `gh` CLI is not logged in.

## What's already done

- `.github/workflows/deploy.yml` — Builds and deploys to GitHub Pages on push to `main`
- `netlify.toml` — Alternative Netlify deploy config (if you prefer Netlify)
- `public/.nojekyll` — Prevents GitHub Pages from ignoring underscore-prefixed files
- `gh-pages` npm package — Available as `npm run deploy` for manual deploys
- All 34 wiki pages integrated and building

## Option A: GitHub Pages (recommended)

Run these commands from the project directory:

```bash
cd /Users/danielvm/.hermes/kanban/boards/astro-wiki/workspaces/t_d983f830

# 1. Authenticate with GitHub
gh auth login
# Follow the prompts (HTTPS + browser auth is easiest)

# 2. Create a repo (or use an existing one)
gh repo create astro-wiki --public --source=. --remote=origin --push
# OR if the repo already exists:
# git remote add origin https://github.com/YOUR_USERNAME/astro-wiki.git
# git push -u origin main

# 3. Enable GitHub Pages (if not auto-enabled)
# Go to https://github.com/YOUR_USERNAME/astro-wiki/settings/pages
# Set Source = GitHub Actions

# 4. Verify — the Actions tab should show a running workflow
gh run list --workflow=deploy.yml
```

### If using a project repo (not username.github.io)

Edit `astro.config.mjs` and set the base path:

```js
export default defineConfig({
  base: '/astro-wiki',  // match your repo name
});
```

Then commit and push:
```bash
git add astro.config.mjs
git commit -m "fix: set base path for project repo"
git push
```

## Option B: Netlify

```bash
cd /Users/danielvm/.hermes/kanban/boards/astro-wiki/workspaces/t_d983f830

# 1. Install Netlify CLI
npm install -g netlify-cli

# 2. Authenticate
netlify login

# 3. Initialize and deploy
netlify init
netlify deploy --prod
```

Or manually:
1. Go to https://app.netlify.com
2. Click "Add new site" → "Import an existing project"
3. Connect to GitHub, select the repo
4. Build command: `npm run build`
5. Publish directory: `dist`

## Option C: Manual deploy via gh-pages

```bash
cd /Users/danielvm/.hermes/kanban/boards/astro-wiki/workspaces/t_d983f830
npm run deploy
```

This builds and pushes the `dist/` folder to the `gh-pages` branch.
You still need to configure GitHub Pages to deploy from the `gh-pages` branch
in repo settings.

## Verification

After pushing to `main`:
1. Go to the Actions tab on GitHub
2. You should see the "Deploy to GitHub Pages" workflow running
3. It should complete in ~1-2 minutes
4. The site will be live at `https://YOUR_USERNAME.github.io/astro-wiki/`
   (or `https://YOUR_USERNAME.github.io/` if using a user/org repo)

## Project location

The full project with git history is at:
```
/Users/danielvm/.hermes/kanban/boards/astro-wiki/workspaces/t_d983f830/
```

Commits:
- `1966a98` — Initial commit from Astro
- `f739ba0` — feat: add wiki content, CI/CD workflow, and Netlify config
- `14e6084` — chore: add gh-pages dev dependency and .nojekyll for GitHub Pages
