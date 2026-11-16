# VGD NEXUS — Responsive animated company website

A complete **source-code project** for a multi-page software-company marketing website built with React, Vite, Motion for React, Lucide icons, and a small Express email API.

## Included

- Home, About, Services, Solutions, Portfolio (illustrative, filterable capabilities), Technologies, Careers, Contact, Privacy, and 404 pages
- Dark navy + yellow identity, original SVG-based iconography and illustrated dashboard
- Responsive navigation, mobile slide-out menu, scroll progress, route transitions, scroll reveals, hover/tap states
- Reduced-motion support, keyboard focus styles, form field labels, skip navigation, basic metadata
- Contact form with client **and server validation**, honeypot, simple in-memory throttling, SMTP email delivery when configured
- Self-contained UI graphics (no purchased stock assets)

## Install and run

Requires **Node.js 20.19+** (or Node 22.12+). In the project root:

```bash
npm install
cp .env.example .env
npm run dev:full
```

Open **http://localhost:5173**. The Vite frontend proxies `/api` to Express at port 3001.

For a static frontend-only preview, run `npm run dev`. The Contact form will indicate that the API is not configured.

## Production build

```bash
npm run build
npm start
```

Open **http://localhost:3001**. Express serves the built Vite assets and handles API calls. Use HTTPS behind a trusted reverse proxy / managed hosting. In production, add standard hosting health checks, logging, durable rate limiting and spam protection as appropriate.

**Single-page routing:** Requests to `/about`, `/services` etc. fall back to `dist/index.html`. On static/CDN hosting, configure an SPA history fallback to `/index.html`.

## Contact form — required owner configuration

Copy `.env.example` to `.env` and set:

| Key | Purpose |
| --- | --- |
| `SMTP_HOST` | SMTP host of your email provider |
| `SMTP_PORT` | Usually `587` for STARTTLS, `465` for TLS |
| `SMTP_SECURE` | Set `true` for implicit TLS (e.g. 465) |
| `SMTP_USER`, `SMTP_PASS` | Provider-issued SMTP account credentials |
| `CONTACT_TO` | Verified company inbox to receive enquiries |
| `CONTACT_FROM` | Sender approved by your email provider |
| `PORT` | Server port (defaults to 3001) |

**Never put SMTP secrets in Vite `VITE_*` environment variables:** they would be embedded in the browser bundle.

The form intentionally refuses to claim an enquiry was sent when SMTP is not configured or the provider fails. Test actual email delivery before publishing. Do not expose the site to public traffic without completing spam, abuse prevention, privacy and security review. The in-memory rate limiter is appropriate for a demonstration or small single-instance deployment, but a production distributed site should use a persistent rate-limit store and a managed anti-abuse solution.

## Update the company details before launch

1. Replace the **original geometric brand mark** in `src/components/UI.jsx` and `public/favicon.svg` with the finalized official logo. The previously discussed logo asset was not accessible in the current project workspace.
2. Confirm the user-provided statistics: **200+ projects, 9+ years, 50+ clients, 15+ experts**. They have not been independently verified.
3. Replace illustrative showcase concepts with permissioned, verified client case studies and project screenshots, if available.
4. Populate the real company email and phone, address, social profiles and job postings when confirmed. These have **not** been invented.
5. Review Privacy page with your privacy/legal team and add the real legal entity, data controller, retention periods, user rights, third-party providers, and contact information.
6. Add analytics only after deciding on consent and privacy requirements.
7. Replace/locally host fonts if you want a completely offline interface; the current CSS uses Google Fonts with system fallbacks.
8. Configure domain, canonical URLs, sitemap and social share image after the production domain is decided.
9. For stronger SEO, consider migrating to SSR/static rendering, or prerender public routes; this starter uses a client-rendered Vite SPA.

## Project structure

```
public/                    favicon and robots.txt
server/index.js            Express routes + SMTP email handler
src/App.jsx                Router shell and animated route transitions
src/components/UI.jsx      Shared header, footer, cards, animation helpers
src/data/site.js           Navigation, services, industries, technology and showcases
src/pages/                 Individual pages
src/styles.css             Responsive design system and animations
```

## Technical notes

- Motion imports use the documented `motion/react` entry point.
- Contact submissions are validated on the backend; there is no browser-only fake success.
- KPI dashboard figures in the hero art (e.g. `+24.8%`) are **decorative demo UI**, not asserted company achievements.
- No copyrighted third-party image assets are bundled.
- This package is ready to run and customize, but is **not represented as a live deployed/production-certified website**. No real contact-inbox delivery can be tested until SMTP credentials are provided.
