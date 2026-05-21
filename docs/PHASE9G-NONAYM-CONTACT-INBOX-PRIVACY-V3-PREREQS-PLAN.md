# Phase 9G — Nonaym Contact Inbox Verification and Privacy Policy v3 Prerequisites Plan

Date: 2026-05-21

## Purpose

Verify the Nonaym public contact path and define the prerequisites for Privacy Policy v3 before any real lead intake is activated.

This phase prepares for future public contact and privacy readiness.

It does not implement `/api/leads`.

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

- Phase 9E documented lead intake redesign.
- Phase 9F documented required lead intake guardrails.
- R2 bucket `nonaym-leads` exists.
- Existing R2 records are confirmed test-only.
- No active `/api/leads` backend exists in production.
- No production repo code currently writes to R2.
- `/security/` page exists and is live.
- `/privacy/` page is not approved yet.
- Contact inbox still needs verification before public customer-intake expansion.

## Phase 9G scope

This phase covers:

1. Verify `contact@nonaym.ai` or choose another monitored contact inbox.
2. Identify what email service/routing handles Nonaym contact mail.
3. Confirm reply path.
4. Confirm who monitors the inbox.
5. Define Privacy Policy v3 prerequisite facts.
6. Create a privacy readiness checklist for future publication.

## Safety rules

No website code changes.
No `/api/leads`.
No R2 writes.
No Cloudflare changes.
No DNS changes.
No deploy.
No live customer intake activation.
No payment/checkout.
No customer dashboard.
No Hermes gateway mode.
No mobile_dispatcher service mode.
Do not use port 18889.

## Contact inbox verification checklist

Verify:

- Can an outside email send to contact@nonaym.ai?
- Does the message arrive?
- Where does it arrive?
- Can a reply be sent?
- Who monitors it?
- How often is it checked?
- Is it acceptable for public Nonaym customer contact?
- Is it acceptable for privacy/deletion requests?

## Test email

Send from an outside email account.

To:

contact@nonaym.ai

Subject:

Nonaym contact inbox verification test

Body:

This is a test to verify that contact@nonaym.ai can receive and reply to Nonaym customer inquiries, privacy requests, and product-interest messages.

## Privacy Policy v3 prerequisite facts to define

Before publishing `/privacy/`, define:

- Contact email
- Monitoring owner
- Expected response process
- Deletion request path
- Website hosting provider
- DNS provider
- Email provider or routing provider
- Future form/backend provider if used
- Future storage provider if used
- Current analytics/cookie status
- Current data collection status
- Future allowed lead fields
- Future excluded lead fields
- Retention/deletion approach
- Link to `/security/`

## Acceptance criteria

Phase 9G is complete when:

- contact inbox verification result is documented
- privacy v3 prerequisite facts are documented
- Danno reviews the result
- no implementation occurs
- optional docs are committed
