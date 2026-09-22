# Dr Jolie Beaute & Aesthetic Centre — Website

A fast, secure, single-file static website for an aesthetic clinic in Jordan, Hong Kong.

**Live:** https://drjolie.com

## Quick Start

```bash
git clone https://github.com/gavalos2394/Jolie.git
cd Jolie
```

Then open `index.html` in a browser to preview locally. To deploy changes, edit `index.html` and push to `main`:

```bash
git add index.html
git commit -m "Your change description"
git push
```

The site updates within 60 seconds.

## Structure

- **`index.html`** — The entire site (markup, CSS, JavaScript)
  - Five pages: Home, About, Services, Price List, Contact
  - Client-side hash routing (`#home`, `#about`, etc.)
  - No build step, no backend
- **`assets/`** — Logo and source artwork
- **`robots.txt`** & **`sitemap.xml`** — Search engine guidance
- **`SETUP.md`** — Full replication and deployment guide

## Hosting

**GitHub Pages** with a custom domain on **Cloudflare DNS**. Every push to `main` triggers a redeploy; HTTPS is automatic.

See [`SETUP.md`](SETUP.md) for full setup, DNS configuration, and troubleshooting.

## Features

- ✅ Responsive design (mobile-friendly)
- ✅ Fast (single HTML file, no build)
- ✅ Secure (HTTPS, no backend)
- ✅ Searchable (robots.txt, sitemap, Open Graph tags)
- ✅ Mobile menu, FAQ accordion, treatment price filter
- ✅ Contact form (pre-filled fields; form submission requires backend)

## Contact

- 📱 **Phone:** +852 6628 6127
- 💬 **WhatsApp:** https://wa.me/85266286127
- 📍 **Address:** Unit 1209, 12/F, 301-309 Nathan Rd, Jordan, HK
- 📸 **Instagram:** [@joliebeaute_hk](https://instagram.com/joliebeaute_hk)

---

For setup, deployment, and troubleshooting details, see [`SETUP.md`](SETUP.md).
