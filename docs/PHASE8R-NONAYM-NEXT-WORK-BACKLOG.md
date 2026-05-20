# Phase 8R — Nonaym Next-Work Backlog

Date: 2026-05-20

## Purpose

Create a clean backlog for the next Nonaym.ai functional build work after the production repo and helper workflow were corrected.

This phase is documentation only.

No website changes.
No commit unless intentionally copying this backlog into docs.
No deploy.
No Cloudflare action.
No service changes.
No Hermes gateway mode.
No mobile_dispatcher service mode.
Do not use port 18889.

---

## Current Production Source of Truth

Production working repo:

~/.openclaw/workspace/websites/nonaym-website-production

GitHub repo:

mslepikas/nonaym-website

Branch:

main

Live site:

https://nonaym.ai

Do not use old production-confusing repo:

~/.openclaw/workspace/websites/nonaym-ai

Old repo:

mslepikas/nonaym-site

---

## Current Production State

Latest confirmed production commits:

a3d338b document nonaym production handoff
b1f85bd document nonaym production source of truth
0d4eca4 nonaym.ai v1.2.1-build002 restore logo assets
8b5dc34 nonaym.ai v1.2.1-build001 public info pages

Live site currently includes:

- Contact page
- RFQ page
- Download/readiness page
- Nonaym DIY — Coming Soon
- Nonaym Lite — In Planning
- Nonaym AI — Later This Year
- No real /api/leads backend yet
- No checkout/payment flow yet
- DIY download is not public yet

---

## Backlog Priority 1 — Verify Contact Inbox

Task:

Verify that contact@nonaym.ai is a working inbox before relying on it publicly.

Why:

Several placeholder forms and messages currently reference contact@nonaym.ai. Before using it for real customers, confirm it can receive email and is monitored.

Acceptance criteria:

- Test email sent to contact@nonaym.ai
- Email is received
- Reply path works
- Inbox owner/responsible person is clear
- Public pages only rely on this address after verification

Notes:

Do not publish additional email addresses unless intentionally approved.

---

## Backlog Priority 2 — Decide Safe Lead Handling

Task:

Decide how Nonaym should collect customer interest.

Current state:

Forms are placeholder/static.
No real /api/leads backend exists.
This is intentional for now.

Options:

1. Keep forms placeholder-only
2. Use mailto fallback after contact@nonaym.ai is verified
3. Add a Cloudflare Pages Function for /api/leads
4. Use a third-party form/CRM service
5. Use a lightweight database or queue later

Recommended next step:

Start with a simple, low-risk intake path before building a full CRM.

Danno review required before collecting or storing customer leads.

Acceptance criteria:

- Data fields are defined
- Storage destination is defined
- Spam/abuse handling is considered
- Privacy wording is written
- No secrets are hardcoded
- Danno reviews before deployment

---

## Backlog Priority 3 — Plan /api/leads Cloudflare Pages Function

Task:

Plan a future Cloudflare Pages Function for:

/api/leads

Do not implement until reviewed.

Possible function behavior:

- Accept basic lead form POSTs
- Validate required fields
- Reject unexpected fields
- Rate-limit or add basic spam protection
- Store or forward the message safely
- Return a simple success/failure response

Allowed basic fields:

- name
- email
- product_interest
- message
- use_case
- old_computer_available
- number_of_locations

Do not collect:

- passwords
- router credentials
- payment information
- credit card information
- full home address
- router serial numbers
- public IPs
- LAN IPs
- Cloudflare tokens
- Tailscale details
- Okta details
- private network details

Acceptance criteria:

- Function plan reviewed by Danno
- Environment variables documented but not exposed
- Public endpoint behavior is safe
- No customer data is exposed in repo
- No secrets in source code

---

## Backlog Priority 4 — DIY Compatibility / Readiness Form

Task:

Design the customer readiness flow before allowing DIY downloads.

Purpose:

Help customers confirm whether an old computer is likely to work before downloading or installing Nonaym DIY.

Suggested readiness questions:

- Is this a 64-bit x86 computer?
- How much RAM does it have?
- How much storage does it have?
- Does it have wired Ethernet?
- Can it boot from USB?
- Can the disk be erased?
- Will this computer stay powered on?
- Are important files backed up?
- Is the customer comfortable changing basic router settings if needed?

Minimum target:

- 64-bit x86 computer
- 4 GB RAM
- 32 GB storage
- USB boot support
- Wired Ethernet recommended
- Disk can be erased

Better target:

- 8 GB RAM
- 64 GB SSD or larger
- Wired Ethernet
- Reliable power
- Can stay powered on

Important warning:

The DIY installer may erase the target computer. Customers should not use a computer that contains files they need unless those files are backed up first.

Acceptance criteria:

- Form asks only useful compatibility questions
- No unnecessary private data collected
- Clear warning about disk erase
- Clear status that download is not live until tested
- Danno review before collecting responses

---

## Backlog Priority 5 — Define Nonaym DIY Minimum Requirements

Task:

Turn the readiness notes into a public-facing minimum requirements page.

Draft requirements:

Minimum:

- 64-bit x86 computer
- 4 GB RAM
- 32 GB storage
- USB boot support
- Wired Ethernet recommended
- Ability to erase the target disk

Recommended:

- 8 GB RAM
- 64 GB SSD or larger
- Wired Ethernet
- Reliable power
- Can stay powered on continuously

Need to decide:

- Supported CPU age
- Whether Wi-Fi-only systems are supported
- Whether laptops are acceptable
- Whether mini PCs are preferred
- Whether UEFI-only boot is required
- Whether Secure Boot must be disabled
- Whether a second USB stick is needed
- Whether installer will support common Lenovo ThinkCentre Tiny devices

Acceptance criteria:

- Minimum requirements documented
- Supported/not-supported hardware examples documented
- Language is customer-friendly
- Avoid overly technical DNS language

---

## Backlog Priority 6 — Nonaym Lite Product Readiness

Task:

Plan the Lite appliance path.

Current direction:

Nonaym Lite is a small DNS/privacy appliance for customers who do not want to repurpose an old computer.

Need to decide:

- Hardware platform
- Vendor/OEM/white-label option
- Base OS
- Technitium DNS packaging
- Admin dashboard scope
- Update path
- Support expectations
- Price target
- Shipping/fulfillment path

Acceptance criteria:

- Hardware candidate selected
- Support burden estimated
- Clear difference from DIY
- Public wording says “In Planning” until ready

---

## Backlog Priority 7 — Buy It Now / Checkout Planning

Task:

Plan future checkout flow.

Do not implement payment code yet.

Possible future checkout:

- Stripe Payment Links
- Shopify Lite / simple ecommerce
- Cloudflare-compatible checkout link
- Manual invoice/RFQ for early customers

Danno review required before publishing payment links or checkout code.

Safety rules:

- No Stripe secret keys in repo
- No payment secrets in frontend
- No fake purchase buttons
- No order promise until product is ready
- Clearly separate waitlist/RFQ from actual purchase

Acceptance criteria:

- Checkout provider chosen
- Fulfillment process defined
- Refund/support policy drafted
- Danno reviews public copy and payment handling

---

## Backlog Priority 8 — Nonaym AI Later

Task:

Keep Nonaym AI as future higher-priced local AI computer.

Current public status:

Nonaym AI — Later This Year

Do not overbuild this yet.

Future topics:

- Local AI logging/intelligence
- Customer dashboard
- Model update controls
- Blocking service selection
- Emergency kill button
- Local-host AI computer option
- Higher price tier

Acceptance criteria:

- Does not distract from DIY and Lite
- No promises beyond realistic roadmap
- No collection of sensitive network data without review

---

## Backlog Priority 9 — Website Content Cleanup

Task:

Review public language for customer friendliness.

Potential cleanup areas:

- Avoid overly technical DNS language
- Avoid scary claims that sound exaggerated
- Keep message focused:
  - cleaner home internet
  - fewer trackers
  - simpler privacy
  - no subscription where possible
  - simple setup

Acceptance criteria:

- Non-technical customer can understand the site
- Product statuses are honest
- No fake download or buy button
- No unsupported pricing promises

---

## Backlog Priority 10 — Review Workflow Discipline

Every future Nonaym production change must start here:

cd ~/.openclaw/workspace/websites/nonaym-website-production

Then verify:

pwd
git branch --show-current
git remote -v
git status -sb

Then run:

nonaym-predeploy-capture
hermes-review ~/.hermes/audits/nonaym-predeploy-output-LATEST.md

Rules:

- Q = technical helper only
- Danno = security/privacy/risk gate
- Human approval required before commit/push/deploy
- Verify Q claims with shell output
- Do not use old nonaym-ai repo for production

---

## Recommended Next Actual Build Phase

Recommended next build phase:

Phase 9A — Contact Inbox Verification and Lead Intake Decision

Do before implementing /api/leads.

Phase 9A should answer:

1. Does contact@nonaym.ai work?
2. Will short-term lead intake use mailto, static placeholder, or Cloudflare Pages Function?
3. What exact fields are allowed?
4. Where will the data go?
5. What privacy wording is needed?
6. What does Danno approve?

