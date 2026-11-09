# The fourteen areas

For each: when it applies, what "done" means in the **code**, what the **page** must say, and the mistake vibe-coded apps usually make.

## 1. Privacy policy
- **Applies:** always, once the app is public. Even a static site has host logs.
- **Code:** nothing collected that the policy doesn't mention.
- **Page:** who runs it and how to reach them · what is collected, per situation · why · who else receives it · where it's stored · how long · user rights and how to use them · how to complain · date.
- **Common mistake:** a generated policy that lists things the app doesn't do and misses what it does (the LLM API, the error tracker).

## 2. Terms & conditions
- **Applies:** always. Essential once there are accounts, user content or payments.
- **Page:** what the service is · acceptable use · accounts and termination · no-warranty and liability limit · IP · payment terms (or link) · governing law · how changes are announced.
- **Code:** if terms must be accepted, record who accepted which version and when. Acceptance is a separate, unticked box, not bundled with marketing.
- **Common mistake:** copying another company's terms, including their name and jurisdiction.

## 3. Cookie consent
- **Applies:** when anything non-essential is stored on or read from the device (analytics, ads, embeds, pixels), for EU/UK users. Strictly necessary items (session, CSRF, saved preferences) need disclosure, not consent.
- **Code:** non-essential scripts **do not load** until consent · reject is as easy as accept · per-category choices · no pre-ticked boxes · choice can be changed later · consent stored with timestamp and notice version · honour Global Privacy Control where required.
- **Page:** table of every cookie/storage item: name, purpose, lifetime, who receives it.
- **Common mistake:** a banner that is decoration — the analytics tag already fired. Test with the network tab on a fresh profile. Also: no cookies means **no banner needed**; don't add one for show.

## 4. Legal basis
- **Applies:** GDPR users. Useful discipline everywhere.
- **Page:** table: each processing purpose → basis (consent, contract, legal obligation, legitimate interests, vital interests, public task). Under Canadian law: consent (express or implied) and reasonable purpose.
- **Code:** where the basis is consent, there's a way to withdraw it that actually stops the processing.
- **Common mistake:** "consent" for everything. Delivering what the user paid for is contract; security logging is legitimate interests; tax records are legal obligation.

## 5. Marketing consent
- **Applies:** any promotional email, SMS or push.
- **Code:** explicit opt-in, unticked, separate from terms · double opt-in recommended · every message has sender identity, a postal/contact address and a working unsubscribe · unsubscribe honoured promptly (CASL: 10 business days; do it instantly) · consent log: who, when, how, wording shown · suppression list survives account deletion.
- **Common mistake:** treating every signed-up user as a marketing subscriber. Transactional email (receipts, password resets) is fine without marketing consent; a "we launched a feature" blast is not.

## 6. Data deletion
- **Applies:** as soon as personal data is stored.
- **Code:** self-service delete in account settings · deletes rows, files, search indexes, caches, and third-party copies (email tool, analytics, payment customer) · backups expire on a stated schedule · confirmation sent · also support export (access/portability) and correction.
- **Page:** how to ask, how identity is checked, timeline (30 days is the usual bar), what can't be deleted and why (tax records).
- **Common mistake:** soft-delete flag only (`deleted_at`) with data kept forever, or deleting the user row and orphaning everything else.

## 7. Data retention
- **Applies:** as soon as personal data is stored.
- **Code:** a scheduled job that deletes or anonymises on schedule — inactive accounts, old logs, expired sessions, unverified sign-ups, old uploads. Backups and logs included.
- **Page:** table: data type → how long → why.
- **Common mistake:** no schedule at all; logs with emails and IPs kept indefinitely.

## 8. Data processing agreements
- **Applies:** every vendor that handles personal data for the app (hosting, database, auth, email, analytics, error tracking, AI APIs, support tools).
- **Do:** list vendors from the data map · confirm each has a DPA and that it's accepted (often automatic in their terms; sometimes a click or signature) · note data location and transfer mechanism (SCCs, adequacy) · check their sub-processor list · check AI vendors' settings for training on your data.
- **If the app is B2B:** customers will ask the owner for a DPA. Have one ready, with a sub-processor list.
- **Common mistake:** free-tier tools with no DPA; pasting user data into an AI API with training enabled.

## 9. Third-party disclosure
- **Applies:** always.
- **Page:** table of every recipient: who, role, what data, where. State plainly whether data is sold or shared for advertising. State when disclosure happens without consent (legal requirement).
- **Code:** the list matches reality — grep for script tags, SDK imports and outbound hosts. A strict Content-Security-Policy makes the list enforceable.
- **Common mistake:** forgetting fonts/CDNs, embedded videos, maps, captcha, and the session-replay tool.

## 10. Data security
- **Applies:** always.
- **Code (minimum):** HTTPS + HSTS · secrets out of the repo and the client bundle · passwords hashed (argon2/bcrypt) or delegated auth · authorisation checked server-side on every request (row-level security actually enabled) · input validation · security headers and CSP · dependencies scanned · encryption at rest · least-privilege keys · MFA on admin and vendor accounts · tested backups · audit logs without sensitive data in them.
- **Page:** what's in place, in honest general terms, plus limits and how to report a vulnerability (`/.well-known/security.txt`).
- **Common mistake:** "bank-grade security" on the page; service-role key in the frontend and RLS off in the database.

## 11. Data breach procedure
- **Applies:** always — written before it's needed.
- **Document:** contain → assess (what, whose, how many, risk of harm) → notify (affected people; regulator — GDPR 72 hours, Canada "as soon as feasible" where there's real risk of significant harm; business customers per contract) → record every breach (Canada: keep 24 months) → fix and review.
- **Code:** enough logging and alerting to notice a breach · a way to force logouts and rotate keys · contact list stored outside the affected systems.
- **Common mistake:** no procedure, and no logs to tell what was accessed.

## 12. Intellectual property
- **Applies:** always.
- **Page:** who owns the app and content · what users may reuse · if users submit content: they keep ownership and grant a licence to host/display it · takedown contact for infringement claims · trademarks of others used only to identify.
- **Check:** the owner actually has rights to the name, logo, images, fonts and copy. AI-generated assets may have unclear ownership; stock images need a licence that covers commercial use.
- **Common mistake:** images lifted from search results; a name that's someone else's trademark.

## 13. Open-source licences
- **Applies:** always — every app has dependencies.
- **Do:** list licences (`npx license-checker --summary`, `pip-licenses`, `cargo license`) · permissive (MIT, BSD, ISC, Apache-2.0): keep notices · copyleft (GPL, LGPL, AGPL, SSPL): understand the obligation before shipping; AGPL triggers on network use · "no licence" means no permission · check fonts/icons too.
- **The app's own code:** if the repo is public, either add a `LICENSE` or say clearly it's all rights reserved. Public is not open source.
- **Page:** credits/notices list, and the status of the app's own code.
- **Common mistake:** AI pasted a snippet from a GPL project; public repo with no licence and an assumption that it's "open".

## 14. Payments & subscriptions
- **Applies:** when money moves.
- **Code:** hosted checkout from a payment provider — card data never touches the server · fulfilment driven by **signature-verified webhooks**, never the success-page redirect · webhooks idempotent · prices server-side, never trusted from the client · cancel online as easily as subscribing · renewal reminders and trial-end notices · failed-payment grace period · receipts · tax handled (or a merchant of record used).
- **Page:** price, currency, taxes, billing period, renewal, how to cancel, refund terms, price-change notice.
- **Common mistake:** unlocking paid features from a client-side flag or the redirect URL; cancel only by email; a "free trial" that quietly converts.
