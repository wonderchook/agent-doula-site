# Agent Doula — Landing Page

A static pre-launch landing page for Agent Doula. Single HTML file, single CSS file, one photo, one Google Font. No build step, no JavaScript, no framework.

## Files

- `index.html` — the page
- `style.css` — all styles
- `kate.jpg` — founder portrait (rotated from the original; the original lives in the project root)
- `.nojekyll` — tells GitHub Pages not to run Jekyll processing

## Before you deploy: three things to do

### 1. Connect the email form to a real provider

Both `<form>` tags in `index.html` currently have `action="#"`, which means the form does nothing when submitted. Pick a provider and replace the action URL. Options in increasing order of commitment:

**Formspree** (quickest, free tier covers 50 submissions/month)
- Sign up at https://formspree.io, create a form, copy the endpoint URL
- Replace `action="#"` with `action="https://formspree.io/f/YOUR_FORM_ID"` in both places
- The form will email you each submission. You manually add them to your list until you pick a real email tool. Fine for the first hundred signups.

**Beehiiv / Substack / ConvertKit** (recommended for actual sequence delivery)
- These are email platforms that let you build the three-letter automated sequence directly.
- Each has its own embed code; you can either paste their embedded form (replacing the custom form markup) or use their API endpoint as the form action.
- If you go this route, also update the placeholder email and replace the form structure if their embed differs.

**Recommendation:** Start with Formspree for the first week (fast, no decision required), then migrate to your chosen email platform once you have the three letters uploaded and scheduled as an automation.

### 2. Add your Instagram handle

Find the footer in `index.html` and replace `href="#"` and `@agentdoula` with your real Instagram handle and link.

### 3. (Optional) Replace `kate.jpg` with your real headshot when it's ready

The current `kate.jpg` is a rotated copy of the photo you placed in the project root. When you have professional headshots taken, replace `kate.jpg` with the new file at ~360x360 pixels or larger (the CSS renders it at 180x180 and at 2x for retina displays).

## How to deploy to GitHub Pages

You have two reasonable options.

### Option A: Dedicated repo (recommended)

Create a new GitHub repository just for the landing page. This keeps it isolated from your thinking/planning docs and gives you a clean URL.

```bash
# From inside the agentdoula/site directory
git init
git add .
git commit -m "Initial Agent Doula landing page"

# Create a new repo on GitHub named "agent-doula-site" or similar
git remote add origin https://github.com/YOUR_USERNAME/agent-doula-site.git
git branch -M main
git push -u origin main
```

Then in GitHub:

1. Go to the repo's **Settings → Pages**
2. Under "Source," select **Deploy from a branch**
3. Choose branch: `main`, folder: `/ (root)`
4. Save

Your site will be live in 1-2 minutes at `https://YOUR_USERNAME.github.io/agent-doula-site/`.

### Option B: Subfolder of an existing repo

If you want to keep the site alongside the rest of the thinking/agentdoula project in one repo:

1. Initialize git at the project root (`agentdoula/`) if you haven't already
2. Push to GitHub as a new repo
3. In **Settings → Pages**, select source branch `main` and folder `/site`
4. The site will be served at `https://YOUR_USERNAME.github.io/REPO_NAME/`

Note: this exposes the `docs/` folder (canvas, letters, patterns) publicly in the repo. If that's a problem, use Option A.

## Custom domain (agentdoula.com or similar)

Once the site is live on GitHub Pages and you own a domain:

1. Create a file named `CNAME` (no extension) in the site root containing just your domain, e.g.:
   ```
   agentdoula.com
   ```
2. Commit and push.
3. At your domain registrar, add an A record or ALIAS/ANAME pointing to GitHub Pages IPs (see https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site).
4. In **Settings → Pages**, enter your custom domain and enable HTTPS.

## Local preview

To preview the site locally before pushing:

```bash
# From inside the site/ directory
python3 -m http.server 8000
```

Then open http://localhost:8000 in a browser. Or double-click `index.html` — the styles will load fine from file://, though the Google Font may take a moment.

## When you change copy

All copy lives in `index.html`. Edit in place. The source-of-truth copy (with drift detection and revision history) lives at `../docs/copy-tests/landing-page-full-2026-04-12.md`. When you change the live HTML, update that file too so future `/fw:copy` sessions stay grounded.

## Design notes

- **Font:** Lora (Google Fonts), 17px body, 1.7 line-height, max-width 640px. Designed for reading comfort.
- **Palette:** Warm off-white background (`#faf8f4`), soft dark text (`#2a2520`), muted brown accent (`#8b5a2b`).
- **No JavaScript.** Fast, accessible, works everywhere.
- **No tracking pixels.** Add your own if you need analytics, or skip them until you have real traffic worth measuring.
- **Mobile-first.** Tested mental model: reader on a phone, 90-second attention window.
