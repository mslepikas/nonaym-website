# Phase 9E — Nonaym Lead Intake Redesign Result

Date: 2026-05-21

## Result

APPROVED WITH MODIFICATIONS

Phase 9E design is sound in principle, but it is not approved for implementation until additional security guardrails are resolved.

## Danno decision

Danno reviewed the lead intake redesign and gave:

APPROVE WITH MODIFICATIONS

Do not proceed to Phase 9F implementation until the guardrails listed below are resolved.

## Approved design direction

- Use email-only first for early intake.
- R2 may be used later for v2+.
- Use `production/leads.jsonl` for future production records.
- Use separate test and production paths.
- Do not mix test and production records.
- Exclude phone from v1.
- Exclude IP addresses from lead records.
- Add Cloudflare Turnstile before any public form.
- Use contact form first, RFQ next.
- Keep `/api/leads` deferred until security guardrails are completed.

## Proposed approved v1 lead schema

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

## Explicitly excluded from v1

- phone
- ip

## Required guardrails before implementation

1. R2 bucket must remain private with no public read access.
2. Pages Function access must be least-privilege.
3. Pages Function must validate fields server-side with a hardcoded allowlist.
4. Unexpected fields must be rejected server-side.
5. Rate limiting or Cloudflare Turnstile must be added before public form submission.
6. Retention must have an enforcement method, not just a policy.
7. Consent checkbox must store only `consent_acknowledged: true`.
8. Consent wording must live in version-controlled documentation.
9. R2 bucket access/log review process must be documented.
10. Test records should be moved or deleted before production use.

## Retention decision

12 months is reasonable for real lead records, but implementation requires an enforcement mechanism.

Possible enforcement methods:
- R2 lifecycle rule
- scheduled cleanup job
- manual documented monthly cleanup process as a temporary bridge

## Not approved yet

This phase does not approve:

- live `/api/leads`
- public R2-backed form submission
- phone collection
- IP storage in lead records
- payment/checkout
- customer dashboard
- live DIY download

## Recommended next phase

Phase 9F should NOT be implementation yet.

Recommended next phase:

Phase 9F — Nonaym Lead Intake Guardrails

Purpose:
Resolve the Danno-required guardrails before building `/api/leads`.

