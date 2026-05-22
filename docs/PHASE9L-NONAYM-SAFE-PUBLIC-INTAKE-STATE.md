# Phase 9L — Nonaym Safe Public Intake State

Date: 2026-05-22

## Purpose

Document the current safe public intake state for Nonaym.ai after completion of Phases 9A through 9K.

This document is intended as a handoff/reference note before future work resumes on `/api/leads`, lead intake, downloads, checkout, or customer dashboards.

## Production source of truth

Working repo:

~/.openclaw/workspace/websites/nonaym-website-production

GitHub repo:

mslepikas/nonaym-website

Branch:

main

Live site:

https://nonaym.ai

## Latest confirmed production commit

8726692 nonaym.ai v1.2.3-build003 make contact flow email-only

## Current public intake state

Nonaym.ai currently uses an email-only public intake flow.

Public customer contact path:

contact@nonaym.ai

Approved current uses:

- general questions
- product interest
- waitlist interest
- DIY compatibility questions
- RFQ questions
- privacy/deletion requests

## Completed safety prerequisites

### Contact inbox

contact@nonaym.ai has been verified as receiving email.

### DMARC

DMARC is configured and verified:

_dmarc.nonaym.ai

TXT value:

v=DMARC1; p=quarantine; adkim=r; aspf=r; pct=100

### Privacy page

Privacy Policy is live:

https://nonaym.ai/privacy/

Published version:

v3.3

Effective date:

May 21, 2026

### Security page

Security guidance page is live:

https://nonaym.ai/security/

Purpose:

Tell visitors not to send passwords, router credentials, payment details, IP addresses, serial numbers, private network details, tokens, or admin credentials.

## Current live form state

Homepage:

No live form fields.

RFQ page:

No live form fields.

Verified absent from live homepage and RFQ page:

- <form>
- </form>
- <input>
- <select>
- <textarea>
- onsubmit

## Current backend state

No active public lead backend is approved or live.

Confirmed absent / deferred:

- no /api/leads
- no functions/
- no api/
- no wrangler.toml
- no live R2 writes
- no payment or checkout
- no customer dashboard
- no live DIY download

## R2 lead storage note

Cloudflare R2 bucket exists:

nonaym-leads

Existing root-level object:

leads.jsonl

Status:

Test-only records confirmed by user.

Decision:

Do not treat existing R2 records as real customer data.

Do not use root-level leads.jsonl for future production records.

Future production/test separation if R2 is used:

- production/leads.jsonl
- test/leads.jsonl

## Future lead intake guardrails

Before any real `/api/leads` implementation:

1. Danno must review and approve implementation plan.
2. Server-side schema allowlist must be used.
3. Unexpected fields must be rejected server-side.
4. IP address must not be stored in lead records.
5. Phone number must not be collected in v1 unless separately justified and disclosed.
6. Cloudflare Turnstile or equivalent anti-abuse control should be used before public form submission.
7. Retention enforcement must be documented.
8. Privacy Policy must be updated if collection changes.
9. Raw lead files must never be committed to Git.
10. R2 bucket must remain private.

## Current approved customer-facing message

Current public wording should direct users to:

contact@nonaym.ai

and remind them:

Do not send passwords, router credentials, payment details, IP addresses, serial numbers, or private network information.

## Not approved yet

The following remain not approved:

- live `/api/leads`
- R2-backed public form submission
- customer dashboard
- payment/checkout
- live DIY download
- phone collection
- IP storage in lead records
- automated marketing/waitlist mailing list without explicit consent

## Recommended next work options

Recommended next safe phases:

### Option A — Phase 10A: DIY Product Requirements

Define minimum hardware requirements for Nonaym DIY before any download or ordering flow.

### Option B — Phase 10B: DIY Readiness Questionnaire Draft

Create a static, non-submitting readiness checklist that helps users decide whether their old computer can run Nonaym DIY.

### Option C — Phase 10C: R2 Test Data Cleanup

Move or delete old test-only R2 records so root-level leads.jsonl is not confused with future production data.

### Option D — Phase 10D: /api/leads Implementation Plan

Design but do not build a reviewed Cloudflare Pages Function for future lead intake.

## Current operating rule

Nonaym.ai is safe for public viewing and email-only inquiry.

Do not re-enable forms or lead collection without a new Danno-reviewed phase.
