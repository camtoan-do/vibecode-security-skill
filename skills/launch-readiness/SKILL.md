---
name: launch-readiness
description: Audit a vibe-coded website for the nineteen launch basics and put the missing pieces in place, safely — custom 404 page, CTA above the fold, meta title and description per page, Open Graph image, favicon, robots.txt, sitemap.xml, alt text, mobile breakpoint, sticky mobile CTA, loading states, form error states, thank-you page, privacy policy page, terms page, cookie banner, analytics, real contact address. Use before launching or relaunching a site, after an AI agent has built or rebuilt pages, or when the user asks "is my site ready to launch", "pre-launch checklist", "what did the AI forget", "why does my link preview look broken" or "why is my form not working on mobile".
---

# Launch readiness for vibe-coded sites

An AI agent will happily build a site that demos well and breaks at the edges: the wrong URL, the slow network, the bad form input, the phone screen, the crawler. These nineteen items are those edges. Each one is also a place where a rushed build leaks information or fails badly, so every check here has a **security and resilience** half, not only a polish half.

Your job: check what the **built site really serves**, fix what is missing with the least new code, and never trade safety for a tick in a box.

## Rules

1. **Check the output, not the source.** Build the site and inspect the served HTML, headers and network requests. A component existing proves nothing.
2. **Never invent facts** about the owner: address, email, company name, analytics IDs. Ask, or leave a visible `TODO(owner)` and list it in the report.
3. **Do not weaken security to pass a check.** If the site has a Content-Security-Policy, new scripts, styles and images must fit it. Never add `unsafe-inline`, a wildcard source, or a third-party script to make something work without telling the user what it costs.
4. **Fail closed and fail quiet.** Error pages and error messages tell the visitor what to do next and tell an attacker nothing: no stack traces, file paths, framework versions, SQL, or "this email is already registered".
5. **Use the platform.** Prefer the framework's own 404, sitemap, image and head features over hand-rolled ones. No new dependency for a few lines.
6. **Not applicable is a valid answer.** A site with no form needs no thank-you page. A site with no cookies needs no banner. Say so; don't build for show.

## Workflow

### 1. Map the site

Find the framework, the host, and how it deploys. List every route (including dynamic ones), every form and where it posts, every third-party script, and any existing security headers (`_headers`, `netlify.toml`, `vercel.json`, middleware, meta tags). Build the site. This list is what you audit against.

### 2. Audit the nineteen items

Go through [references/checklist.md](references/checklist.md). For each item record one status:

- **in effect** — present in the built output and safe
- **gap** — missing, broken, or present but unsafe
- **not applicable** — say why, and when it would start to apply

### 3. Fix, in this order

1. **Unsafe first:** anything leaking information (verbose errors, secret paths in robots.txt or the sitemap, personal data in URLs) or loading before consent (analytics, pixels).
2. **Broken edges:** 404, form error states, loading states, mobile layout.
3. **Missing files and tags:** titles, descriptions, Open Graph image, favicon, robots.txt, sitemap.xml, alt text.
4. **Pages and conversion:** CTA, sticky mobile CTA, thank-you page, contact address.
5. **Legal three** (privacy policy, terms, cookie banner): confirm the page exists and is linked from the footer here. For what the pages must say and whether the banner really blocks scripts, run the [`legal-readiness`](../legal-readiness/SKILL.md) skill.

### 4. Verify

Rebuild, then prove each fix against the built site:

- request a URL that does not exist → status **404** (not 200), custom page, no internals
- every page has a unique `<title>` and meta description
- `/robots.txt`, `/sitemap.xml`, the favicon and the Open Graph image all return 200
- 375px wide: no horizontal scroll, CTA visible without scrolling, sticky CTA does not cover content or the cookie banner
- submit each form empty, with bad input, with the network throttled, and twice quickly
- fresh browser profile: no analytics request before consent (where consent is required)
- browser console: no Content-Security-Policy violations

### 5. Report

Give the user:

- a 19-row table: item · status · what you did · what's left
- every `TODO(owner)`
- anything you chose **not** to add and why (for example: no cookie banner because nothing non-essential is stored)
- any new third party the site now talks to, and what it receives

## Red flags — stop and tell the user

- The "404" page returns status 200, or shows a stack trace or framework debug page
- robots.txt `Disallow` lines that name admin, staging, backup or API paths — it is a public file and a map for attackers, not access control
- The sitemap lists drafts, admin, thank-you or per-user pages
- Form data, email addresses or tokens in the URL (`?email=`, GET forms) — they end up in logs, analytics and the Referer header
- Error messages that confirm whether an account exists
- Analytics or pixels firing before consent, or capturing form fields and URLs with personal data
- A fix that needed `unsafe-inline`, a disabled header, or a removed validation to work
- A contact address that is a placeholder, a personal home address, or a mailbox nobody reads
