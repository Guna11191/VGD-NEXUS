# Deployment checklist

## Render / Railway / managed Node server

1. Upload this repository or connect your Git provider.
2. Build command: `npm install && npm run build`.
3. Start command: `npm start`.
4. Choose Node 22.x runtime; set `PORT` as required by the platform.
5. Add the SMTP and contact environment variables from `.env.example` to the host's secrets manager. Never upload `.env`.
6. Enable HTTPS and a custom domain with the host.
7. Verify route refreshes (`/about`, `/services`, `/contact`), form delivery, 404 behavior, and mobile menu.
8. Add production spam protection, centralized logs, monitoring and durable rate limiting.

## Netlify / Vercel static hosting

The frontend may be deployed statically with `npm run build`, but `/api/contact` is an **Express server endpoint** and is not automatically deployed by static-only hosting. You must either deploy the Express API separately and configure a secure `/api` proxy or adapt it to the host's supported serverless function format. Do not publish the form as operational until end-to-end delivery is verified.

For static SPA hosting, configure a history fallback to `/index.html` for all page URLs.

## Security and launch checklist

- Replace the placeholder brand mark with official logo
- Confirm claims, contact details and portfolio permissions
- Finalize privacy notice and legal policies
- Configure sender SPF/DKIM/DMARC according to email provider
- Add abuse protection (CAPTCHA or equivalent as appropriate)
- Audit dependencies, browser accessibility, SEO and mobile performance
- Implement structured logging/monitoring and production rate limits
- Test enquiry emails to the real inbox
- Configure HTTPS, origin policies, backups (if data is stored) and error monitoring
- Add sitemap, canonical tags and OpenGraph image with the real domain
