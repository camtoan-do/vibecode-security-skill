# vibecode-security-skill

Agent skills for securing vibe-coded apps.

## Skills

| Skill | What it does |
| --- | --- |
| [`legal-readiness`](skills/legal-readiness/SKILL.md) | Audits an app for the 14 legal and privacy basics (privacy policy, terms, cookie consent, legal basis, marketing consent, deletion, retention, DPAs, third-party disclosure, data security, breach procedure, IP, open-source licences, payments) and puts the missing pieces in place. |

## Install (Claude Code)

Copy a skill folder into your project or user skills directory:

```bash
cp -r skills/legal-readiness ~/.claude/skills/
```

Then ask: "Run a legal readiness audit on this app."

## Not legal advice

These skills produce honest drafts and working mechanisms. They don't replace a lawyer.
