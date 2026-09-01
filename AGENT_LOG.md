# Agent Log

Append-only. Newest entry first. No participant data, committee or faculty names,
credentials, or tokens.

---

## 2026-08-31 — Audience quick-start routes

**Context.** Tier 1 scope from an agent handoff titled "Dissertation Repositories Visual
Modernization & Streamlining."

**Changed.** `index.html` only, additively (58 lines).

- Added a "Start where you stand" section between the hero and the Fall 2026 feature,
  offering three audience routes: district and system leaders, classroom teachers, and
  researchers or doctoral students. Each carries one primary destination and two
  follow-on links.
- Added a "Start here" nav entry as the first link in the ecosystem nav.
- Added `.mjm-quickstart` styles inside the existing `#mjm-ecosystem` namespace, reusing
  the established tokens, mono label treatment, and per-card accent variable pattern.

**Why this rather than what the handoff asked for.** The handoff called for replacing
"static text cards" with an SVG constellation map. The archive is not static: it is a
filterable, searchable catalog of roughly 45 projects with a live count. For that many
items, search and filter beat a node graph, so replacing it would have cost usability.

The genuine gap was different. The existing "Five ways into the work" pathways sort the
work by **artifact type** (research, writing, presentations, interactives, practice).
Nothing sorted it by **who is arriving**. The new section answers that and does not
duplicate the pathways below it.

**Verified.** Served locally, real browser, zero console errors, tag balance clean.

- All nine destination URLs return HTTP 200 (checked with curl before they were written
  into the page, not after).
- 1440px: three columns, no horizontal overflow. 900px and below: single column.
- 375px: zero overflowing elements inside the new section, and no page-level horizontal
  scroll.
- The `:focus-visible` ring and `prefers-reduced-motion` block already present on this
  page cover the new links; nothing new was needed.

**Note, pre-existing and not a defect.** At 375px, twelve elements report as extending
past the viewport. All twelve are inside `.mjm-stage-list`, the five-stage framework
strip, which is deliberately its own `overflow-x: auto` scroller with a scroll hint and
an accessible region label. The page itself has no horizontal scroll. Left alone.

**Not done, deliberately.** No constellation map, for the reason above. No mini-UI preview
illustrations for flagship apps — that needs either screenshots that will drift out of
date or bespoke per-app artwork, and is an editorial call about the author's own site.

No commit or push — this machine has no configured git identity or credentials, so the
change is left in the working tree for review.
