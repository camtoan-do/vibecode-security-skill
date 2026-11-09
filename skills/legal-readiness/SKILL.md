---
name: legal-readiness
description: Audit a vibe-coded web app for the legal and privacy basics and put the missing pieces in place — privacy policy, terms & conditions, cookie consent, legal basis, marketing consent, data deletion, data retention, data processing agreements, third-party disclosure, data security, data breach procedure, intellectual property, open-source licences, payments & subscriptions. Use before launching an app, when adding sign-up, analytics, a newsletter, payments or a new third-party service, or when the user asks "is my app legal", "do I need a privacy policy / cookie banner", "GDPR", "CASL", "PIPEDA" or "what do I need before I launch".
---

# Legal readiness for vibe-coded apps

Vibe-coded apps ship fast and usually skip this layer. Your job: find out what the app **really does with data**, then make the legal pages and the code tell the same true story.

You are not a lawyer and neither is this skill. Say so once, plainly. Produce honest drafts and working mechanisms, and tell the user to get a lawyer's review before handling sensitive data (health, children, finance) or real revenue.

## Rules

1. **Describe reality, never aspirations.** A policy that says "we encrypt everything" when the code doesn't is worse than no policy. Every claim must trace to code or config you read.
2. **Never invent facts** about the owner: company name, address, jurisdiction, retention periods, refund terms. Ask, or leave a visible `TODO(owner)` and list it in the report.
3. **Collect less first.** The cheapest fix for most gaps is deleting the field, tracker or vendor.
4. **Mechanisms beat documents.** A delete-account button matters more than a paragraph promising deletion.
5. **Plain English.** Short sentences. No "herein".

## Workflow

### 1. Build the data map (do not skip)

Read the code, not the README. If the repo is large, use a code-graph or search tool rather than reading every file. Find:

- **Inputs:** forms, sign-up/login, file uploads, API routes that accept bodies
- **Storage:** database schemas/models, object storage, local/session storage, cookies set (`Set-Cookie`, `document.cookie`, auth libraries)
- **Third parties:** every SDK, script tag, embed, font CDN, and outbound API call (analytics, auth, email, payments, AI/LLM APIs, error tracking, hosting, logs)
- **Email sent:** transactional vs marketing
- **Money:** checkout, subscriptions, webhooks
- **Dependencies and assets:** licences of packages, fonts, icons, images

Write it as a table: `data | where collected | why | where stored | sent to | kept how long`. Unknown cells are findings. This table drives everything else.

### 2. Decide which laws are in play

Ask where the owner is based and where users are. Defaults: EU/UK users → GDPR and ePrivacy; Canada → PIPEDA or provincial law, CASL for email; California → CCPA/CPRA; any US → CAN-SPAM, FTC auto-renewal rules. If unsure, build to GDPR for privacy and CASL for email — the strictest common bar.

### 3. Audit the fourteen areas

Go through [references/checklist.md](references/checklist.md). For each area record one status:

- **in effect** — applies now and is done
- **gap** — applies now and is missing or untrue
- **standby** — doesn't apply yet; write down the rule for when it does

Do not mark something "in effect" because a page exists. Check the mechanism.

### 4. Fix, in this order

1. **Stop the bleeding:** trackers firing before consent, secrets in the repo, card data touching the server, marketing email without opt-in or unsubscribe.
2. **Build mechanisms:** consent banner that actually blocks scripts, unsubscribe, delete-my-account, retention job, verified payment webhooks.
3. **Write the pages** from the data map, using [references/page-templates.md](references/page-templates.md). One page per area, or sections of one page for a small app. Link them from the footer.
4. **Add tripwires** so the pages can't silently go stale — see [references/tripwires.md](references/tripwires.md).

Each page ends with an **"If this changes"** section: the rules that apply before the next feature (accounts, analytics, payments) is added. That is what lets a static site be ready ahead of time.

### 5. Report

Give the user:

- the data map
- a 14-row table: area · status · what you did · what's left
- every `TODO(owner)` and every commitment the pages now make on their behalf (response times, retention periods, refund terms, governing law), so they can confirm each one
- what needs a lawyer

## Red flags — stop and tell the user

- Children's data, health data, biometrics, precise location, or government IDs
- Sending user content to an AI API without disclosing it
- Storing card numbers, or passwords in plain text
- A bought or scraped email list
- GPL/AGPL code inside a closed-source product
- Dark patterns: pre-ticked consent, hidden cancel, "accept" bigger than "reject"
