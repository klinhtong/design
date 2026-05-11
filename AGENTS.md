# Memory Context

# [design] stable context, 2026-05-11 6:00pm GMT+7

## Mapme: working product model

Mapme is a geospatial platform intended to become a single source of truth for the Mekong Delta and, over time, broader Vietnam. It is not just map software. It is meant to function as:
- a geospatial exploration tool
- a curated data repository
- a platform for community-linked knowledge and stories

The working role context for Codex in this repo is:
- cofounder
- chief data scientist / architect
- design feasibility partner

## Repo status

This repo contains exploratory HTML prototypes and design briefs, not canonical product truth. Existing files are useful design probes and references, but all HTML can change. The purpose of current work is to help lock down the MVP design while keeping it technically feasible.

Do not assume current page flows or components are final just because they exist in HTML.

## App structure

Mapme should be treated as one app with two sections:

1. Advanced
2. Community

These are separate product surfaces with separate data models, but they live inside one shared app shell and design system.

## MVP promises

### Community
Browse a curated map of craft households in Vietnam and open rich household pages with story, products, and context.

### Advanced
Explore layered Mekong geospatial data, inspect places, and extract lightweight spatial insights through filtering and comparison.

## Community MVP: locked understanding

Community MVP is intentionally narrow for now:
- craft households
- functional map
- household detail pages

Important constraints:
- `household` is the canonical public entity
- `village` is parent context
- one village has many households
- each household has one detail page
- each household detail page can showcase multiple products

For MVP, the detail page design is a top priority artifact to lock down.

### Updated household-page mental model

The household detail page is a **storefront** and eventual claimable household presence, not just a passive profile.

The page must let a visitor do something:
- message the household through mapme
- discuss collaboration or commissioning where appropriate
- request a visit or learning pathway where appropriate

The household page is not a direct-ordering surface. No cart, checkout, or instant-buy flow should be assumed in design or implementation planning.

Actions are threaded throughout the page, not isolated in one footer CTA.

### Updated household-page content understanding from Trip 1 references

The first field trip appears to have richer household-level material than earlier mockups implied. Design should assume the household page may have:
- artisan identity and signature quotes
- emotional heritage narrative
- process steps
- workshop spatial layout / zones
- materials and supply-chain context
- economics and market viability
- succession / future-of-craft signal
- products
- connections to other households across multiple axes
- audio clips / interview excerpts

Real Trip 1 media exists in the field-trip archive but is not currently present in this repo. Public-facing page design should assume real media is part of the intended launch quality, even if repo prototypes still need graceful fallbacks during design.

### Upstream journey note

Before a visitor reaches a household detail page, they are on the craft households map. That upstream surface must:
- orient the visitor geographically
- help them filter and compare households
- provide enough preview context to justify opening one household

The craft map should therefore surface, at minimum, for each household preview:
- artisan name
- craft type
- village / province context
- succession signal
- one-line emotional or practical hook
- detail-page entry CTA

### Household-page structural note

Do not treat an embedded map as a primary requirement of the household detail page itself. The village or upstream craft-map experience handles map navigation; the household page is a deep profile / storefront / story surface.

Community is broader long-term, but that is not the immediate MVP scope. Long-term exploratory/community concepts seen in the repo include:
- field stories
- projects
- trips
- submissions / community contributions

Those should be treated as future-adjacent or supporting concepts unless explicitly pulled into MVP scope.

## Advanced: locked understanding

Advanced is the Mekong geospatial intelligence surface.

It should support, at minimum:
- place inspection
- layer exploration
- filtering
- comparison
- lightweight insight extraction

It should be designed to support mixed geospatial source types over time, not only current available files.

Known raw data modalities expected:
- `.tif` rasters
- `GeoJSON`
- tabular spatial data with coordinates or polygon columns

The exact available layer inventory is still pending from the user and must be requested later before implementation constraints harden.

## Design direction

Stable design assumptions:
- design-led, high-resolution UI
- technically feasible, not pure concept art
- bilingual VN / EN
- desktop-first
- performance-conscious

The main objective of this repo in the near term is:
- lock down the design in a way that matches the data Mapme has or can realistically support

## Prototype file interpretation

Treat these as references only:
- `mapme-app.html`: landing page / mode selection reference
- `mapme-prototype.html`: current community/craft map reference
- `reference/household-detail-brief-v2.md`: current strongest household-page product brief
- `reference/claude-design-instruction-v2.md`: strongest implementation-oriented household-page reference

They are not fixed requirements, but the v2 household references supersede the earlier household-page assumptions where they conflict.

## Recommended MVP interaction priorities

Priority user actions for early design and implementation:
1. search place or record
2. switch layers or datasets
3. inspect feature details
4. filter records
5. move between map, list, and detail/story views

Priority household-page actions:
1. message
2. collaborate / commission when appropriate
3. visit / learn when appropriate

Lower priority for first MVP design pass:
- uploads
- downloads
- NLQ
- drawing areas
- full transaction flows

## Current open follow-ups to ask the user later

1. Real available `advanced` datasets / layer list
2. Real craft household fields and assets, especially which Trip 1 media files are ready to use in-repo
3. Which exploratory community surfaces beyond craft households should graduate into later scope

Until those arrive, optimize for product clarity and design feasibility rather than overfitting to current mock data.


<claude-mem-context>
# Memory Context

# [design] recent context, 2026-05-11 5:27pm GMT+7

Legend: 🎯session 🔴bugfix 🟣feature 🔄refactor ✅change 🔵discovery ⚖️decision
Format: ID TIME TYPE TITLE
Fetch details: get_observations([IDs]) | Search: mem-search skill

Stats: 23 obs (9,746t read) | 313,307t work | 97% savings

### May 11, 2026
621 3:24p 🔵 Mapme Platform — Mission, Scope, and Role Defined
622 3:25p 🔵 mapme/design Repo — Nearly Empty, Only AGENTS.md Present
623 3:41p ⚖️ mapme — Craft Villages MVP Scoping Decisions Captured
625 3:53p 🔵 mapme/design Repo — Full File Inventory and Prototype Architecture Confirmed
627 3:59p ⚖️ mapme Architecture Scoping — Craft Villages MVP Answers
630 5:07p ⚖️ mapme MVP Design Lock Plan Created — PLAN.md
632 5:10p 🔵 mapme/design Repo — Reference Folder Contents Confirmed
633 " 🔵 mapme Household Detail Page — v2 Design Brief Full Spec Confirmed
634 " 🔵 mapme Claude Design Instruction v2 — Two-Household Prototype Build Spec Confirmed
635 5:12p 🔵 mapme Reference HTML Prototypes — Full Implementation Confirmed, Not Just CSS Samples
636 " 🔴 AGENTS.md Was Empty — Deleted
641 5:13p ✅ PLAN.md Phase 2 Updated — Storefront Model + Expanded Content Contract
642 " 🔵 mapme/design Git Repo — All Files Untracked, No Commits Yet
643 5:19p ⚖️ mapme Household Page CTA — Connect Not Commerce
644 " ⚖️ mapme Journey — Map Page (mapme-prototype.html) → Household Detail Page
647 5:20p 🔵 mapme Reference Docs Current State — Action Triad + CTA Model Pre-Edit
649 " 🔴 household-detail-brief-v2.md Patch — Partial Apply, Action Layer Table Mismatch
653 5:21p ✅ household-detail-brief-v2.md — CTA Model + Map Journey Section Updated
655 5:22p ✅ claude-design-instruction-v2.md — CTA Framing + Upstream Journey Constraint Added
658 " ✅ claude-design-instruction-v2.md — Per-Household Specifics + Action Forms Updated
659 " 🔵 AGENTS.md in mapme/design Was Empty — Deleted Again
663 5:23p ✅ PLAN.md — No-Ordering Policy + Upstream Craft-Map Contract Added
664 5:25p ✅ household-detail-brief-v2.md — Final "Đặt hàng" Sweep Complete, All Appendix Samples Updated

Access 313k tokens of past work via get_observations([IDs]) or mem-search skill.
</claude-mem-context>