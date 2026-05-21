# Phase 9G — Nonaym Contact Inbox Verification and Privacy Policy v3 Prerequisites Result

Date: 2026-05-21

## Result

CONTACT INBOX VERIFIED — PRIVACY V3 PREREQUISITES DOCUMENTED

## Contact inbox

Contact address:

contact@nonaym.ai

## Inbox verification

- External test email sent: YES
- Email received: YES
- Reply path confirmed: TBD / expected available through monitored inbox
- Inbox routing/provider: Cloudflare Email Routing confirmed by DNS MX/SPF
- Monitoring owner: Mark
- Monitoring cadence: Manual / TBD
- Approved for public customer contact: YES
- Approved for privacy/deletion requests: YES, as the initial public request path

## Email DNS evidence

MX records:

- route1.mx.cloudflare.net
- route2.mx.cloudflare.net
- route3.mx.cloudflare.net

SPF:

- v=spf1 include:_spf.mx.cloudflare.net ~all

DMARC:

- No DMARC TXT record returned during check

## Current public site data collection

Current production repo does not contain:

- active /api/leads backend
- functions/ directory
- api/ directory
- wrangler.toml

Current forms remain placeholder-only.

No real public form submission is approved in this phase.

## Future lead intake status

Future lead intake remains deferred.

Before real lead intake:

- Privacy Policy v3 must be approved
- Phase 9F guardrails must remain in force
- Contact inbox must remain monitored
- /api/leads implementation must get a separate Danno review

## Privacy Policy v3 prerequisites

### Contact path

Use:

contact@nonaym.ai

For:

- general inquiries
- product interest
- privacy questions
- deletion requests

### Hosting/service providers

Known:

- Website hosting: Cloudflare Pages
- DNS provider: Cloudflare
- Email routing: Cloudflare Email Routing
- Future candidate storage: Cloudflare R2

TBD:

- final analytics/cookie status
- future backend implementation details
- final retention enforcement method

### Current data collection

No real customer data is collected by current production website forms.

Existing R2 `leads.jsonl` records are test-only and should not be treated as production customer data.

### Future approved candidate fields

- name
- email
- product_interest
- use_case
- old_computer_available
- number_of_locations
- message
- consent_acknowledged

### Future excluded fields

- phone in v1
- IP address in lead records
- passwords
- router credentials
- payment information
- private network details

### Retention candidate

- Test leads: delete within 30 days when no longer needed
- Real lead records: retain up to 12 months after last interaction
- Deletion requests: respond within 30 days where reasonable

### Security guidance

Privacy Policy v3 should link to:

/security/

## Not approved in this phase

This phase does not approve:

- live /api/leads
- R2-backed public form submission
- payment/checkout
- customer dashboard
- live DIY download
- phone collection
- IP storage in lead records

## Recommended next phase

Phase 9H — Privacy Policy v3 Draft
