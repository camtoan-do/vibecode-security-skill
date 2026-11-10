# The nineteen items

For each: what "done" means, the **security and resilience** half, and the mistake vibe-coded sites usually make.

## 1. Custom 404 page
- **Done:** an unknown URL returns HTTP **404** with a branded page, a link home and the main navigation.
- **Safe:** no stack trace, file path, framework name or version. The requested URL is not echoed into the page unescaped (reflected XSS). Same rule for the 500 page.
- **Common mistake:** a single-page app that returns 200 for everything ("soft 404"), or the host's default page leaking the stack.

## 2. CTA above the fold
- **Done:** one primary action visible without scrolling at 375px and at desktop width. It is a real `<a>` or `<button>`, reachable by keyboard, with text that says what happens.
- **Safe:** external targets opened with `target="_blank"` carry `rel="noopener"`. The destination is a fixed URL, never built from a query parameter (open redirect).
- **Common mistake:** a clickable `<div>`; three competing CTAs; a hero so tall the button is below the fold on a phone.

## 3. Meta title per page
- **Done:** every route has its own `<title>`, roughly 50–60 characters, specific first, site name last.
- **Safe:** titles built from content or URL data are escaped by the framework, not concatenated as raw HTML.
- **Common mistake:** every page titled the same, or still "Vite + React" / "Create Next App".

## 4. Meta description per page
- **Done:** every route has its own `<meta name="description">`, roughly 120–160 characters, true to the page.
- **Safe:** same escaping rule as titles. Private or per-user pages get `noindex` instead of a description.
- **Common mistake:** one description in the layout copied to every page; none on dynamic routes.

## 5. Open Graph image
- **Done:** `og:title`, `og:description`, `og:url`, `og:image` (absolute HTTPS URL, about 1200×630, under ~1 MB) and `twitter:card` on every page. The image URL returns 200.
- **Safe:** the image is a static file or generated at build time. A dynamic image endpoint that renders text from the URL lets anyone make your domain serve their message and can be hammered for CPU — validate input, cache, rate-limit, or don't build it. Strip metadata (EXIF, location) from photos.
- **Common mistake:** a relative image path; a screenshot containing a real email, dashboard or API key.

## 6. Favicon
- **Done:** `favicon.svg` or `.ico`, plus a 180px `apple-touch-icon.png`, linked in `<head>` and returning 200.
- **Safe:** served from your own origin so it fits the Content-Security-Policy `img-src` and no third party sees every page load.
- **Common mistake:** the framework's default logo; an icon hot-linked from someone else's server.

## 7. robots.txt
- **Done:** served at `/robots.txt` as plain text, allows what should be indexed, and has a `Sitemap:` line.
- **Safe:** it is public and advisory. It is **not** access control. Never list secret, admin, staging or backup paths in `Disallow` — that advertises them. Protect those with authentication; keep them out of search with `noindex` or an `X-Robots-Tag` header.
- **Common mistake:** `Disallow: /` left over from staging, hiding the whole site; or a neat list of every sensitive path.

## 8. sitemap.xml
- **Done:** generated at build time from the real routes, absolute HTTPS URLs on the canonical domain, referenced from robots.txt.
- **Safe:** contains only pages meant to be public and indexed. No drafts, admin, thank-you, preview or per-user URLs.
- **Common mistake:** a hand-written sitemap that goes stale; localhost or preview-domain URLs.

## 9. Alt text
- **Done:** every `<img>` has an `alt` attribute. Meaningful images describe what they show; decorative ones use `alt=""`. Icon-only buttons and links have an accessible name.
- **Safe:** alt text from user content is escaped. No sensitive detail in alt text that the image itself was cropped to hide.
- **Common mistake:** `alt="image"`, the file name, or keyword stuffing.

## 10. Mobile breakpoint
- **Done:** `<meta name="viewport" content="width=device-width, initial-scale=1">`. At 375px: no horizontal scroll, text at least 16px, tap targets about 44px, navigation usable.
- **Safe:** zoom is not disabled (`user-scalable=no`, `maximum-scale=1`). Anything hidden on mobile with CSS is still in the page — hide for layout, never for secrecy.
- **Common mistake:** fixed pixel widths; a table or code block that pushes the page sideways.

## 11. Sticky mobile CTA
- **Done:** on small screens the primary action stays reachable while scrolling, respects `env(safe-area-inset-bottom)`, and the page has bottom padding so it never hides the last content.
- **Safe:** it does not cover the cookie banner's reject button, form error messages or the submit button (an overlay that hides a consent choice is a dark pattern). Keyboard focus is never hidden under it.
- **Common mistake:** the bar sits on top of the footer links and the banner; it also shows on the page it links to.
- **Not applicable:** short single-screen pages.

## 12. Loading states
- **Done:** anything that waits on the network shows it: the button disables and says what is happening, results areas use `aria-busy` or a status region.
- **Resilient:** every request has a timeout and a visible failure message — no infinite spinner. The submit button is disabled while sending so a double tap cannot create two orders or two emails; anything that costs money or sends mail is also idempotent on the server.
- **Common mistake:** a spinner with no error path; the happy path was the only one tested.

## 13. Form error states
- **Done:** each error is shown next to its field, in words, linked with `aria-describedby` and `aria-invalid`. The user's input is kept. Focus moves to the first error.
- **Safe:** the browser check is for convenience; the **server validates everything again**. Error text is generic toward attackers — no stack traces, SQL, or "that email is already registered" on sign-up, login or reset. Public forms have rate limiting and a spam check (honeypot or challenge).
- **Common mistake:** validation only in the browser; a raw 500 response printed to the page; the form clearing itself on error.

## 14. Thank-you page
- **Done:** after a successful submit the visitor lands on a page (or state) confirming what happened and what comes next.
- **Safe:** reached by POST then redirect, so refresh does not resubmit. No personal data or tokens in its URL. Marked `noindex` and left out of the sitemap. If it fires a conversion event, it does not send form values with it.
- **Common mistake:** `/thank-you?name=…&email=…`; a page anyone can open directly that fires a fake conversion.
- **Not applicable:** no forms and no checkout.

## 15. Privacy policy page
- **Done:** exists, linked from the footer on every page, dated, and describes what this site really collects.
- **Safe / content:** run the `legal-readiness` skill — a policy that does not match the code is a liability.
- **Common mistake:** a generated policy describing features the site does not have.

## 16. Terms page
- **Done:** exists, linked from the footer, names the real owner and governing law.
- **Safe / content:** run the `legal-readiness` skill.
- **Common mistake:** another company's terms with their name still in it.

## 17. Cookie banner
- **Done:** if anything non-essential is stored or read on the device, a banner appears before it happens, reject is as easy as accept, and the choice can be changed later.
- **Safe:** non-essential scripts **do not load** until consent — check the network tab on a fresh profile. The banner works within the Content-Security-Policy and is usable by keyboard.
- **Common mistake:** a decorative banner while the tag already fired.
- **Not applicable:** nothing non-essential is stored. Then **no banner** — don't add one for show.

## 18. Analytics installed
- **Done:** one analytics tool, confirmed receiving a page view from the live site. Prefer a cookieless, privacy-friendly one (it can remove the need for a banner).
- **Safe:** loads only after consent where consent is required. Its script and endpoint are added to the Content-Security-Policy narrowly (exact host, no wildcard, no `unsafe-inline`). It does not capture form fields, or URLs carrying emails or tokens. Session-replay and "capture everything" features are off unless the owner chose them and the privacy policy says so. The tool is named in the privacy policy.
- **Common mistake:** two or three overlapping trackers pasted in by different prompts; an ID copied from a tutorial; the CSP loosened to `*` to make it work.

## 19. Real contact address
- **Done:** a working, monitored way to reach the owner — at least an email address on the owner's domain — on a contact page or in the footer. Send a test message and confirm it arrives. Ask the owner for it; never invent one.
- **Safe:** the sending domain has SPF, DKIM and DMARC so the address cannot be trivially spoofed. A business or mailing address rather than a home address (ask the owner). Add `/.well-known/security.txt` so vulnerability reports have somewhere to go. If there is a contact form, item 13 applies.
- **Common mistake:** `hello@example.com`, "123 Main St", or a `mailto:` to a mailbox that was never created.
