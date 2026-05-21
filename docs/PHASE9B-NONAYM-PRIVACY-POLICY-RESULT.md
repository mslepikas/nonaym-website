# Phase 9B — Nonaym Privacy Policy Draft Result

Date: 2026-05-21

## Result

CLOSED — REVISION NEEDED

The Nonaym.ai Privacy Policy Draft v2 was reviewed by Hermes/Danno.

## Danno decision

Do not publish the v2 privacy policy as-is.

## Main issues found

Danno flagged the following issues:

1. The "Information We Do Not Want You To Send" section reads more like a security FAQ than a privacy policy.
2. Hosting/email/service providers are not named or described specifically enough.
3. Placeholder form behavior is still a liability if users can type and submit data.
4. Retention periods are not specific enough.
5. Incident response language does not include a concrete timeline.
6. Legal-rights language is too vague.
7. Cookie/web technology language is underspecified.
8. Cross-border processing and service-provider roles need more clarity.
9. Future-feature wording should avoid sounding like product roadmap commitments.

## Decision

Do not create or publish /privacy/ yet.

Split the work into smaller phases:

- Phase 9C — Create a public "Security / What Not To Send" page
- Phase 9D — Create Privacy Policy v3 after confirming:
  - email provider
  - website hosting provider details
  - whether analytics are used
  - whether Cloudflare logs/cookies are used
  - whether contact@nonaym.ai is verified
  - retention periods
  - whether forms are disabled, mailto-only, or active

## Current website state remains approved

- Static placeholder pages only
- No /api/leads backend
- No real lead collection
- No payment/checkout
- No live DIY download

## Safety

No website code should be changed from the v2 privacy draft.

Q remains technical helper only.
Danno remains security/privacy/risk gate.
Human approval required before commit, push, deploy, Cloudflare action, or backend/API work.
