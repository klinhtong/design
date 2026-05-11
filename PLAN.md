# Mapme MVP Design Lock Plan

## Summary
Mapme MVP is one app with two sections: `community` and `advanced`.

The immediate goal is to stop treating the current HTML files as implicit product truth and instead lock a canonical MVP design that is both high-resolution and technically feasible. The first priority is `community`, specifically the craft-household experience. The second priority is defining the thinnest real `advanced` experience that can launch with available geospatial data and scale as data coverage expands.

This plan should be treated as the working contract for the next design cycle.

## Locked Product Model
### App structure
- One shared app shell
- Two sections:
  - `community`
  - `advanced`

### Community MVP promise
Browse a curated map of craft households in Vietnam and open rich household pages with story, products, and context.

### Advanced MVP promise
Explore layered Mekong geospatial data, inspect places, and extract lightweight spatial insights through filtering and comparison.

### Canonical community entity model
- `village` has many `households`
- `household` is the canonical public-facing entity
- each `household` has one detail page
- each `household` detail page can showcase multiple `products`

## Design Principles
- Current HTML files are exploratory references, not fixed requirements.
- `reference/household-detail-brief-v2.md` is the strongest current contract for the household page and supersedes the earlier v1 household assumptions where they conflict.
- Design should be desktop-first and bilingual (`VN` and `EN`).
- UI quality should be high-resolution and editorial where appropriate, but every major interaction must remain technically feasible.
- The system must be designed for mixed geospatial inputs:
  - `.tif` rasters
  - `GeoJSON`
  - tabular spatial data with coordinates or polygon geometry
- Data availability should constrain implementation, not prematurely narrow the design language.

## Phase 1: Lock the Community MVP
### Objective
Define the canonical `community` experience for MVP around craft households.

### Required decisions
- Treat `community` MVP as:
  - craft household map
  - functional household detail pages
- Defer broader community concepts from the MVP critical path:
  - projects
  - trips
  - open contribution flows
  - broader repository surfaces beyond craft households

### Canonical user flow
1. user enters the app from the landing page
2. user selects `community`
3. user lands on the craft households map experience
4. user searches, filters, or browses households
5. user selects a household
6. user opens the household detail page

### Craft map interaction contract
The MVP craft map must support:
- place or record search
- filtering
- map marker selection
- list or summary browsing state
- click-through to household detail

Lower-priority actions that should not drive the first design pass:
- uploads
- downloads
- natural-language questions
- draw/select area workflows
- built-in commerce flows

## Phase 2: Lock the Household Detail Page
### Objective
Create one canonical household detail page template that can represent most curated households cleanly.

### Household page mental model
- The household page is a storefront and eventual claimable household presence, not just a passive profile.
- The page must support real visitor actions:
  - message
  - collaborate or commission where appropriate
  - visit or learn where appropriate
- The page should not support direct ordering or checkout.

### Detail page content contract
Each household detail page should support:
- hero/title block with succession signal and primary actions
- artisan identity and signature quote
- real media gallery when assets are available, with graceful fallback during prototyping
- short narrative or story summary
- workshop spatial layout / zone diagram
- process walkthrough
- materials and supply-chain context
- economics / viability portrait
- succession / future-of-craft section
- connections to other households across multiple axes
- village context
- product showcase
- methodology / data disclosure in the footer

### Upstream craft-map contract
Before a user opens a household page, the craft-household map should provide enough context to justify the click. For each selected or previewed household, the map experience should surface:
- artisan name
- craft type
- village / province context
- succession signal
- one-line emotional or practical hook
- clear entry into the household page

### What not to treat as primary on the household page
- embedded location map as a core section
- standalone provenance section
- passive “related households” stub cards

The upstream craft-map or village surface handles map navigation. The household page is the deep profile / storefront / story surface.

### Template rule
- There should be one default reusable household detail template for the MVP.
- Richer editorial storytelling can exist as an optional expansion layer for especially curated households later.
- Do not make the MVP depend on every household having a long-form editorial treatment.

### Existing file interpretation
- `mapme-prototype.html` is a useful interaction reference for the craft map.
- `village-ren-phu-my.html` is a useful richness reference for household storytelling.
- Neither file should be treated as a final structural contract by default.

## Phase 3: Define the Thin Advanced MVP
### Objective
Keep `advanced` in scope as a real section, but trim it to the smallest launchable data-backed experience.

### Advanced MVP interaction contract
The first live `advanced` section should support:
- layer browsing
- map canvas exploration
- place inspection
- filtering
- lightweight insight cards or summaries

### What to avoid locking too early
Do not commit the MVP to:
- deep composite indices
- heavy reporting
- large recommendation systems
- complex analytic workflows

Those can be added later once the actual layer inventory is confirmed and the MVP interaction model is stable.

## Phase 4: Convert the Design into an Implementation Contract
### Recommended production architecture
- `Next.js` for app shell and routing
- `MapLibre GL JS` for map rendering
- `Postgres + PostGIS` for spatial backend

### Minimal base data model
- `Village`
- `Household`
- `Product`
- `Dataset` or `Layer`

### Required structural constraints
- bilingual content fields from the start
- support for raster, vector, and spatial table-backed data
- one shared app shell with separate `community` and `advanced` section logic
- no MVP-critical dependency on a full admin system

## Phase 5: Validate Against Real Data
### Required follow-up inputs from Mel
Before implementation hardens, gather:
- real `advanced` layer inventory
- real craft household fields
- real available craft assets:
  - coordinates
  - heritage / narrative text
  - quotes and audio clips
  - process and workshop-layout data
  - economics / succession data
  - product information
  - images
  - source / provenance material

### Validation rule
Use the real dataset inventory to trim or validate the locked design. Do not let the absence of that inventory prevent design decisions that are already stable at the product level.

## Review Sequence
1. approve the canonical `community` MVP flow
2. approve the household detail page content hierarchy
3. approve the craft map interaction model
4. trim `advanced` to the smallest real launchable slice
5. approve the implementation architecture and base data model
6. replace exploratory HTML with a canonical production-oriented prototype

## Acceptance Criteria
This plan is successful when:
- the MVP no longer depends on interpreting exploratory HTML as product truth
- `community` has a stable map flow and a stable household detail page template
- `advanced` has a stable minimum interaction model
- the app structure is decision-complete enough for implementation
- the design remains compatible with mixed geospatial input types and future expansion

## Assumptions
- `community` MVP is strictly craft households plus map and detail pages
- `household` remains the canonical public entity
- `village` remains parent context
- `advanced` is part of the MVP but should launch thin
- current HTML files may be restructured or discarded entirely
