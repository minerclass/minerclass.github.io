# Agent Log

Append-only. Newest entry first. No participant data, committee or faculty names,
credentials, or tokens.

---

## 2026-08-31 - Ecosystem map: the first diagram in the hub layer

**Why.** A design review across 31 repositories found **zero `<svg>` and zero `<details>`
on every hub page**, measured against the rendered DOM rather than the source. Every hub
was text in boxes; nothing anywhere showed the shape of the thing. This root hub carries
68 project cards, 159 links, and roughly 2,400 words with no orientation graphic at all.

**Changed.** `index.html`: an `.mjm-map` above the catalog filter bar, plus styles and a
render block.

- Six domain nodes, one per catalog category, each an SVG disc in that domain's existing
  accent colour with its count inside.
- **Counts are computed at runtime from the rendered catalog**, not hardcoded, so they
  cannot drift as the catalog grows. Verified against a live tally: 16 / 21 / 7 / 9 / 5 /
  10, totalling the 68 entries present.
- Disc radius scales with the square root of the count, so **area** is proportional to
  volume rather than radius, which would overstate the larger domains.
- Selecting a node dispatches a click on the existing `.mjm-filter` button rather than
  reimplementing the filter, so filtering logic stays in exactly one place. The map also
  listens to those buttons so it stays in step when the filter bar is used directly.

**This is the good version of the handoff's "constellation map".** That idea was declined
earlier because it proposed *replacing* a searchable 68-entry catalog with a node graph,
which would have cost usability. Added above the catalog instead, it gives orientation
without taking away search or filtering.

**Accessibility.** Each node is a real `<button>` with `aria-pressed`, so it is keyboard
operable and announced as a toggle; the SVG inside is `aria-hidden` and decorative. The
count is also rendered as text, so the information does not depend on disc size.

**Verified in a real browser.** Clicking the games node filters the catalog to exactly 9,
matching the tally; the matching filter button reports `aria-pressed="true"`; reset
restores all 68; exactly one node is pressed at a time. At 375px the rail reflows from six
columns to three with **zero** overflowing elements inside the map and no page-level
horizontal scroll. A real Tab keypress moves between nodes and the focused node matches
`:focus-visible`, showing the shared gold ring from the token layer. Zero console errors.

**Note on validation.** A naive tag-balance check reports a false mismatch on this file
because the script builds HTML inside JS strings. Strip `<script>` and `<style>` before
checking; the markup is balanced.

**Pre-existing, unrelated.** At 375px, twelve `.mjm-stage` elements extend past the
viewport. They sit in their own `overflow-x: auto` scroller and cause no page-level
scroll.


---

## 2026-08-31 - Link the shared token file from the root hub

This repo hosts `tokens.css`, and its own `--mjm-*` block was the basis for the canonical
palette, but it was not actually loading the shared file. It now does, via a relative
`tokens.css` link.

**Nothing changes visually.** The local `#mjm-ecosystem` block still defines the same
names with the same values and is more specific, so it continues to win. The point of the
link is that later additions to the shared file, such as the paper-ground accent inks,
the radius and measure tokens, and the shared focus ring, become available here too
without duplicating them.

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
