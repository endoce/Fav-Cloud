# AI README

This document gives AI agents durable project context. Read it with `AGENTS.md` and the current-state section of `WORKLOG.md` before making changes.

## Project identity

- Repository: `endoce/Fav-Cloud`
- Default branch: `master`
- Published sites: https://endoce.github.io/Fav-Cloud/, https://fav-cloud.pages.dev/, and https://fav.ydht.net/
- Purpose: a personal, fast-loading browser navigation page for frequently used links and lightweight network-route checks
- Primary language: Simplified Chinese, with short English category labels
- Deployment: GitHub Pages and Cloudflare Pages (`fav-cloud`, `master`, no build command, output directory `/`)
- Architecture: dependency-free static HTML, CSS, and JavaScript
- Operating boundary: `endoce/Fav-Cloud` is the sole source and handoff authority for Fav Cloud. Do not select or update Fav Cloud through `personal-infra-ops`; Cloudflare resource operations remain separately scoped and require their own explicit authorization.

## Files

- `index.html`: page structure, inline styles, bookmark data, and interaction logic
- `README.md`: public user-facing project description
- `AGENTS.md`: automatic instructions and safety rules for Codex and compatible agents
- `AI_README.md`: durable architecture and design context
- `WORKLOG.md`: current state, handoff notes, recent work, and pending items
- `FiraCode-Regular.woff2`: local interface font
- `The_Internet.png`: site icon

There is no dependency installation, build command, package manager, framework, or database.

## Design decisions

- Default appearance is dark.
- The page uses a clean modern palette without a background image.
- Cards are responsive and should remain compact, professional, and fast.
- A light theme remains available through the theme toggle.
- Fira Code is used locally to avoid a remote font dependency.
- Bookmark categories are limited to eight:
  - `WEB`
  - `AI`
  - `MEDIA`
  - `CLOUD`
  - `PROJECTS`
  - `MAKER`
  - `RESOURCES`
  - `OTHERS`
- `OTHERS` contains retained links that are used less frequently.
- Category counts are derived automatically from the number of list items.
- Avoid adding frameworks, large icon libraries, analytics, trackers, or unnecessary network requests.

## Current bookmark decisions

- Linkding is the self-hosted bookmark tool at https://link.crownpartnersgroup.com/.
- Uptime Kuma is the self-hosted status monitor at https://up.ydht.net/ and is listed in `PROJECTS`.
- Tailscale is in `CLOUD` and links to its Machines admin console.
- RFCHOST is retained in `OTHERS`.
- The private OctoPrint address is intentionally present for use on the corresponding local network.

When moving a link, remove the original entry and preserve it in the requested destination. Keep the category total at eight or fewer.

## Network status architecture

The bottom panel checks two browser egress paths only after the user clicks the detection button.

### Mainland path

- Endpoint: `https://whois.pconline.com.cn/ipJson.jsp`
- Method: dynamic JSONP script callback
- Reason: the endpoint is hosted in mainland China, making it suitable for observing the direct mainland route without depending on a Cloudflare hostname that may follow proxy rules.
- Displayed information: masked public IP, location/provider data, and observed latency.

### Google/international path

- Endpoint: `https://google-ip.crownpartnersgroup.com/`
- Method: `fetch` returning JSON
- Backend: Cloudflare Worker `fav-cloud-ip-check`
- Intended routing: the client proxy configuration should route this hostname through the same proxy path used for Google.
- Displayed information: masked public IP, city/country, ASN/organization, and observed latency.

The page compares the two returned IP addresses:

- Different addresses: report that split routing appears normal.
- Same address: report that split routing was not detected.
- One failed request: report a partial result without claiming the route is working.

Public IP addresses remain masked unless the user explicitly reveals them with the control in the page.

### Legacy Cloudflare resource

`cn-ip.crownpartnersgroup.com` was previously bound to the same Worker for mainland detection. The page no longer uses it. It may still exist in Cloudflare and must not be deleted without explicit user authorization.

## Cloudflare Worker behavior

The Worker returns JSON containing fields such as:

- `success`
- `ip`
- `city`
- `region`
- `country`
- `asn`
- `organization`
- `colo`

It permits `https://endoce.github.io`, `https://fav-cloud.pages.dev`, and `https://fav.ydht.net`, reflects the matching request origin, sends `Vary: Origin`, and uses no-store cache headers. Do not place credentials in the Worker response or repository documentation.

## Privacy and safety

This is a public repository.

Never commit:

- API tokens or passwords
- Cloudflare session data
- cookies or authorization headers
- private keys
- complete personal IP addresses copied from test results
- private infrastructure details beyond information already intentionally published

Network checks must remain opt-in. Do not add automatic checks on page load.

## Change workflow

1. Fetch the latest `master` version before editing.
2. Inspect `AGENTS.md`, this file, and `WORKLOG.md`.
3. Make the smallest coherent change.
4. Verify that HTML IDs match JavaScript selectors and that links use HTTPS where possible.
5. Verify desktop/mobile behavior when layout changes.
6. Update `WORKLOG.md`.
7. Commit to the authorized branch and report the commit SHA.

For concurrent or larger changes, prefer a branch and pull request. Avoid having two devices directly edit `WORKLOG.md` at the same time.

## Durable product direction

Fav-Cloud should remain closer to a fast personal start page than a full homelab dashboard. Features borrowed from projects such as Homer or Homepage should be implemented selectively and should not compromise static deployment or load speed without explicit user approval.
