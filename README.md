# MyCommunity UAE — Website

A static site for mycommunityuae.com. Built to host the privacy policy, support page, and account deletion instructions required for App Store and Google Play submissions, plus a landing page and building-manager pitch section.

## Files

```
/
├── index.html              ← Landing page
├── privacy.html            ← Privacy policy
├── support.html            ← Support page
├── delete-account.html     ← Account deletion (required by Play)
├── CNAME                   ← GitHub Pages custom domain config
├── assets/
│   ├── styles.css          ← Shared styles
│   ├── icons/              ← App icons
│   └── screens/            ← App screenshots used on landing page
└── README.md
```

Pure static HTML + CSS. No build step. No JavaScript dependencies. Just upload to GitHub Pages and point your domain at it.

## Local preview

Just open `index.html` in a browser. Or run any static file server, e.g.:

```bash
python3 -m http.server 8000
# Then visit http://localhost:8000
```

## Deployment — GitHub Pages

### Step 1: Create the repo

1. On GitHub, create a new public repo. Recommended name: `mycommunityuae-site` (any name works).
2. Upload all these files to the root of the repo. Either drag-and-drop in the GitHub web UI, or use git:

```bash
git init
git remote add origin https://github.com/YOURUSER/mycommunityuae-site.git
git add .
git commit -m "Initial site"
git branch -M main
git push -u origin main
```

### Step 2: Enable Pages

1. In the repo, go to **Settings → Pages**.
2. Under "Build and deployment", set:
   - **Source:** Deploy from a branch
   - **Branch:** `main`, folder `/ (root)`
3. Click **Save**. The site will be live at `https://YOURUSER.github.io/mycommunityuae-site/` in 1-2 minutes.

### Step 3: Custom domain

1. Still in **Settings → Pages**, scroll to "Custom domain".
2. Enter `www.mycommunityuae.com` and click **Save**.
3. GitHub will check the DNS — it'll fail until you do step 4.

### Step 4: Point GoDaddy DNS at GitHub

Log into GoDaddy and open the DNS management for `mycommunityuae.com`.

Add these records (you can leave any unrelated existing records alone, but **remove or update** any conflicting A/CNAME records pointing at Replit):

**For the apex domain (mycommunityuae.com → redirects to www):**

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | `185.199.108.153` | 1 hour |
| A | @ | `185.199.109.153` | 1 hour |
| A | @ | `185.199.110.153` | 1 hour |
| A | @ | `185.199.111.153` | 1 hour |

**For the www subdomain (the canonical URL):**

| Type | Name | Value | TTL |
|------|------|-------|-----|
| CNAME | www | `YOURUSER.github.io` | 1 hour |

Replace `YOURUSER` with your actual GitHub username.

### Step 5: Wait + verify

- DNS propagation takes 5 minutes to an hour. Sometimes longer.
- Go back to **GitHub repo → Settings → Pages**. The DNS check should turn green.
- Enable **Enforce HTTPS** (checkbox below the custom domain field). GitHub will auto-provision a Let's Encrypt certificate once DNS is verified.
- Visit `https://www.mycommunityuae.com` — your site should load.

That's it. Total work: 20 minutes including DNS propagation time.

## What about the Replit site?

Once GitHub Pages is live and verified, you can either:

- **Decommission Replit** — change the DNS records (above), and the Replit site stops being reachable from your domain. Keep the Replit project if you want, just don't pay for it.
- **Move things over gradually** — keep Replit live for now, and only switch DNS when you're confident the new site is right.

I'd recommend the first option since this site already covers everything you need for store listings.

## Editing the site

Every page is a self-contained `.html` file. Open in any text editor, make your change, push to GitHub. Pages auto-deploys in 30-60 seconds.

Common edits:

- **Email address:** search the repo for `hello@mycommunityuae.com` to find all references
- **Phone number:** search for `971567874381`
- **Last updated dates:** in the prose footer of each content page
- **Screenshots:** drop new files into `assets/screens/` and update the `<img src=>` paths in `index.html`
- **Copy:** all the visible text is in the HTML files directly. No CMS, no database.

## What's required for store submission (recap)

When you submit to App Store / Google Play, you'll need to provide these URLs in the listing:

- **Privacy policy URL:** `https://www.mycommunityuae.com/privacy.html`
- **Support URL:** `https://www.mycommunityuae.com/support.html`
- **Account deletion URL (Play, required):** `https://www.mycommunityuae.com/delete-account.html`

If you prefer cleaner URLs without `.html`, that's possible but requires a slightly more complex setup (Jekyll, or a `_redirects` file). Not necessary — Apple and Google accept the `.html` URLs without issue.
