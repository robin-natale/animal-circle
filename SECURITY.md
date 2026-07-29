# Security Policy

## Reporting a Vulnerability

**Please do NOT report security vulnerabilities through public GitHub issues.**

Instead, report them privately via:

1. **GitHub Security Advisory** (preferred, if the repo is hosted on GitHub): Security tab → "Report a vulnerability"
2. **Email**: hello@animalcircle.org

We will acknowledge receipt within 48 hours and provide a status update within 5 business days.

## Security Measures

This is a static site, so the attack surface is small.

### Content Security Policy
- Enforced via `public/_headers` at the Cloudflare edge
- `frame-ancestors 'none'` prevents clickjacking
- `form-action 'self'` restricts form submissions
- Allows only configured analytics + the OpenStreetMap embed

### Secrets
- All secrets via Cloudflare Pages secrets or `.dev.vars` (gitignored)
- No secrets in code — enforced locally by `pnpm run validate:secrets` (part of `pnpm run lint`)

### Infrastructure
- **Cloudflare Pages** — DDoS protection, WAF, automatic TLS

## Scope

This policy applies to the Animal Circle codebase and its deployed site.

This policy does NOT cover:
- User-deployed infrastructure (Cloudflare account settings, DNS, etc.)
- Third-party services — report to their security teams
