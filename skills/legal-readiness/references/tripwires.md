# Tripwires

Legal pages go stale the moment someone prompts "add analytics". A tripwire is a small automated check that fails the build when the app starts doing something the pages don't cover, and tells the developer which page to update.

## Pattern

In the project's existing build check or CI (don't add a framework for this):

```js
// Things the legal pages currently say the app does NOT do.
// When one appears: update the legal pages first, then add its name to REVIEWED.
const REVIEWED = [];
const TRIPWIRES = [
  { name: "form",              pattern: /<form[\s>]/i,            pages: "privacy policy, legal basis, retention" },
  { name: "cookie",            pattern: /document\.cookie|Set-Cookie/i, pages: "cookies" },
  { name: "third-party-embed", pattern: /<(script|iframe|img)\b[^>]*\ssrc="https?:\/\/(?!example\.com)/i, pages: "third-party disclosure, cookies, DPAs" },
];
```

Scan the built output, fail with a message naming the pages. Once the pages are updated, the developer acknowledges by adding the name to `REVIEWED`. Replace `example.com` with the app's own domain.

## Other useful tripwires

- New dependency whose licence is not on an allow-list (`license-checker --onlyAllow "MIT;ISC;BSD-2-Clause;BSD-3-Clause;Apache-2.0"`)
- New outbound host in server code that isn't in the third-party table
- Database migration adding a column named like `email`, `phone`, `address`, `dob` without a retention entry
- Secret scanning on every push
- A Content-Security-Policy with `default-src 'self'`: the browser itself then blocks unlisted third parties

## Also record it for the AI

Add a line to the project's agent instructions (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`):

> Before adding anything that collects data, sets a cookie, sends email, takes payment or calls a new third-party service, update the legal pages first.
