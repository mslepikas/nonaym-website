# Phase 9F — Nonaym Lead Intake Guardrails Plan

Date: 2026-05-21

## Purpose

Resolve Danno's required guardrails before any future Nonaym `/api/leads` implementation.

This phase does not build `/api/leads`.

It defines the security, privacy, retention, storage, consent, and anti-abuse requirements that must be satisfied before implementation.

## Production source of truth

Working repo:

~/.openclaw/workspace/websites/nonaym-website-production

GitHub repo:

mslepikas/nonaym-website

Branch:

main

Live site:

https://nonaym.ai

## Current state

Phase 9E was completed and committed.

Latest known commit:

40a451f document nonaym lead intake redesign result

Phase 9E result:

- Danno approved the lead intake redesign with modifications.
- Do not proceed to implementation until guardrails are resolved.
- Early intake should use email-only first.
- R2 may be used later for v2+.
- Phone is excluded from v1.
- IP is excluded from lead records.
- Turnstile is recommended before public form submission.
- Contact form should come first, RFQ next.

## Phase 9F is not implementation

Do not create:

- functions/
- api/
- /api/leads
- wrangler.toml
- Cloudflare Pages Function
- R2 binding
- Turnstile widget
- live form submission

This phase is only a guardrail decision record.

## Required guardrails from Danno

### 1. R2 bucket privacy

Requirement:

The R2 bucket used for leads must remain private.

Decision:

`nonaym-leads` must have public access disabled.

No public read access is allowed.

No public object URLs are allowed for lead records.

### 2. Least-privilege write access

Requirement:

A future Pages Function must have the minimum required access.

Decision:

Future `/api/leads` should only write approved lead records to the intended R2 path.

Preferred future paths:

- production/leads.jsonl
- test/leads.jsonl

The function should not expose read/list/delete operations to the public website.

### 3. Server-side schema allowlist

Requirement:

Approved fields must be validated on the server.

Decision:

The future Pages Function must use a hardcoded allowlist.

Approved v1 fields:

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

Rejected v1 fields:

- ip
- phone
- password
- token
- secret
- API key
- router password
- Wi-Fi password
- credit card
- payment info
- full address
- router serial
- LAN IP
- public IP
- Tailscale details
- Okta details
- Cloudflare credentials

### 4. Unexpected field rejection

Requirement:

Unexpected fields must be rejected server-side.

Decision:

The future backend should reject submissions containing keys outside the approved allowlist.

Client-side validation is not sufficient.

### 5. Turnstile / anti-spam

Requirement:

Public forms need anti-abuse protection.

Decision:

Before public `/api/leads` goes live, Nonaym should use Cloudflare Turnstile or equivalent Cloudflare-native abuse protection.

Recommended:

- Turnstile required for public form POST
- Rate limiting if available through Cloudflare plan/config
- Short message length limits
- Basic honeypot field optional
- No IP storage in lead record

### 6. Retention enforcement

Requirement:

Retention must be enforceable, not just stated.

Decision:

Recommended retention:

- Test leads: delete within 30 days when no longer needed
- Real leads: retain up to 12 months after last interaction
- Deletion requests: respond within 30 days where reasonable

Enforcement options:

Preferred:

- R2 lifecycle rule, if supported for the target object pattern

Temporary acceptable bridge:

- documented monthly manual review/delete process

Future option:

- scheduled cleanup job after Danno review

### 7. Consent wording

Requirement:

Consent text must live in version-controlled docs.

Decision:

Store only:

consent_acknowledged: true

Do not store the full consent sentence inside each lead record.

Consent copy must be documented in the repo.

Candidate consent wording:

"I agree that Nonaym may use this information to respond to my inquiry and provide product availability updates. Do not send passwords, payment information, router credentials, IP addresses, or private network details."

### 8. Access/log review

Requirement:

Access/log review process must be documented.

Decision:

Monthly review should confirm:

- R2 bucket remains private
- no unexpected public access
- no unexpected lead fields
- no raw lead files committed to Git
- test and production records remain separated
- retention cleanup is performed if needed

### 9. Test/production separation

Requirement:

Do not mix test and production records.

Decision:

Future path separation:

- test/leads.jsonl
- production/leads.jsonl

Existing root-level `leads.jsonl` should not be used for future production intake.

Existing root-level test records may be retained temporarily, moved, or deleted in a later reviewed phase.

### 10. Contact inbox verification

Requirement:

Early intake should use email-only first.

Decision:

Before public customer-contact language is expanded, contact@nonaym.ai or an alternate inbox should be verified.

This can be handled in a separate inbox-verification phase if not already completed.

## Recommended implementation gate

Do not build `/api/leads` until all of the following are true:

- privacy policy v3 is approved
- contact inbox is verified
- R2 bucket privacy is confirmed
- schema allowlist is finalized
- Turnstile/rate limiting approach is chosen
- consent wording is committed
- retention approach is documented
- Danno approves implementation plan

## Acceptance criteria for Phase 9F

Phase 9F is complete when:

- this guardrails plan is reviewed by Danno
- Danno blockers are recorded
- a final guardrails decision document is created
- optional docs are committed to the production repo
- no implementation has occurred