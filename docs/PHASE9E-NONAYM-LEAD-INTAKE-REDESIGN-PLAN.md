# Phase 9E — Nonaym Lead Intake Redesign Plan

Date: 2026-05-21

## Purpose

Design the future Nonaym.ai lead intake flow before rebuilding or enabling `/api/leads`.

This phase uses lessons from the existing R2 test lead storage, but does not implement the backend yet.

## Current production source of truth

Working repo:

~/.openclaw/workspace/websites/nonaym-website-production

GitHub repo:

mslepikas/nonaym-website

Branch:

main

Live site:

https://nonaym.ai

## Current known state

- Production repo has no active `/api/leads` backend.
- No `functions/` or `api/` files exist in production.
- Existing R2 bucket `nonaym-leads` exists.
- Existing `leads.jsonl` contains test-only data.
- Danno confirmed no incident response is needed.
- Existing test schema includes:
  - created
  - email
  - id
  - ip
  - message
  - name
  - phone
  - tier

## Main redesign question

What should the real lead intake flow collect, store, and disclose when Nonaym starts collecting real customer interest?

## Safety rules

No code changes.
No backend implementation.
No Cloudflare changes.
No R2 writes.
No commit/push/deploy unless only saving documentation.
No checkout/payment.
No live DIY download.
No Hermes gateway mode.
No mobile_dispatcher service mode.
Do not use port 18889.

## Design principles

The future lead intake flow should:

- collect the minimum useful information
- avoid sensitive network details
- avoid automatic IP storage unless specifically justified
- avoid phone number unless necessary
- explain what is collected and why
- provide a retention/deletion plan
- avoid storing secrets or private network details
- be easy to disable if something breaks

## Proposed allowed fields

Recommended production lead fields:

- id
- created
- source_page
- name
- email
- product_interest
- message
- use_case
- old_computer_available
- number_of_locations
- consent_acknowledged

## Fields to remove or avoid

Avoid by default:

- ip
- phone

Avoid always:

- passwords
- router credentials
- Wi-Fi passwords
- payment information
- credit card numbers
- full home address
- public IP addresses
- LAN/internal IP addresses
- router serial numbers
- private network diagrams
- private keys
- API keys
- Cloudflare tokens
- Tailscale details
- Okta details
- admin credentials

## Phone field decision

Recommended:

Do not collect phone number in the first production lead form.

Reason:

Email is enough for early interest, waitlist, RFQ, and DIY readiness. Phone increases sensitivity and support expectations.

Possible future exception:

Add phone later only for quote requests or appliance fulfillment after Danno review.

## IP field decision

Recommended:

Do not intentionally store visitor IP addresses in `leads.jsonl`.

Reason:

IP addresses are privacy-sensitive and not needed for basic customer interest.

If abuse prevention is needed later:

Use Cloudflare-native protections, Turnstile, or rate limiting without storing IP in lead records unless specifically approved.

## Storage decision

Candidate storage:

Cloudflare R2 bucket:

nonaym-leads

Object format:

leads.jsonl

Recommended production object path:

production/leads.jsonl

Recommended test object path:

test/leads.jsonl

Reason:

Separate test and production records to avoid confusion.

## Retention proposal

Recommended:

- Test leads: delete when no longer needed or every 30 days
- Real lead inquiries: retain up to 12 months after last interaction
- Deletion requests: respond within 30 days where reasonable
- Security/abuse logs: keep separate from lead records if needed

## Consent proposal

Before real form submission, add an unchecked consent checkbox:

"I agree that Nonaym may use this information to respond to my inquiry and provide product availability updates. Do not send passwords, payment information, router credentials, IP addresses, or private network details."

Submission should not proceed unless checked.

## Privacy/security pages required before launch

Before real `/api/leads` goes live:

- `/security/` page already exists
- `/privacy/` page still needs approved v3
- Contact inbox status should be verified or an alternate monitored contact path chosen

## Future `/api/leads` behavior

A future Cloudflare Pages Function should:

- accept only POST
- reject unexpected methods
- parse JSON or form data safely
- validate required fields
- reject unexpected fields
- limit message length
- include basic spam protection
- store only approved fields
- not store IP by default
- not store phone by default
- append sanitized record to R2
- return simple success/error response
- avoid leaking internal errors
- require Danno review before deploy

## Recommended approved schema v1

{
  "id": "generated-id",
  "created": "ISO-8601 timestamp",
  "source_page": "contact|rfq|download|homepage",
  "name": "string, optional",
  "email": "string, required",
  "product_interest": "diy|lite|ai|not_sure|multiple",
  "use_case": "home|small_office|family|other|not_provided",
  "old_computer_available": "yes|no|not_sure|not_applicable",
  "number_of_locations": "1|2-3|more_than_3|not_provided",
  "message": "string, optional, max length",
  "consent_acknowledged": true
}

## Open questions

1. Should R2 remain the lead store, or should early intake use email only?
2. Should production leads go to `production/leads.jsonl` instead of root `leads.jsonl`?
3. Should test records be deleted or moved to `test/leads.jsonl`?
4. Should phone be excluded entirely for v1?
5. Should IP be excluded entirely from lead records?
6. Should Cloudflare Turnstile be added before public forms?
7. What should the exact retention period be?
8. What should the first real form be: contact, RFQ, DIY readiness, or waitlist?

## Recommended decision for Phase 9E

Recommended initial production intake design:

- R2 may be used later, but only after Privacy Policy v3 is approved.
- Do not collect phone in v1.
- Do not collect IP in lead records.
- Use production/test path separation.
- Require consent checkbox.
- Keep current forms placeholder-only until Phase 9F or later.
- Build `/api/leads` only in a separate implementation phase after Danno approves this design.

## Acceptance criteria

Phase 9E is complete when:

- allowed fields are documented
- prohibited fields are documented
- phone/IP decisions are documented
- storage path decision is documented
- retention proposal is documented
- Danno reviews the redesign plan
- no implementation occurs yet
