# www.franvallejo.es

Personal and professional site of Francisco Vallejo Luna, served by Apache from
`/var/www/franvallejo`.

## Stack

- Static HTML + CSS + a small vanilla JS file. No frameworks, no jQuery, no build step.
- `index.html` is the single-page site. Styles in `assets/css/site.css`, behaviour in
  `assets/js/site.js`.
- Light/dark theme follows the system preference and can be toggled manually
  (`localStorage` key: `theme`).
- Legacy HTML5UP assets (`assets/css/main.css`, `assets/sass`, `assets/js/jquery*`) are
  kept for history but are no longer referenced by the site.

## Decisions (2026-11-04 redesign)

- Full rewrite of `index.html`: semantic, responsive (mobile/tablet), accessible,
  no tracking and no third-party assets.
- Removed the public phone number and the `cv/` directory (the CV PDF was from 2022).
- Removed personal data not needed on a public professional site: birth year and exact
  towns. Only `Madrid, Spain` is shown.
- Updated experience to 20 years and current role at OpenText.
- Certifications refreshed from the public Credly profile
  (`https://www.credly.com/users/francisco-vallejo/badges`), including the 2024–2026
  badges that were missing. CKAD is listed under earlier credentials because the badge
  expired in 2022.
- Fixed old errors: `mailto:neotherack@gmail`, `Lón` -> `León`, `KCAD` -> `CKAD`,
  `+15 years` -> 20 years, mixed `http` links.
- `moba.py`, `ace.apk`, `HSK3.pdf`, `video/`, `lucky_video/`, `charts/`, `mcp_exam/` and
  `shouji/` are intentionally left untouched.

## Security (Apache vhost)

Hardening lives in `/etc/apache2/sites-available/001-franvallejo.es-le-ssl.conf`:

- `Options -Indexes` and no `.htaccess` overrides.
- Hidden files blocked, except ACME files under `.well-known/acme-challenge`.
- `venv.tar.gz` blocked from public download. `moba.py` is explicitly not touched.
- HSTS, `X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy` and
  `Permissions-Policy` on the whole vhost.
- A strict CSP is applied only to the homepage (`/` and `/index.html`) so that the
  standalone study apps in subdirectories (`charts/`, `mcp_exam/`, `shouji/`) keep
  working with their own inline styles/scripts.

## Backup

Before the redesign, a full backup (site without `.git` plus both vhost files) was
written to:

```
/mnt/backup-nas/franvallejo/franvallejo_web_2026-11-04_pre-redesign.tar.gz
```

Delete it once the redesign has been stable for a few weeks.

## Git

- Remote: `git@github.com:neotherack/franvallejo_website.git`
- Work is done on `develop`. `main` is only updated after explicit approval.
