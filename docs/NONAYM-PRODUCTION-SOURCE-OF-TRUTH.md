# Nonaym.ai Production Source of Truth

Date recorded: 2026-05-20

## Correct production website/repo

The correct Nonaym.ai production working copy is:

~/.openclaw/workspace/websites/nonaym-website-production

The correct GitHub production repo is:

mslepikas/nonaym-website

The correct production branch is:

main

The live production site is:

https://nonaym.ai

## Important warning

Do NOT use the older/reference repo as the production source:

~/.openclaw/workspace/websites/nonaym-ai

That older working copy is tied to:

mslepikas/nonaym-site

That repo/path caused confusion because it accepted commits and pushes, but Cloudflare production was not using it.

## Current confirmed production state

Latest production commits confirmed live:

0d4eca4 nonaym.ai v1.2.1-build002 restore logo assets
8b5dc34 nonaym.ai v1.2.1-build001 public info pages

Live site confirmed:
- Contact link present
- RFQ link present
- Download link present
- Nonaym DIY — Coming Soon
- Nonaym Lite — In Planning
- Nonaym AI — Later This Year
- Logo restored/fixed

## Helper issue to repair

The helper command:

nonaym-predeploy-capture

was observed scanning the old path:

~/.openclaw/workspace/websites/nonaym-ai

even when run from:

~/.openclaw/workspace/websites/nonaym-website-production

Before the next production Nonaym change, repair this helper so it reviews the correct production repo:

~/.openclaw/workspace/websites/nonaym-website-production

## Required future workflow

For future Nonaym.ai production changes:

1. Work from:
   ~/.openclaw/workspace/websites/nonaym-website-production

2. Confirm:
   git branch --show-current
   git remote -v
   git status -sb

3. Production branch should be:
   main

4. Production remote should be:
   git@github.com:mslepikas/nonaym-website.git

5. Run corrected predeploy review.

6. Danno must approve before commit/push/deploy.

7. Commit and push only from the production repo.

Do not commit or push Nonaym production changes from the old nonaym-ai / nonaym-site repo.
