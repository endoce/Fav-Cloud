# AI README

This document gives AI agents durable project context. Read it with `AGENTS.md` and the current-state section of `WORKLOG.md` before making changes.

## Project identity

- Repository: `endoce/Fav-Cloud`
- Default branch: `master`
- Published sites: https://endoce.github.io/Fav-Cloud/, https://fav-cloud.pages.dev/, and https://fav.ydht.net/
- Purpose: a personal, fast-loading browser navigation page for frequently used links
- Primary language: Simplified Chinese, with short English category labels
- Deployment: GitHub Pages and Cloudflare Pages (`fav-cloud`, `master`, no build command, output directory `/`)
- Architecture: dependency-free static HTML, CSS, and JavaScript
- Operating boundary: `endoce/Fav-Cloud` is the sole source and handoff authority for Fav Cloud. Do not select or update Fav Cloud through `personal-infra-ops`; Cloudflare resource operations remain separately scoped and require their own explicit authorization.

## Files

- `index.html`: page structure, inline styles, bookmark data, and interaction logic
- `text-visualizer.html`: standalone bilingual character visualizer with inline styles and scripts, local-only text processing, and shared saved theme preference
- `README.md`: public user-facing project description
- `AGENTS.md`: automatic instructions and safety rules for Codex and compatible agents
- `AI_README.md`: durable architecture and design context
- `WORKLOG.md`: current state, handoff notes, recent work, and pending items
- `FiraCode-Regular.woff2`: local interface font
- `The_Internet.png`: site icon

There is no dependency installation, build command, package manager, framework, or database.

## Design decisions

- Default appearance is light, as approved in the September 8 redesign; existing saved dark preferences remain respected.
- The page uses a clean modern palette without a background image.
- Cards are responsive and should remain compact, professional, and fast.
- A light theme remains available through the theme toggle.
- System sans-serif fonts are used without remote font dependencies. Local SVG brand icons live in `assets/icons`; remaining sites use initials.
- Bookmark categories are limited to eight:
  - `WEB`
  - `AI`
  - `MEDIA`
  - `CLOUD`
  - `HOSTING` (托管与网络)
  - `PROJECTS`
  - `RESOURCES`
  - `OTHERS`
- `OTHERS` contains retained links that are used less frequently. Modify its bookmarks only after explicit user instructions; do not rebalance them automatically.
- Category counts are derived automatically from actual anchors (Hacker News and CN are separate links). Local search filters by category, name, and URL; `/` focuses search and Escape clears it.
- Avoid adding frameworks, large icon libraries, analytics, trackers, or unnecessary network requests.

## Current bookmark decisions

- Linkding is the self-hosted bookmark tool at https://link.crownpartnersgroup.com/.
- Uptime Kuma is the self-hosted status monitor at https://up.ydht.net/ and is listed in `PROJECTS`.
- HomeLab Homepage is the family-LAN homepage at http://192.168.13.220:3001/ and is listed in `PROJECTS`.
- Resend is the email service dashboard at https://resend.com/emails and is listed in `CLOUD`.
- `CLOUD` (云服务) contains Cloudflare, Resend, Oracle Cloud, Azure, and iCloud.
- `HOSTING` (托管与网络; HTML class `networking`) contains GitHub, DMIT, and Tailscale. Tailscale links to its Machines admin console.
- RFCHOST is retained in `OTHERS`.
- The maker category and OctoPrint Pi shortcut were removed at the user’s request. Thingiverse and MakerWorld were moved to `OTHERS`; its five existing bookmarks and their order remain unchanged.

When moving a link, remove the original entry and preserve it in the requested destination. Keep the category total at eight or fewer.

## Text visualizer

- The tool bookmark uses the original local `assets/icons/text-visualizer.svg` character tile icon (A/a/0/#), matching the rounded navy HomeLab icon style and the tool’s category colors.
- The PROJECTS bookmark 信号译码 points to `./text-visualizer.html`; the tool links back to `./` so both root-domain and GitHub Pages subpath hosting work.
- Adapted from `endoce/Codex-Web/text-visualizer.html`, it is now independently maintained in Fav-Cloud. The source repository is retained; its 废土终端 homepage bookmark was removed at the user’s request.
- UI uses Chinese and English, light by default, and the same `theme` storage key as the homepage. Only the theme is persisted; input text is not stored or uploaded.
- Classifies Unicode uppercase/lowercase letters, decimal digits, whitespace, and remaining characters. Displays spaces, tabs and newlines; CRLF and lone CR normalize to LF for display.
- No remote fonts, libraries, backend or build step. Use safe text nodes for all input rendering.

## Former network checker

The homepage no longer provides network exit detection. Its former Cloudflare Worker and DNS resources are managed separately; do not delete or reconfigure them without explicit authorization.

## Privacy and safety

This is a public repository.

Never commit:

- API tokens or passwords
- Cloudflare session data
- cookies or authorization headers
- private keys
- complete personal IP addresses copied from test results
- private infrastructure details beyond information already intentionally published

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
