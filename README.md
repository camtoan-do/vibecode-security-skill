# vibecode-security-skill

Agent skills for securing vibe-coded apps.

## Skills

| Skill | What it does |
| --- | --- |
| [`legal-readiness`](skills/legal-readiness/SKILL.md) | Audits an app for the 14 legal and privacy basics (privacy policy, terms, cookie consent, legal basis, marketing consent, deletion, retention, DPAs, third-party disclosure, data security, breach procedure, IP, open-source licences, payments) and puts the missing pieces in place. |
| [`launch-readiness`](skills/launch-readiness/SKILL.md) | Audits a site for the 19 launch basics (custom 404, CTA above the fold, meta title and description per page, Open Graph image, favicon, robots.txt, sitemap.xml, alt text, mobile breakpoint, sticky mobile CTA, loading states, form error states, thank-you page, privacy policy, terms, cookie banner, analytics, real contact address) and fixes the gaps without leaking information or weakening security headers. |

## Jurisdictions

| Jurisdiction | Status |
| --- | --- |
| Canada | Ready — [canada.md](skills/legal-readiness/references/jurisdictions/canada.md) |
| United States | Underway |
| European Union / UK | Underway |

## Install (Claude Code)

Copy a skill folder into your project or user skills directory:

```bash
cp -r skills/legal-readiness skills/launch-readiness ~/.claude/skills/
```

Then ask: "Run a legal readiness audit on this app" or "Is this site ready to launch?"

## Not legal advice

These skills produce honest drafts and working mechanisms. They don't replace a lawyer.
