# Phase 9F — Nonaym Lead Intake Guardrails Decision

Date: 2026-05-21

## Result

DANNO_PLAN_OK

## Purpose

Record the required guardrails before any future Nonaym `/api/leads` implementation.

## Implementation status

No implementation approved in this phase.

No `/api/leads` created.
No Cloudflare Pages Function created.
No R2 writes performed.
No Cloudflare settings changed.
No deploy performed.

## Guardrail decisions

### R2 privacy

Lead storage bucket must remain private.

Public access must be disabled.

No public lead object URLs are allowed.

### Storage paths

Future production leads:

production/leads.jsonl

Future test leads:

test/leads.jsonl

Existing root-level `leads.jsonl` must not be used for future production records.

### Allowed v1 fields

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

### Excluded v1 fields

- phone
- ip

### Always-prohibited fields

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

### Validation

Future backend must use server-side validation with a hardcoded allowlist.

Unexpected fields must be rejected server-side.

Client-side validation alone is not sufficient.

### Anti-abuse

Cloudflare Turnstile or equivalent abuse protection is required before public form submission.

Rate limiting should be used where available.

No visitor IP should be stored in the lead record.

### Consent

Store only:

consent_acknowledged: true

Consent wording must live in version-controlled documentation.

Approved candidate consent text:

"I agree that Nonaym may use this information to respond to my inquiry and provide product availability updates. Do not send passwords, payment information, router credentials, IP addresses, or private network details."

### Retention

Recommended retention:

- Test leads: delete within 30 days when no longer needed
- Real leads: retain up to 12 months after last interaction
- Deletion requests: respond within 30 days where reasonable

Retention must have an enforcement method before production use.

Preferred enforcement:

- R2 lifecycle rule, if available and appropriate

Temporary bridge:

- documented monthly manual cleanup

### Review process

Monthly review should confirm:

- R2 bucket remains private
- no raw lead files are committed to Git
- production/test records remain separated
- no unexpected schema fields are present
- retention cleanup has been performed
- contact inbox is operational

## Danno review

Phase 9F guardrails plan reviewed by Hermes/Danno.

Danno result:

DANNO_PLAN_OK

## Phase 9F conclusion

Phase 9F closes the design guardrail gap only.

It does not approve implementation.

## Required before implementation planning

Before implementation planning:

1. Verify contact@nonaym.ai or choose another monitored inbox.
2. Approve Privacy Policy v3.
3. Confirm Cloudflare Turnstile approach.
4. Confirm R2 lifecycle/manual retention approach.
5. Confirm R2 bucket public access remains disabled.
6. Confirm Danno approval for implementation plan.

## Recommended next phase

Phase 9G — Nonaym Contact Inbox Verification and Privacy Policy v3 Prerequisites
