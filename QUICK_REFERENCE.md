# Dr Jolie Website — Quick Reference Card

For common tasks and one-liners.

## Deploy a Change

```bash
# Edit index.html
git add index.html
git commit -m "Your change description"
git push
```

**Live in ~60 seconds.** No build, no extras needed.

## Preview Locally

1. Open `index.html` in a browser, or
2. Run a local server: `python -m http.server 8000`, then visit `http://localhost:8000`

## View All Commits

```bash
git log --oneline
```

## Revert a Commit

```bash
git revert <commit-hash>
git push
```

(This creates a new commit that undoes the old one — safer than resetting.)

## Check Site Status

- **Live site:** https://drjolie.com/
- **GitHub repo:** https://github.com/gavalos2394/Jolie
- **GitHub Pages settings:** https://github.com/gavalos2394/Jolie/settings/pages
- **Google Search Console:** https://search.google.com/search-console
- **Cloudflare DNS:** https://dash.cloudflare.com/ → drjolie.com

## Edit the Website

Everything is in `index.html`:

- **HTML:** Markup starting around line 143
- **CSS:** `:root` variables define colors; styles start around line 20
- **JavaScript:** Event handlers start around line 883

The file is single-paged (`#home`, `#about`, etc. for navigation), so there's no multiple-file structure.

## Add a Image or Asset

1. Place the file in `assets/` subfolder
2. Reference it in HTML: `<img src="assets/myimage.png" />`
3. Commit and push

The path is relative to the site root, so it works on both `localhost` and `drjolie.com`.

## Update the Logo

1. Replace `assets/logo.png` with a new 256×256 PNG (transparent background works best)
2. Optionally replace `assets/source/logo-original.jpg` with the original artwork
3. Commit and push

The logo appears in the header, footer, and browser tab automatically.

## Contact Info

All in `index.html`:

- **Phone:** +852 6628 6127 (search `6628 6127`)
- **WhatsApp:** wa.me URL (search `wa.me`)
- **Instagram:** @joliebeaute_hk (search `joliebeaute_hk`)
- **Address:** Jordan, Hong Kong (search `Nathan Rd` or `Jordan`)

## Fix a Typo

1. Edit `index.html`
2. Search for the text you want to change
3. Update it
4. Commit and push

Changes go live in ~60 seconds.

## Emergency: Revert to Yesterday's Version

```bash
git log --oneline   # Find yesterday's commit hash
git revert <hash>   # Creates a new commit undoing it
git push
```

Or if you need to go back further:

```bash
git log --all --decorate --oneline --graph
git revert <hash>
git push
```

## Troubleshooting

| Problem | Check |
|---|---|
| Site not updating after push | Refresh browser (Ctrl+Shift+Delete), wait 60 sec, check `git push` succeeded |
| Domain not loading | Verify DNS records in Cloudflare are all **DNS only** (grey), not proxied (orange) |
| Certificate error | Wait 24 hours after setting custom domain; check all DNS records are grey |
| Google still not showing the site | Submit sitemap in Search Console, request indexing, wait 1–2 weeks |

For detailed troubleshooting, see `SETUP.md` or `RECOVERY.md`.

## File Sizes

| File | Size | Role |
|---|---|---|
| `index.html` | ~970 KB | The site |
| `assets/logo.png` | ~19 KB | Clinic logo |
| `assets/source/logo-original.jpg` | ~20 KB | Original artwork |
| `robots.txt` | <1 KB | Search engine instructions |
| `sitemap.xml` | <1 KB | Pages list |
| `CNAME` | 11 bytes | Custom domain pointer |

Total: ~1 MB. A fast network downloads the entire site in milliseconds.

## The Clinic

- **Name:** Dr Jolie Beaute & Aesthetic Centre
- **Location:** Unit 1209, 12/F, 301-309 Nathan Rd, Jordan, Hong Kong
- **Phone:** +852 6628 6127
- **Services:** Botox, fillers, Profhilo, facials, IPL, laser, waxing
- **Hours:** (Check the website or call)

## Support

- **Quick questions:** Check the relevant section in this file or `README.md`
- **Setup help:** See `SETUP.md`
- **Full recovery:** See `RECOVERY.md`
- **Code details:** Comments in `index.html`
