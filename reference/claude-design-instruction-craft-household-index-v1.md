# Instruction to Claude Design — Craft Household Index Prototype v1

**From:** Mapme Data Team
**Date:** 2026-05-11
**You will produce:** one improved standalone HTML prototype file for the craft-household index page
**Brief:** `reference/craft-household-index-brief-v1.md` (read in full before starting)
**Reference prototype:** `mapme-prototype.html` (inherit design system; do not diverge casually)

---

## Context You Need

This page is the upstream discovery surface for the `community` MVP.

The current file name `mapme-prototype.html` is misleading. Product-wise, this page is the **craft household index**: the map-first discovery layer that sits between the landing page and the household detail pages.

The household detail pages do the deep work:
- artisan identity
- story
- process
- economics
- succession
- connection actions

This index page does the selection work:
- orientation
- filtering
- comparison
- click confidence

If the page does not help a user decide which household to open, it is not doing its job.

---

## Deliverable

Produce one improved prototype file, conceptually replacing `mapme-prototype.html`.

Recommended filename:
- `craft-household-index.html`

If file renaming is not desired in the prototype handoff, keep the output as `mapme-prototype.html` but treat it internally as the craft-household index page.

The design system comes from the current `mapme-prototype.html`; do not create a new visual language.

---

## What Must Improve

The current prototype is a useful starting point, but the next pass must improve these specific product behaviors:

1. **Clarify what is being indexed**
   - households first
   - village and province as context
   - craft family as a comparative axis

2. **Strengthen the selection moment**
   - the user should not click a marker blindly
   - the preview state must feel informative and intentional

3. **Strengthen the journey to the household page**
   - the click into the detail page must feel like the obvious next move
   - the index page should tee up the detail page, not compete with it

4. **Reduce demo noise**
   - content that exists only to show possible directions should not dominate the page
   - persona demo structures should not drive the page architecture if they interfere with the actual MVP job

5. **Make the page scalable**
   - it should look like a page that can grow from a curated first-trip set into a larger atlas

---

## Core Interaction Contract

The page must support:
- search place or household
- filter households
- browse via map
- select a marker
- inspect a household preview
- open the household detail page

The page should also support light comparison through a small number of meaningful signals:
- craft family / craft type
- province
- succession state

Do not overcomplicate the interaction model beyond that.

---

## Required Preview Contract

Before a user clicks into the detail page, the selected-household preview must show:
- artisan name
- craft type
- village / province
- succession signal
- one-line emotional or practical hook
- detail-page entry CTA

Strongly recommended if it fits cleanly:
- material
- experience / year signal
- one product or output hint

The preview should make the detail-page click feel justified.

It should not become a mini detail page.

---

## Page Structure Guidance

Design the page around a map-first index layout.

Suggested structure:

1. **Top bar / identity layer**
   - page title / context
   - search
   - lightweight orientation

2. **Filter rail**
   - compact, high-signal
   - likely craft / province / succession

3. **Main map experience**
   - map canvas as the anchor
   - selected state clearly visible

4. **Preview / index panel**
   - where the user decides whether to open the household page

5. **Optional supporting modules**
   - only if they improve selection confidence
   - not if they distract from the map

This should not become a long scrolling content page.

---

## Relationship to the Household Detail Page

Assume the detail page will handle:
- long-form story
- full product showcase
- process walkthrough
- workshop layout
- economics
- succession narrative
- connection actions like message / collaborate / visit

Therefore this index page should **not** spend its best real estate on:
- long prose
- full profile detail
- heavy storytelling
- direct outreach forms

Its job is to help the user choose where to go deeper.

---

## CTA Model

This page is **not** a direct-ordering surface.

Its primary CTA is:
- open household detail page

It may also support small secondary page-level actions like:
- clear filters
- browse related households
- jump to featured selection

It should not try to route message / collaboration / visit directly from the map page unless a very strong reason emerges later. Those belong primarily on the household detail page.

---

## Map Behavior Expectations

The map should:
- feel primary, not decorative
- support clear selected-marker behavior
- preserve orientation while filtering
- make it obvious which household is active

Do not overload the map with too many simultaneous overlays, legends, and explanatory blocks.

The user should be able to answer quickly:
- where is this household?
- what kind of craft is it?
- why might I open it?

---

## Filter Expectations

Keep filters small and meaningful.

Recommended filters:
- craft family / craft type
- province
- succession state

Optional only if they remain lightweight:
- material
- status / recognition

Avoid turning this page into a dense enterprise dashboard.

---

## What to Reuse from the Current Prototype

Reuse from `mapme-prototype.html` where still effective:
- overall dark visual system
- typography tone
- marker-led browsing
- craft-family coloring logic
- general sense of warmth and curation

Do not preserve structure just because it exists.

If a current section does not help the user choose a household, demote it or cut it.

---

## What to Avoid

Avoid these failure modes:

- a generic GIS portal
- a long editorial page with a map embedded inside it
- a cluttered side panel that feels administrative
- marker clicks that reveal too little to justify a next step
- a page that duplicates the household detail page instead of funneling into it

---

## Data Assumptions

Ground the design in the current craft-household MVP.

Assume household-level records may provide:
- artisan name
- craft type
- village / province
- coordinates
- succession state
- one-line hook
- product or output hints

Do not assume every household has equally rich data on the index page.

Build graceful preview fallbacks.

---

## Mobile Guidance

Desktop-first, but mobile must stay coherent.

On mobile:
- map remains central
- filters collapse cleanly
- selected preview is easy to open and dismiss
- opening the detail page remains the primary next action

Do not simply shrink the desktop layout without rethinking density.

---

## Success Criteria

You are done when:

1. The page reads immediately as a map of craft households, not just villages or craft categories.
2. A user can compare households without opening them blindly.
3. The selected-household preview clearly explains why that household matters.
4. The detail-page CTA feels like the natural next step.
5. The page still feels premium, humane, and Mapme-native.
6. The page appears structurally capable of scaling beyond the first curated set.

---

## One Last Thing

The household detail page is where the visitor forms a relationship.
This page is where the visitor chooses where to begin.

Design for that decision.
