# Craft Household Index Page — Design Brief v1
**For:** Claude Design
**From:** Mapme Data Team
**Date:** 2026-05-11
**Reference prototype:** `mapme-prototype.html`
**Working product name:** `craft-household-index`

---

## Naming Note

The current file name `mapme-prototype.html` is misleading. In product terms, this page is the **craft household index**:
- it is the index into the craft-household corpus
- it is the map-first discovery surface
- it sits upstream of every household detail page

Use `craft-household-index` as the working name in design language, documentation, and internal references.

If a more user-facing label is needed later, it can become:
- `Bản đồ hộ làng nghề`
- `Craft Household Atlas`
- `Craft Household Map`

For now, the functional name is more useful than a marketing name.

---

## What This Page Is

This page is the **decision surface** before the household detail page.

The user does not come here to read long stories. They come here to:
- orient themselves geographically
- browse and compare households
- understand what kinds of households exist
- decide which household is worth opening next

This page sits between the landing page and the household detail page. It is the front door of the `community` MVP.

The household detail page is the deep profile / storefront / story surface.
This page is the high-signal map index that gets the visitor there.

---

## Core Product Job

Help a user move from:

`I know nothing about these households`

to:

`I know which household I want to open, and why`

That is the entire job.

If the page becomes too editorial, too busy, or too abstract, it fails. If it becomes a sterile GIS UI with no emotional signal, it also fails.

---

## MVP Promise of This Page

Browse a curated map of craft households in Vietnam, compare households through a few meaningful signals, and open rich detail pages for the ones you care about.

---

## Audience

This page serves multiple audiences at once:

- **Researchers / officials**
  They need fast orientation, filtering, and confidence about what each household represents.

- **Designers / brands / buyers**
  They need a fast way to spot relevant craft types, material worlds, and households worth contacting.

- **Funders / NGOs**
  They need to quickly identify households by craft, place, and vulnerability / continuity signals.

- **Travelers / apprentices / the curious**
  They need to browse intuitively and feel invited into a household’s world.

This page should not assume expert GIS literacy.

---

## Relationship to the Household Detail Page

The household detail page should not solve first-contact orientation. This page should.

Before a visitor clicks into a household detail page, this page should already have shown:
- artisan name
- craft type
- village / province context
- succession signal
- one-line emotional or practical hook

The detail page can then spend its best real estate on identity, story, process, economics, and connection actions.

---

## Design System

Inherit the visual system from `mapme-prototype.html`. Do not diverge from the established dark theme, spacing rhythm, typography pairing, or interaction tone unless a specific problem in the prototype requires correction.

Claude Design will receive `mapme-prototype.html` directly and should sort the design-system details from there.

This brief focuses on product behavior, information hierarchy, and page structure.

---

## Page Architecture

This should remain a map-first page, but the current prototype should be reworked into a clearer index experience.

Recommended structure:

```
1.  HEADER / CONTEXT BAR        — identity, back-to-community, search entry
2.  PAGE INTRO                  — what the atlas is + high-value orientation
3.  FILTER & SIGNAL RAIL        — craft, province, succession, etc.
4.  MAP + INDEX LAYOUT          — map canvas + selected household panel
5.  HOUSEHOLD PREVIEW LAYER     — what appears before detail-page click
6.  OPTIONAL SUPPORTING MODULES — only if they help the click decision
```

This is not a long scrolling editorial page. The map and the preview state are the core of the experience.

---

## Information Hierarchy

### Primary
- map
- household selection
- preview card / preview panel
- filtering
- click-through to household detail page

### Secondary
- summary counts
- featured or highlighted household
- craft-family signals
- succession signal explanation

### Tertiary
- editorial flourishes
- persona-specific demo content
- large narrative blocks

If tertiary material competes with map selection, cut it.

---

## What the Page Must Let the User Do

The MVP index page must support:
- search place or household
- filter households
- scan the map visually
- click a marker
- inspect a preview without committing to the detail page yet
- move into the household detail page

It should also support lightweight comparative browsing:
- same craft
- same province
- same succession state

---

## Required Household Preview Contract

The preview state is the most important design problem on this page.

Every selected household preview must include:
- artisan name
- craft type
- village + province
- succession signal
- one-line hook
- detail-page CTA

Strongly recommended additions if they fit without clutter:
- key material
- years of experience or birth year
- one product or output signal
- one confidence / curation signal

The preview should feel like:
- enough to choose
- not enough to replace the detail page

It must create curiosity and confidence at the same time.

---

## Succession Signal

Succession is a primary emotional and comparative axis on this page.

It should be visible before the user opens the household detail page.

Minimum requirement:
- clear visual signal on marker selection and preview
- understandable label
- quick explanation available without leaving the page

The user should be able to distinguish:
- passing on / training successors
- no successor yet
- last generation

Do not make the user decode a numeric code.

---

## Map Behavior

The map is not just decoration. It is the primary navigation mechanism.

The page should feel like a map product first, but a humane one.

Required map behaviors:
- clear marker click state
- visible selected household state
- stable navigation between markers and preview
- ability to filter without losing orientation

Do not overload the map with too many simultaneous legends, statistics, and side modules.

The map should answer:
- where is this household?
- what kind of craft is here?
- why might I open it?

---

## List / Summary Behavior

The page should not force the user to browse only through markers.

There should be a secondary browsing state that helps:
- keyboard / search-oriented users
- comparison across households
- users scanning multiple households in the same region or craft family

This can be:
- a side panel list
- a selected-household rail
- a compact results list under filters

The exact UI is up to the designer, but it must remain subordinate to the map.

---

## Filters

The filter model should stay small and meaningful.

Recommended MVP filters:
- craft family / craft type
- province
- succession state

Optional if it stays clean:
- material
- active / recognized / revival status

Do not build an enterprise filter wall.

The page must feel curated, not bureaucratic.

---

## CTA Model on This Page

This page does **not** support direct ordering.

This page’s primary CTA is:
- open household page

Secondary CTAs can include:
- clear selection / compare another
- jump to a highlighted household
- explain succession signal

Connection actions like message / collaborate / visit belong primarily on the household detail page, not here.

This page should optimize for:
- discovery
- selection
- click confidence

not for direct outreach.

---

## Content Tone

This page should feel:
- clear
- curated
- alive
- trustworthy

It should not feel:
- like a GIS portal
- like a spreadsheet on a map
- like a story page trying to do the job of the detail page

The emotional tone should come from the preview signals and craft identity, not from long paragraphs.

---

## Recommended Structural Changes from Current Prototype

The current prototype is useful, but the next pass should improve these things:

### 1. Strengthen the map-to-detail journey
- make the preview layer more explicit
- make the household click decision easier
- make the detail-page entry CTA unmistakable

### 2. Reduce non-essential demo content
- remove or downgrade content that does not help a user choose a household
- do not let persona demo devices dominate the page structure

### 3. Clarify what the page indexes
- households first
- village and province as context
- craft family as a major comparative axis

### 4. Make the selected state feel premium
- the selected household panel should feel intentional and desirable
- not like a generic popup or admin side panel

### 5. Make the page scalable
- it should feel capable of growing from a curated first-trip set to a much larger national corpus

---

## Data Assumptions

This brief is grounded in the first field-trip household data and the current craft-household MVP.

The page should assume household-level data can include:
- artisan name
- craft type
- village and province
- coordinates
- succession status
- short narrative hook
- products or output hints
- media readiness in later iterations

Do not assume every household has full media or full narrative on this page. This page is the index, not the archive dump.

---

## Empty / Missing Data Behavior

If some households have missing fields:
- do not hide the household entirely
- degrade gracefully
- prioritize showing what helps a user still decide whether to open the page

For example:
- missing product → omit that preview field
- missing hook → fall back to a concise craft/location line
- missing media → keep preview clean; do not insert broken image slots here

This page should remain strong even with uneven records.

---

## Mobile Behavior

Desktop is the priority, but mobile should remain coherent.

On mobile:
- map remains primary
- filters must collapse cleanly
- selected household preview must remain easy to dismiss and easy to advance from
- opening the detail page should still feel like the primary next step

Do not recreate the full desktop side-panel density on mobile.

---

## Success Criteria

The page is successful when:

1. A first-time user can understand within seconds that this is a map of craft households, not just villages or generic craft categories.
2. A user can compare multiple households without opening each detail page blindly.
3. The selected-household state clearly answers: who is this, what do they make, where are they, what is at stake, why open this page.
4. The transition from map to household detail feels like a natural deepening, not a context switch.
5. The page still feels premium and human, not bureaucratic.
6. The page can scale beyond the first curated set without structural redesign.

---

## One Last Thing

The household detail page is where the visitor forms a relationship.
This page is where the visitor chooses where to begin.

If the current design helps users admire the interface but not choose a household confidently, it is failing the product.
