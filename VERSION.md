# nonaym.ai Version

Site: nonaym.ai
Current approved version: v1.1.0
Current sandbox build: v1.2.0-build001
Next planned sandbox build: v1.2.0-build001
Last approved/base commit: d2c31d5
Deployment status: approved/current live site; v1.2.0-build001 in sandbox review, Cloudflare form backend not yet wired
Documentation correction note: production documentation was corrected to identify mslepikas/nonaym-website as the production repository. Lead capture, /api/leads, and Cloudflare backend wiring remain not approved unless handled in a separate reviewed phase.
GitHub remote: git@github.com:mslepikas/nonaym-website.git
Legacy/deprecated repo note: git@github.com:mslepikas/nonaym-site.git is not the current production repository unless Mark explicitly re-approves it.

## Versioning Convention

Format:

    SITE vMAJOR.MINOR.PATCH-buildNN

Examples:

    nonaym.ai v1.2.0-build001

Meaning:

    MAJOR = major redesign, product direction change, or site architecture change
    MINOR = new page, new product section, new workflow, or meaningful content block
    PATCH = typo, small copy edit, link fix, image fix, or layout tweak
    buildNN = human approval/build order number for this site

## Approval Rules

Sandbox work can be proposed by Hermes/Q.

Real repo commits require:

1. git status review
2. git diff review
3. Danno review
4. user approval

Public push/deploy requires a separate explicit approval.

Example approval phrases:

    APPROVE: nonaym.ai v1.2.0-build001 for real repo commit only
    APPROVE: push nonaym.ai v1.2.0-build001 to GitHub for Cloudflare deploy

## Domain / Hosting Note

Active business site.
