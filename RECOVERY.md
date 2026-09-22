# Dr Jolie Website — Recovery and Replication Checklist

If you need to rebuild or recover this website from scratch, follow these steps.

## Step 1: Get the Code

```bash
git clone https://github.com/gavalos2394/Jolie.git
cd Jolie
```

Everything is in version control. All commits are on GitHub.

## Step 2: GitHub Pages Setup

1. Ensure you own or have access to **github.com/gavalos2394/Jolie**
2. Go to **Settings → Pages**
3. Set **Source** to **Deploy from a branch**
4. Set **Branch** to `main`, folder to `/ (root)`
5. Click **Save**

GitHub will create/update a `CNAME` file and deploy the site. It will appear at `https://gavalos2394.github.io/Jolie/` immediately (no certificate yet if custom domain not set).

## Step 3: Set Up Custom Domain (Optional)

You need a registered domain. This guide assumes **Cloudflare**.

### Buy the Domain

- Register `drjolie.com` (or your choice) at **Cloudflare** or transfer it to them
- Cloudflare will auto-configure DNS if you buy there

### Point GitHub at the Domain

1. In GitHub Pages settings, add the domain under **Custom domain** → enter `drjolie.com`
2. Click **Save**
3. GitHub commits a `CNAME` file; pull it locally: `git pull`
4. Wait for the Let's Encrypt certificate (up to 24 hours)
5. Once ready, tick **Enforce HTTPS**

### Verify DNS Records

In **Cloudflare → DNS → Records**, verify:

| Type | Name | Value | Status |
|---|---|---|---|
| A | @ | 185.199.108.153 | **DNS only** (grey) |
| A | @ | 185.199.109.153 | **DNS only** (grey) |
| A | @ | 185.199.110.153 | **DNS only** (grey) |
| A | @ | 185.199.111.153 | **DNS only** (grey) |
| CNAME | www | gavalos2394.github.io. | **DNS only** (grey) |

**All must be "DNS only" (grey cloud), not "Proxied" (orange).** If any are orange, the certificate won't issue.

Once DNS resolves and the certificate issues, `https://drjolie.com/` and `https://www.drjolie.com/` will both work, with automatic redirects.

## Step 4: Google Search Console (Optional but Recommended)

1. Go to **search.google.com/search-console**
2. Click **+ Create property**
3. Choose **Domain** (not URL prefix)
4. Enter `drjolie.com`
5. Google shows a TXT record to add

### Add the DNS Record

In **Cloudflare → DNS → Records → Add record:**
- Type: **TXT**
- Name: **@**
- Content: paste Google's verification string

Click **Add record**.

### Verify in Search Console

Go back to Search Console and click **Verify**. This usually works within a minute.

### Submit the Sitemap

1. In Search Console, go to **Sitemaps**
2. Click **Add/test sitemap**
3. Enter `sitemap.xml`
4. Click **Submit**

Status will show "Success" within a few minutes. Google will start crawling within a few days.

### Request Indexing

1. Go to **URL Inspection** (search bar at the top)
2. Paste `https://drjolie.com/`
3. Click **Request Indexing**

This nudges Google to crawl sooner. Expect the homepage in results within a week.

## Step 5: Make Changes and Deploy

Edit `index.html` locally:

```bash
# Edit index.html in your editor
git add index.html
git commit -m "Description of changes"
git push
```

The site updates within ~60 seconds. No build step, no deployment service needed.

## What If Something Goes Wrong?

### DNS Records Are Correct but Site Won't Load

- Check that **all A records and the CNAME are DNS only** (grey), not proxied (orange)
- Verify the DNS takes effect: `nslookup drjolie.com` should return the GitHub IPs (185.199.108–111.153)
- Force a refresh: `Ctrl+Shift+Del` (hard refresh), or open in a private window

### Certificate Not Issuing

- Ensure **all DNS records are DNS only**, not proxied
- Wait 24 hours (Let's Encrypt can be slow on first issue)
- In GitHub Pages settings, remove then re-add the custom domain to re-trigger

### Google Not Crawling

- Verify the sitemap in Search Console (it may take a few minutes to fetch)
- Request indexing on the homepage
- Wait at least a week; new domains are low priority
- Check **Coverage** in Search Console to see if any pages were excluded

## Files Needed for Recovery

| File | Purpose |
|---|---|
| `index.html` | The entire website |
| `assets/logo.png` | Clinic logo |
| `robots.txt` | Search engine instructions |
| `sitemap.xml` | Pages list for search engines |
| `README.md` | Quick start guide |
| `SETUP.md` | Full setup and deployment guide |
| `RECOVERY.md` | This file |
| `.gitignore` | Files to not version-control |
| `.git/` | Git history (created by `git clone`) |

Everything except `.git/` is on GitHub. All are needed for a working site.

## Backup

GitHub is the backup. Every commit is stored there forever. If your local copy breaks:

```bash
rm -rf Jolie
git clone https://github.com/gavalos2394/Jolie.git
```

And you're back to where you started.

## Questions?

Refer to `SETUP.md` for more detail on any section, or `README.md` for a quick overview.
