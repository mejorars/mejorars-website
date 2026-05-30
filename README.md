# Mejorars Website

The complete launch-ready website for Mejorars Creative Studio.

## What's in this folder

```
mejorars-launch/
├── index.html         # Main site (single-file, ~50KB)
├── 404.html           # On-brand "lost in space" 404 page
├── favicon.svg        # Magenta-dot favicon
├── robots.txt         # Search crawler instructions
├── sitemap.xml        # Search engine sitemap
├── netlify.toml       # Netlify deployment config (headers, caching)
├── vercel.json        # Vercel deployment config (alternative to Netlify)
└── README.md          # This file
```

That's it. No build step, no node_modules, no framework. Just static files.

---

## Quick Deploy Options

### Option 1: Netlify (easiest, free)

1. Sign up at [netlify.com](https://netlify.com) (free tier is generous)
2. Drag and drop this entire folder into the Netlify dashboard
3. Site goes live in ~30 seconds at a random subdomain like `wonderful-curie-abc123.netlify.app`
4. To use your own domain (e.g. `mejorars.com`):
   - Buy domain at Namecheap / GoDaddy / Google Domains
   - In Netlify: **Domain settings** → **Add custom domain** → follow DNS instructions
   - SSL certificate is automatic and free

### Option 2: Vercel (also easy, free)

1. Sign up at [vercel.com](https://vercel.com)
2. Install Vercel CLI: `npm i -g vercel`
3. From this folder, run: `vercel`
4. Follow prompts — site deploys in seconds
5. Custom domain: **Project Settings** → **Domains** → add your domain

### Option 3: GitHub Pages (free, requires Git)

1. Create a new GitHub repo named `mejorars-website` (or whatever)
2. Push these files to it
3. In repo settings → **Pages** → set source to `main` branch → `/` root
4. Site goes live at `https://<username>.github.io/mejorars-website/`
5. Custom domain: add a `CNAME` file with your domain name

### Option 4: Cloudflare Pages (free, fast CDN)

1. Sign up at [pages.cloudflare.com](https://pages.cloudflare.com)
2. **Create a project** → **Direct Upload** → drag this folder
3. Live in seconds with their global CDN
4. Custom domain through Cloudflare DNS (very fast if you transfer your domain too)

### Option 5: Your own server (advanced)

The site is pure static HTML/CSS/JS. Any web server works:
```bash
# Quick local test
python3 -m http.server 8000
# Or with Node
npx serve .
```

For production: nginx, Apache, Caddy — just serve the folder as static files.

---

## Before You Launch — Customization Checklist

### 1. Replace placeholder URLs

The site references `mejorars.com` in several meta tags. Open `index.html` and find/replace:

- `https://mejorars.com/` → your real domain (in canonical, Open Graph, Twitter card, schema.org)
- `https://mejorars.com/og-image.jpg` → URL to your social preview image (see step 2)
- `https://mejorars.com/logo.png` → URL to your real logo

Also in `sitemap.xml` and `robots.txt`: replace `mejorars.com`.

### 2. Create a social preview image (`og-image.jpg`)

This is the image that appears when someone shares your site on LinkedIn / Twitter / Slack / iMessage.

- Size: **1200×630px exactly**
- Format: JPG or PNG (JPG smaller, PNG sharper)
- Should include: your logo, the headline "Beyond ideas into impact", your brand colors
- Tools: Figma, Canva (search "OG image template"), or any image editor
- Place the file in this folder as `og-image.jpg`

### 3. Add a favicon.ico (optional, for older browsers)

The site already has `favicon.svg` which works in all modern browsers. For older browsers and Windows taskbar:

- Go to [realfavicongenerator.net](https://realfavicongenerator.net)
- Upload `favicon.svg`
- Download the generated package
- Drop `favicon.ico` and `apple-touch-icon.png` into this folder

### 4. Replace social media links

In `index.html`, find the contact section's social links:
```html
<a href="#">Instagram</a>
<a href="#">LinkedIn</a>
<a href="#">Behance</a>
<a href="#">X / Twitter</a>
<a href="#">Dribbble</a>
```
Replace `#` with your actual profile URLs (e.g. `https://instagram.com/mejorars`).

### 5. Update the email address

Search for `hello@mejorars.com` across `index.html` and replace with your real email. There are several places:
- The contact section
- The "Hire us" nav button
- The "Start your journey" CTA

Make sure the email is real and you check it.

### 6. Update the schema.org structured data

In `index.html` find the `<script type="application/ld+json">` block. Update:
- `name`, `url`, `logo`
- Address (currently "Bangalore, IN")
- `email`
- `sameAs` URLs (your social profiles)

This helps Google understand your business and show rich results.

### 7. Update copyright year and meta info

In the footer of `index.html`: `© 2026 · Creative studio · Bangalore` — change as needed.

---

## Testing Before Launch

Open `index.html` in a browser locally:

```bash
# From this folder
python3 -m http.server 8000
# Then open http://localhost:8000
```

**Test these things:**

- [ ] All links work (nav, services, CTAs, socials)
- [ ] Hover effects work on service rows and approach cards
- [ ] Email link opens your email client
- [ ] Loader fades cleanly within 3 seconds
- [ ] Site looks good at 375px (mobile), 768px (tablet), 1440px (desktop)
- [ ] No console errors (open DevTools → Console)
- [ ] Test with throttled network (DevTools → Network → "Slow 3G")
- [ ] Test with JavaScript disabled (site should still show all content)
- [ ] Tab through with keyboard — focus rings should be visible

**Then verify your social preview:**

After deploying with your real domain:
- [Twitter card validator](https://cards-dev.twitter.com/validator)
- [Facebook sharing debugger](https://developers.facebook.com/tools/debug/)
- [LinkedIn post inspector](https://www.linkedin.com/post-inspector/)

Paste your URL into each. If the image doesn't show, you may need to wait a few minutes (or "scrape again" in each tool).

---

## Performance Notes

This site is intentionally lean:

- **No frameworks** — vanilla HTML/CSS/JS only
- **Single HTML file** with inlined CSS (no separate stylesheet to fetch)
- **Three CDN scripts**: GSAP, ScrollTrigger, Lenis — cached aggressively by their CDNs
- **Four Google Fonts** loaded together in one request
- **Total page weight: ~70KB** before fonts/JS libs cache
- **Lighthouse target**: 90+ Performance, 95+ Accessibility, 100 Best Practices, 100 SEO

If you want to make it even faster:
- Self-host the fonts (download from Google Fonts, serve from your domain, drop the `https://fonts.googleapis.com` preconnect)
- Self-host GSAP and Lenis (download minified versions, serve from your domain)
- Add a service worker for offline caching

---

## Browser Support

Tested and working in:
- Chrome / Edge / Brave (modern Chromium): full experience
- Firefox: full experience
- Safari 15+: full experience
- Mobile Safari / Chrome Android: full experience

Older browsers (IE11, Safari < 14): site still renders all content but loses smooth-scroll, magnetic cursor, and some animations. Acceptable degradation.

---

## Maintenance

- **Updating content**: just edit `index.html` directly. No build step.
- **Adding pages**: create new `.html` files in this folder. Add them to `sitemap.xml`.
- **Changing colors**: at the top of the `<style>` block in `index.html`, find the `:root { ... }` CSS variables and edit there.
- **Changing fonts**: update the Google Fonts URL in `<head>` and the `--display`, `--serif`, `--mono`, `--hand` variables.

---

## Questions

For technical issues, check the browser DevTools console first. Most problems are visible there.

If something looks broken after deployment, hard-refresh (Ctrl+Shift+R / Cmd+Shift+R) to bust the cache.

Built 2026 · Mejorars Creative Studio
