# Page templates

Fill these from the data map. Delete rows that don't apply; never leave a claim you didn't verify. `{{…}}` are owner facts — ask, or leave `TODO(owner)`.

Every page uses the same shape:

```markdown
# {{Title}}
_Last updated {{date}} · Status: in effect | standby_

## Today
What is true right now, in plain English.

## If this changes
The rules that apply before the next feature ships.
```

## Privacy policy

```markdown
## The short version
{{App}} is run by {{owner}}, based in {{place}}. Contact: {{email}}.

## What is collected
| Situation | What | Who holds it |
| --- | --- | --- |
| You visit | IP address, browser, pages requested | {{host}} |
| You sign up | {{fields}} | {{database provider}} |
| You pay | Name, email, payment details | {{payment provider}} — we never see your card number |

## What it's used for
{{purposes}}. We don't sell personal information.

## Who else sees it        → link to third-party page
## How long it's kept      → link to retention page
## Your rights
Access, correction, deletion, withdrawal of consent: {{how}}. We answer within 30 days.
## Complaints
{{regulator for the owner's jurisdiction}}
```

## Cookie table

```markdown
| Name | Purpose | Category | Lifetime | Shared with |
| --- | --- | --- | --- | --- |
| `session` | Keeps you signed in | Strictly necessary | 30 days | Nobody |
```

If the table has only strictly-necessary rows: say "no banner, because there's nothing to consent to."

## Legal basis table

```markdown
| What we do | Why | GDPR basis |
| --- | --- | --- |
| Run your account | To provide the service | Contract |
| Security logs | To protect the service | Legitimate interests |
| Invoices | Tax law | Legal obligation |
| Newsletter | You opted in | Consent |
```

## Retention table

```markdown
| Information | Kept for | Why |
| --- | --- | --- |
| Account data | Until you delete the account, then {{n}} days in backups | To provide the service |
| Server logs | {{n}} days | Security and debugging |
| Invoices | {{years required locally}} | Tax law |
```

## Third parties / processors table

```markdown
| Provider | Role | What it sees | Where | DPA |
| --- | --- | --- | --- | --- |
| {{host}} | Hosting | Request data | {{region}} | In standard terms |
```

## Breach procedure

```markdown
1. Contain — lock accounts, rotate keys, revoke sessions.
2. Assess — what data, whose, how many, how sensitive, risk of harm.
3. Notify — affected people; regulator ({{deadline for jurisdiction}}); business customers.
4. Record — every breach, including those not notified.
5. Fix and review — root cause, blameless write-up.
```

## Payments

```markdown
- Checkout is run by {{provider}}; card details never reach us.
- Price: {{amount}} {{currency}} per {{period}}, {{tax}}. Renews automatically until cancelled.
- Cancel any time at {{where}}; access continues until the end of the paid period.
- Refunds: {{owner's actual policy}}.
```
