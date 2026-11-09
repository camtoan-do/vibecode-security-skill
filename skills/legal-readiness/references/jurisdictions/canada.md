# Canada

Use this when the app's owner is in Canada or the app has Canadian users. It covers what Canadian law expects, **what each document must include**, and how to lower the owner's risk of being sued.

Laws change. Before relying on a number or deadline here, check the current text. This is not legal advice.

## The honest answer to "make sure I don't get sued"

Nobody can promise that. Anyone can file a claim. What you can do is make claims unlikely, weak and cheap:

1. **Do less risky things.** Collect less data, promise less, don't hold money or secrets you don't need.
2. **Say only true things.** Most claims start from a gap between what was promised and what happened.
3. **Set the terms.** Disclaimers and a liability limit, properly agreed to.
4. **Keep the user's rights intact.** Canadian consumer law voids terms that go too far, and a void term protects nobody.
5. **Limit what's at stake.** A sole proprietor's personal assets are exposed. Incorporating and carrying insurance (errors & omissions, cyber) change that. Tell the owner to speak to a lawyer and an insurance broker; you can't do this part in code.

## Which laws apply

| Area | Law | Applies when |
| --- | --- | --- |
| Privacy | **PIPEDA** (federal) | Commercial activity anywhere in Canada, and across provincial or national borders |
| Privacy | **Alberta PIPA**, **BC PIPA** | Organisations operating within those provinces |
| Privacy | **Quebec Law 25** | Any Quebec users. The strictest of the four. |
| Email, SMS, installs | **CASL** | Any commercial electronic message sent to or from Canada |
| Selling online | **Provincial consumer protection acts** (e.g. Alberta, Ontario, BC, Quebec) | Selling to consumers. The buyer's province usually governs. |
| Advertising, pricing | **Competition Act** | Any marketing claim or displayed price |
| Language | **Quebec Charter of the French Language** | Offering goods or services to Quebec consumers |
| Accessibility | **AODA** (Ontario), **Accessible Canada Act** (federally regulated) | Larger organisations; good practice for all |
| Copyright | **Copyright Act** | Any content, code, fonts, images |
| Computer misuse | **Criminal Code s. 342.1, 430(1.1)** | Any security testing, scanning or scraping |
| Tax | **Excise Tax Act (GST/HST)** | Revenue over the small-supplier threshold (CA$30,000 across four consecutive quarters) |

If the owner can't say which provinces their users are in, build to PIPEDA and flag Quebec as a gap.

## What to include

### Privacy policy

Must include:

- [ ] **Who is accountable**: name or title of the person responsible for privacy, and how to reach them. PIPEDA requires one to be designated. For a solo owner it's the owner.
- [ ] **What is collected and why**, stated at or before collection. Purposes a reasonable person would consider appropriate.
- [ ] **Consent**: how it's obtained, and how to withdraw it. Express consent for sensitive information (health, financial, biometrics, precise location, children).
- [ ] **Who it's shared with**, including service providers.
- [ ] **Storage outside Canada**: say that data may be processed in other countries (name them where you can) and may be accessible to authorities there. Alberta PIPA specifically requires notice when service providers outside Canada are used.
- [ ] **Retention**: how long, and that it's destroyed or anonymised afterwards.
- [ ] **Safeguards**, described honestly.
- [ ] **Access and correction**: how to request, and that you respond within 30 days.
- [ ] **How to complain**: to the owner first, then the Office of the Privacy Commissioner of Canada or the provincial commissioner (Alberta OIPC, BC OIPC, Quebec CAI).
- [ ] **Date** of last update.

Add for Quebec users:

- [ ] Name and contact of the privacy officer, published on the site
- [ ] Notice of any profiling, tracking or location technology, and how to turn it on (it must be **off by default**)
- [ ] Notice of decisions made solely by automated processing, with a way to ask for human review
- [ ] Rights to portability and to stop dissemination (de-indexing)
- [ ] Parental consent for anyone under 14
- [ ] A privacy impact assessment before sending personal information outside Quebec (an internal record, not on the page)
- [ ] The policy available in French

### Terms & conditions

Must include:

- [ ] **Who the agreement is with**: the owner's legal name (or company) and contact.
- [ ] **What the service is and isn't**: general information, not professional advice; no professional-client relationship without a separate written agreement.
- [ ] **Acceptable use**, including: only use security tooling or guidance on systems you own or have written permission to test.
- [ ] **User responsibility**: for AI-generated output, the user reviews and tests it before relying on it.
- [ ] **No warranty**: "as is" and "as available".
- [ ] **Limitation of liability**: exclude indirect and consequential loss; cap total liability (a fixed amount for free services; fees paid in the last 12 months for paid ones).
- [ ] **Consumer rights carve-out**: "Nothing here limits rights that can't be waived under consumer protection law." Without it, an over-broad clause can be struck entirely.
- [ ] **Indemnity** for the user's own misuse or law-breaking. Keep it narrow and mutual in tone.
- [ ] **Accounts and termination**, if there are accounts.
- [ ] **Intellectual property**: what's owned, what users may reuse, licence over user content.
- [ ] **Payment terms** or a link to them.
- [ ] **Governing law and courts**: the owner's province, "and the federal laws of Canada applicable there", with an exception where consumer law gives the user their home courts.
- [ ] **Changes**: how they're announced. For paid consumer contracts, give advance notice and a right to cancel; unilateral silent changes are not enforceable in several provinces.
- [ ] **Severability** and **no waiver**.

Make it enforceable:

- [ ] **Clickwrap for anything that matters.** An unticked "I agree" box or a button labelled as agreement, next to a link to the terms. Canadian courts enforce clickwrap. Terms merely linked in a footer (browsewrap) are weak; they only hold where the user clearly had notice.
- [ ] **Record acceptance**: user, timestamp, version of the terms.
- [ ] **Plain language**, with the liability limit and renewals not buried. Unfair terms nobody could reasonably have noticed get struck as unconscionable.
- [ ] **Don't rely on mandatory arbitration or class-action waivers** against consumers. Ontario and Quebec void them; Alberta restricts them; the Supreme Court has struck one for unconscionability.
- [ ] **Don't exclude liability for your own deliberate or grossly negligent acts**, or for death or injury. Quebec bars excluding liability for your own acts against consumers.

### Cookie notice

- [ ] Canada has no separate cookie law; cookies fall under privacy law. Disclose them in the privacy policy with a cookie table.
- [ ] Analytics and advertising trackers need meaningful consent. The federal commissioner treats behavioural advertising as needing at least an easy opt-out, and opt-in where the data is sensitive.
- [ ] **Quebec**: tracking and profiling technology must be off until the user turns it on. Use an opt-in banner if there are Quebec users.
- [ ] No trackers, no banner.

### Marketing email (CASL)

Every commercial message must have:

- [ ] **Consent** obtained before sending. Express consent: the user actively opts in after being told who is asking and why, with a statement that they can unsubscribe. No pre-ticked boxes. Not bundled with the terms.
- [ ] **Identification**: who is sending, and on whose behalf.
- [ ] **Contact details**: a mailing address plus a phone number, email or web address, valid for 60 days after sending.
- [ ] **Unsubscribe**: free, simple, working for 60 days, honoured within 10 business days.

Know the limits of implied consent: an existing customer for 2 years after their last purchase; someone who made an enquiry for 6 months. After that, express consent or stop. Keep proof of every consent; the sender carries the burden. Receipts, password resets and security notices are exempt from consent but still need identification.

### Selling online

Before the buyer pays, show:

- [ ] Seller's name, business address, phone and email
- [ ] A fair description of what's being sold
- [ ] **The all-in price.** Mandatory fees must be in the headline price. Adding them at checkout is "drip pricing" and is prohibited under the Competition Act. Only government-imposed taxes may be added later.
- [ ] Currency, taxes, delivery or access date
- [ ] Cancellation, return and refund terms
- [ ] For subscriptions: the amount, how often, how it renews, how to cancel

Then:

- [ ] Let the buyer review and correct the order before confirming
- [ ] Send a copy of the contract or receipt (provincial rules generally require it within 15 days for internet sales over a small threshold, about $50)
- [ ] Honour statutory cancellation rights; where disclosure was missing, buyers can cancel
- [ ] Cancelling a subscription must be as easy as joining; send a reminder before long-term renewals
- [ ] Register for and charge GST/HST once over the small-supplier threshold, or sell through a merchant of record that handles tax

### Marketing claims

- [ ] Every claim is true and can be backed up: "secure", "compliant", "guaranteed", "bank-grade", performance numbers
- [ ] No fake reviews, testimonials or urgency ("only 2 left")
- [ ] "Free" means free; conditions are stated next to the claim
- [ ] Environmental claims need proof

### Breach response

- [ ] Assess for **real risk of significant harm** (sensitivity of the data, likelihood of misuse)
- [ ] If met: report to the Privacy Commissioner of Canada (and the provincial commissioner where provincial law applies) and notify affected people **as soon as feasible**
- [ ] Notify any organisation that can reduce the harm (payment processor, police)
- [ ] **Keep a record of every breach for 24 months**, including ones not reported
- [ ] Quebec: also keep an incident register and notify the CAI

### Intellectual property

- [ ] Copyright notice and reuse terms
- [ ] A contact for infringement complaints. Canada uses **notice-and-notice**, not US-style takedown: a host forwards the notice to the user and keeps records. There is no automatic duty to remove on notice, though leaving clearly infringing content up after you know is risky.
- [ ] Licences recorded for all third-party code, fonts, icons and images

### Language and accessibility

- [ ] Quebec consumers: the site, terms, checkout and support available in French, at least as prominently as English
- [ ] Follow WCAG 2.0 AA where practical. It's mandatory for larger Ontario organisations and federally regulated ones, and lowers human-rights complaint risk for everyone.

## Extra rules for security tools and security advice

Vibe-coded security apps carry a specific risk: the tool, or advice from it, gets used on a system without permission, or someone relies on it and gets breached.

- [ ] **Authorisation first.** Any scan, test or assessment requires the system owner's written permission. Unauthorised access or interference is a criminal offence (Criminal Code s. 342.1 and 430(1.1)), for the user and potentially for whoever ran the tool.
- [ ] **Scanners prove ownership** before scanning a target: DNS record, file upload, or login to the target account.
- [ ] **State what the tool doesn't do.** "This checks X. It is not a penetration test or a guarantee of security."
- [ ] **Results are point-in-time.** Say so on every report.
- [ ] **For paid services, a written engagement agreement**: scope, authorisation, access and its removal, confidentiality, data handling, liability cap, and who to call if something breaks.
- [ ] **Rate-limit and log** anything that sends traffic to third parties.

## Things outside the code — tell the owner

These matter more than any page, and only the owner can do them:

- **Business structure.** A sole proprietor is personally liable for everything. A corporation separates business risk from personal assets.
- **Insurance.** Errors & omissions (professional liability) and cyber liability.
- **A lawyer's review** of the terms and privacy policy before real revenue or sensitive data.
- **Trade name registration** if operating under a brand name.
- **GST/HST registration** at the threshold.

## Canada-specific mistakes

- Using a US template: "DMCA", "CCPA", "COPPA", governing law of Delaware
- Citing GDPR legal bases but never mentioning consent, which is what Canadian law runs on
- No named privacy contact
- Not disclosing that data is stored in the US
- Treating a purchase as permanent permission to send marketing email
- Adding a service fee at checkout
- A blanket "we are not liable for anything" clause with no consumer carve-out
- Forgetting Quebec exists
