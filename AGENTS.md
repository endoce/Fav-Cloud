# AGENTS.md

## Purpose

This repository is maintained across devices and AI sessions. Treat GitHub branch `master` as the source of truth.

## Required startup sequence

Before changing anything:

1. Read `AI_README.md`.
2. Read the current-state section at the top of `WORKLOG.md`.
3. Inspect the latest relevant files and recent commits.
4. Confirm that the file version being edited is still current.

## Working rules

- Preserve this project as a lightweight, dependency-free static site unless the user explicitly approves an architectural change.
- Keep the default theme dark and do not restore a background image without explicit approval.
- Keep no more than eight bookmark categories. Preserve the `OTHERS` category for lower-frequency links.
- Keep link counts automatic; do not hard-code category totals.
- Preserve responsive desktop and mobile layouts.
- Network detection must run only after an explicit user click.
- Mainland-route detection uses the mainland-hosted PConline JSONP endpoint.
- Google-route detection uses `https://google-ip.crownpartnersgroup.com/`.
- Public IP addresses must remain masked by default.
- Never add passwords, API tokens, cookies, private keys, full personal IP addresses, or other secrets to this public repository.
- Do not delete or replace Cloudflare resources, DNS records, links, or user data unless the user clearly authorizes that exact action.
- Preserve unrelated user changes and avoid destructive Git operations.

## Completion checklist

Before handing off work:

1. Verify changed links, markup, and JavaScript in proportion to the change.
2. Confirm the page still works as a static GitHub Pages site.
3. Update the current state and recent history in `WORKLOG.md`.
4. Commit changes with a concise, descriptive message.
5. Report what changed, what was verified, the commit SHA, and anything still pending.

## Documentation responsibilities

- Update `AI_README.md` only when architecture, durable decisions, external services, or operating rules change.
- Update `WORKLOG.md` after every material repository change.
- Keep `WORKLOG.md` concise. Record outcomes and handoff facts, not private reasoning or complete chat transcripts.
