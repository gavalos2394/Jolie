# Dr Jolie Website — Setup and Replication Guide

This guide documents how to set up or replicate this website. Last updated: 2026-09-22.

## What This Is

A single-file static website for Dr Jolie Beaute & Aesthetic Centre, Hong Kong. One HTML file, one CSS stylesheet, client-side hash routing for five pages (home, about, services, price list, contact). No build step, no backend.

**Live at:** https://drjolie.com

## File Structure

```
.
├── index.html              # The entire site (single-page app)
├── assets/
│   ├── logo.png           # Clinic logo (256×256, circular, transparent bg)
│   └── source/
│       └── logo-original.jpg  # Original artwork from Downloads
├── robots.txt             # Search engine crawling instructions
├── sitemap.xml            # List of pages for search engines
├── CNAME                  # Custom domain (created by GitHub Pages)
├── netlify.toml           # Unused; Netlify account was blocked
└── .gitignore             # Standard OS/editor ignores
```

## Hosting: GitHub Pages + Cloudflare DNS

The site runs on **GitHub Pages** and is accessed via a custom domain on **Cloudflare DNS**.

### GitHub Pages Setup

1. **Repository:** `github.com/gavalos2394/Jolie` (public)
2. **Branch:** `main` — pushed here auto-deploys to `https://gavalos2394.github.io/Jolie/` within 60 seconds
3. **Custom domain:** `drjolie.com` via GitHub Pages settings → adds a `CNAME` file to the repo
4. **HTTPS:** Let's Encrypt certificate, auto-issued and renewed
5. **Enforce HTTPS:** Enabled — all traffic redirects to `https://`

Every `git push` to `main` triggers a redeploy. No build step, no secrets needed.

### Cloudflare DNS Configuration

Domain registered and DNS hosted on **Cloudflare**. Records (all with **DNS only** toggled, not proxied):

| Type | Name | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | gavalos2394.github.io. |

**Critical:** Every A record and the CNAME must be set to **DNS only** (grey cloud icon in Cloudflare). Leaving any one on "Proxied" (orange) breaks GitHub's domain verification and prevents certificate issuance.

Apex domain (`drjolie.com`) automatically redirects to `www.drjolie.com`, and `www` redirects back to the apex — GitHub handles the redirect.

### Why Not Netlify?

Netlify (`netlify.toml` exists but unused) had its anti-spam system auto-block the user's account at signup on 2026-09-21. This is a known false positive; accounts can be appealed via `support@netlify.com`. GitHub Pages was used instead.

## Google Search Console

**Property type:** Domain (covers `www`, apex, both `http://` and `https://`)  
**Verification method:** DNS TXT record  
**Status:** Verified 2026-09-21  

To re-verify or set up in a new account:
1. Go to **search.google.com/search-console**
2. Add property → Domain → enter `drjolie.com`
3. Copy the TXT record from Google
4. Add to Cloudflare DNS (same way as above)
5. Verify in Search Console

Once verified, submit the sitemap at **Sitemaps** → `sitemap.xml`. Google will crawl within a few days.

## If You Need to Replicate This

### 1. Clone the Repository

```bash
git clone https://github.com/gavalos2394/Jolie.git
cd Jolie
```

### 2. Set Up GitHub Pages

- Go to **github.com/gavalos2394/Jolie → Settings → Pages**
- **Source:** Deploy from a branch
- **Branch:** `main`, folder `/ (root)`
- Save → GitHub creates/updates a `CNAME` file

After saving, the site will be live at `https://gavalos2394.github.io/Jolie/` (or your custom domain if you add one).

### 3. Optional: Add a Custom Domain

- Buy a domain from **Cloudflare** (or another registrar)
- If Cloudflare: no extra setup needed, domain is auto-configured
- If elsewhere: update nameservers to Cloudflare's or add A records manually (see DNS table above)
- In GitHub Pages settings, add the domain under **Custom domain**
- GitHub adds/updates the `CNAME` file; pull the changes: `git pull`
- Wait for the Let's Encrypt certificate (up to 24 hours)
- Enable **Enforce HTTPS** once available

### 4. Optional: Register with Google Search Console

- Verify the domain via DNS TXT (see section above)
- Submit the sitemap
- Request indexing on the homepage via **URL Inspection**
- Wait for Google to crawl (days to a couple of weeks)

### 5. Deploy Changes

```bash
# Make changes to index.html
git add index.html
git commit -m "Description of changes" -m "Co-Authored-By: Claude Haiku 4.5 <noreply@anthropic.com>"
git push
```

Site updates within ~60 seconds.

## Known Constraints and Future Work

- **Single-page structure:** The whole site is one URL to Google, so it won't rank separately for specific treatments (e.g., "Profhilo Hong Kong"). Real separate pages would fix this but need a proper rebuild.
- **Stock photography:** 18 of 20 images are Unsplash hotlinks. Replace with real clinic photos for credibility.
- **No backend:** No contact form database, no email notifications. Form submissions go nowhere. (Can be added via a third-party service like Formspree if needed.)
- **Untracked files:** `docs/2026-09-09-dr-jolie-prices.xlsx` is in `.gitignore` because the repo is public and it's an internal pricing sheet.

## Mobile Menu, FAQ, Price Filter — They Work Now

Three features were broken by a script error (line 793: calling a function before its variables were declared). This was fixed by reordering the JavaScript. They now work:

- Mobile menu (burger button on phones)
- FAQ accordion (expand/collapse questions)
- Price list filter (filter by treatment category)

See commit `5ca26d7` for the fix.

## Metadata and Social Sharing

The site includes:

- **Open Graph tags** (`og:title`, `og:description`, `og:url`, `og:image`, `og:site_name`)
- **Canonical URL** (points to `https://drjolie.com/`)
- **Twitter card** metadata
- **Favicon** (the clinic logo in the browser tab)
- **robots.txt** and **sitemap.xml** for search engines

These ensure link previews on WhatsApp and Instagram render properly, and help search engines understand the site.

## Contact Info in the Site

- **Phone:** +852 6628 6127
- **WhatsApp:** https://wa.me/85266286127
- **Instagram:** @joliebeaute_hk
- **Address:** Unit 1209, 12/F, 301-309 Nathan Rd, Jordan, HK

All clickable from the Contact page and footer.

## Questions or Issues?

- **GitHub Pages not updating:** Check that `main` is the source branch and the `CNAME` file is present.
- **Certificate not issuing:** Verify DNS records are all **DNS only**, not proxied.
- **Google not crawling:** Verify the sitemap in Search Console, wait a few days, then request indexing on the homepage.
- **Mobile menu / filter buttons not working:** Check browser console for JS errors; the fix is in commit `5ca26d7`.
