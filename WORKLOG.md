# Worklog

This file is the concise cross-device handoff record for humans and AI agents. Read `AGENTS.md` and `AI_README.md` before acting.

## Current state

- Last synchronized: 2026-08-27 (Asia/Shanghai)
- Repository: `endoce/Fav-Cloud`
- Branch: `master`
- Published sites: https://endoce.github.io/Fav-Cloud/ and https://fav-cloud.pages.dev/
- Last functional baseline commit: `3d4ddfa0ad267d53af14eb9f6fa08b07f5e7084f`
- Status: deployed on GitHub Pages and Cloudflare Pages
- Active work: none
- Blockers: none

## Current behavior

- Pure static GitHub Pages site with no build step or runtime dependency
- Modern responsive card layout
- Dark theme by default; light theme available
- Eight bookmark categories
- Tailscale is listed in `CLOUD`
- RFCHOST is listed in `OTHERS`
- Linkding is listed in `PROJECTS`
- Network panel checks mainland and Google/international exits on demand
- Mainland detection uses the PConline JSONP endpoint
- International detection uses `google-ip.crownpartnersgroup.com`
- IP addresses are masked by default
- The panel reports whether the two observed exits differ

## External resources

- GitHub Pages: https://endoce.github.io/Fav-Cloud/
- Cloudflare Pages: https://fav-cloud.pages.dev/ (project `fav-cloud`, source `master`, no build command, output directory `/`)
- Linkding: https://link.crownpartnersgroup.com/
- Active international IP endpoint: https://google-ip.crownpartnersgroup.com/
- Cloudflare Worker: `fav-cloud-ip-check`
- Legacy, currently unused page endpoint: `cn-ip.crownpartnersgroup.com`

Do not delete or reconfigure external resources without explicit user authorization. Do not record credentials or complete personal IP addresses here.

## Known considerations

- The mainland JSONP service is a third-party dependency and may occasionally time out or change response fields.
- The split-route result depends on the user's local proxy rules.
- The legacy `cn-ip` custom domain may still be bound in Cloudflare even though the page no longer calls it.
- The project intentionally favors speed and simplicity over dashboard-style integrations.
- Direct edits to `master` from multiple devices can conflict. Fetch the latest version before every write.

## Next candidates

No feature is currently approved or in progress. Previously discussed possibilities include:

- fuzzy search and keyboard navigation
- selective service-status indicators
- small improvements inspired by Homer or Homepage

Treat these as ideas, not authorized work.

## Handoff protocol

At the start of a new task:

1. Fetch the latest `master`.
2. Read `AGENTS.md`, `AI_README.md`, and this current-state section.
3. Review recent commits relevant to the request.
4. Confirm there is no newer overlapping change.

At the end of a material task:

1. Update the current state above.
2. Add one concise entry under Recent changes.
3. Include the date, outcome, important decision, verification, and commit reference when available.
4. Keep entries factual and omit private chain-of-thought or credentials.

## Recent changes

### 2026-08-27

- Created Cloudflare Pages project `fav-cloud` from `endoce/Fav-Cloud` branch `master`.
- Deployed the dependency-free static site with no build command and output directory `/`.
- Verified that the page and mainland exit check load successfully at https://fav-cloud.pages.dev/.
- Updated Worker `fav-cloud-ip-check` to allow both `https://endoce.github.io` and `https://fav-cloud.pages.dev`, with `Vary: Origin`.
- Verified both deployments return mainland and Google/international exit data and report split routing as normal.
- Preserved the existing GitHub Pages deployment and made no DNS or custom-domain changes.

### 2026-08-26

- Added the cross-device AI handoff system: `AGENTS.md`, `AI_README.md`, and `WORKLOG.md`.
- Moved RFCHOST from `CLOUD` to `OTHERS`.
- Added Tailscale to `CLOUD`, linking to the Machines admin console.
- Functional change commit: `3d4ddfa0ad267d53af14eb9f6fa08b07f5e7084f`.

### 2026-08-04

- Switched mainland-route detection from the Cloudflare Worker hostname to PConline's mainland-hosted JSONP endpoint.
- Retained the Cloudflare Worker for the Google/international route.
- Added explicit reporting for identical versus different exit addresses.
- Documented the updated route-detection architecture.
- Relevant commits: `d323667e76858cf9cb7cdb2ddea8c95c625a23fd`, `f2454f2ff07b9eeb7983b0a8813e5d895c5ad0fe`.

### 2026-08-03

- Added simultaneous mainland and Google/international exit display.
- Created and deployed Cloudflare Worker `fav-cloud-ip-check`.
- Bound `cn-ip.crownpartnersgroup.com` and `google-ip.crownpartnersgroup.com`.
- Relevant commit: `69b839031350aae7ee66bc3656d83b6a54899710`.

### 2026-07-29 to 2026-08-01

- Reorganized all bookmarks into no more than eight categories while preserving `OTHERS`.
- Reworked the page into a modern background-free design with dark mode as the default.
- Fixed HTTPS and language details and added the public README.
- Added Linkding and corrected its displayed name.
- Added the opt-in network status panel.
