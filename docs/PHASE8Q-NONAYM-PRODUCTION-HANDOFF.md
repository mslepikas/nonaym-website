# Phase 8Q — Nonaym Production Handoff

Date: 2026-05-20

## Status

Nonaym.ai production repo path and review helper have been corrected and validated.

## Production source of truth

Working repo:

~/.openclaw/workspace/websites/nonaym-website-production

GitHub repo:

mslepikas/nonaym-website

Branch:

main

Live site:

https://nonaym.ai

## Do not use as production

Old/reference working repo:

~/.openclaw/workspace/websites/nonaym-ai

Old/reference GitHub repo:

mslepikas/nonaym-site

This repo may still exist for reference, but it must not be used for production commits, pushes, or deploys.

## Latest confirmed production commits

b1f85bd document nonaym production source of truth
0d4eca4 nonaym.ai v1.2.1-build002 restore logo assets
8b5dc34 nonaym.ai v1.2.1-build001 public info pages

## Live site confirmed

The live site includes:

- Contact link
- RFQ link
- Download link
- Nonaym DIY — Coming Soon
- Nonaym Lite — In Planning
- Nonaym AI — Later This Year
- Restored logo assets

## Helper validation

The `nonaym-predeploy-capture` helper was repaired and guardrail-tested.

When run from the old repo:

~/.openclaw/workspace/websites/nonaym-ai

it still reviewed the correct production repo:

~/.openclaw/workspace/websites/nonaym-website-production

Phase 8P guardrail result: PASSED.

## Reviewer notes

Q previously overclaimed implementation during Phase 8O by saying the helper was repaired after only reviewing the plan.

Going forward:
- Treat Q as a technical helper only.
- Verify Q claims with shell output.
- Treat Danno as the security/privacy gate.
- Human approval remains required before commit, push, deploy, service change, or Cloudflare action.

## Future Nonaym workflow

Before any future Nonaym production work:

1. Start from:

   cd ~/.openclaw/workspace/websites/nonaym-website-production

2. Confirm:

   pwd
   git branch --show-current
   git remote -v
   git status -sb

3. Run:

   nonaym-predeploy-capture
   hermes-review ~/.hermes/audits/nonaym-predeploy-output-LATEST.md

4. Only commit/push/deploy after Danno review and human approval.

## Restrictions

Do not start Hermes gateway mode.
Do not start mobile_dispatcher service mode.
Do not use port 18889.
Do not commit/push/deploy from the old nonaym-ai repo.
