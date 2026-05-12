# Instruction to Claude Design — Household Detail Prototype v2

**From:** Mapme Data Team
**Date:** 2026-05-10
**You will produce:** two standalone HTML prototype files, one per household.
**Brief:** `prototypes/household-detail-brief-v2.md` (read this in full before starting)
**Reference prototype:** `prototypes/village-ren-phu-my.html` (inherit design system; do not diverge)

---

## Context You Need

Mapme is a Mekong Delta craft village documentation platform. The "Root layer" — cultural heritage and craft documentation across 13 provinces. This is the **household detail page** — a single artisan's storefront. Visitors arrive from a village map and leave able to connect with the household through mapme, request a visit, discuss collaboration or commissioning, or express interest in learning/supporting the craft. Eventually, households claim and edit their own page.

The brief you are building from (`household-detail-brief-v2.md`) is itself a v2 — a council of advisors reviewed v1 and the brief was rewritten in response. Read the section "What Changed in v2" first. The shifts that matter most for your work:

1. **Storefront, not detail page.** Actions threaded through every section. Hero carries an action triad centered on connection, not checkout. Sticky mobile action bar.
2. **Real media gallery.** No five gradient placeholder cards. A 12-column varied grid with photos, audio clips, video — captioned editorially. Placeholders only as a transitional state.
3. **AI provenance badges removed.** No `✦ Tạo bởi heritage-analyst` per section. Single methodology disclosure in the footer.
4. **CONNECTIONS replaces Related Households.** Four lenses: same trip · same craft · same region · same theme. Default lens = same theme. Each card carries a one-line editorial rationale.
5. **Defensive sections cut.** No "What This Page Is NOT". No standalone DATA PROVENANCE section.

---

## Deliverables

Two files, in `prototypes/`:

| File | Household | Accent | Succession |
|------|-----------|--------|------------|
| `household-le-thi-huych.html` | Lê Thị Huých — basket weaving (đan lát), Củ Chi | `#8fad5a` bamboo green | Code 3 — Thế hệ cuối |
| `household-huynh-xuan-huynh.html` | Huỳnh Xuân Huỳnh — Nắng Ceramics, Lái Thiêu | `#c4623a` terracotta | Code 1 — Đang truyền nghề |

Both pages use the **same** HTML structure, CSS variables, and component vocabulary. Per-household differences are achieved by setting `--accent` and swapping content. A reader who scrolls both pages should feel the design system is one system, not two designs.

These two were chosen deliberately:
- **Lê Thị Huých** is the platform's most emotionally consequential page — code 3, last-generation, dramatic arc, richest data. It tests whether the design holds the weight of "this craft is ending."
- **Huỳnh Xuân Huỳnh** is the contrasting case — code 1, growing, the youngest artisan in the corpus, an apprentice pathway active. It tests whether the design works when the news is good.

If the design serves both, it serves the four households between them.

---

## Sequencing

Do **not** build both pages in parallel from a blank slate. Build in this order:

1. Build `household-le-thi-huych.html` first. This is the reference page. Get every section right here.
2. Once that page is review-ready, fork it into `household-huynh-xuan-huynh.html` and adapt: swap `--accent`, swap content, swap succession state, swap CONNECTIONS cards, swap action triad rules where the economic / succession profile differs.
3. Verify the two pages share an HTML skeleton — diff them, and the diff should be content + accent, not structure.

## Upstream Journey Constraint

Be mindful that this page is never the first craft-household touchpoint. Before clicking into it, the visitor is on `mapme-prototype.html` or its eventual replacement.

That upstream craft-map surface must do three things before the detail page opens:
1. orient the visitor geographically
2. help them filter and compare households
3. give enough household preview to justify the click

Design the household page assuming the map already supplied:
- artisan name
- craft type
- village / province
- succession signal
- one-line hook

Do not waste the household page hero re-solving map orientation that should already be handled upstream.

---

## Section Checklist (11 sections + footer)

Build in the order specified by the brief. For each section, the brief specifies layout, content, and behavior. Do not reorder.

- [ ] **HERO** — full-bleed, 80vh, gradient (no real hero photo yet), succession badge top-right (hoverable, one-line tooltip), connection-oriented action triad, h1 with `<br>` between name and tagline, meta strip
- [ ] **QUICK FACTS STRIP** — 6-col grid, em-dash for null fields
- [ ] **THE ARTISAN** — two-col card, signature quote with inline play button (use a stub `<audio>` element with no `src`; render the play button regardless), source line, action row
- [ ] **MEDIA GALLERY** — 12-col responsive grid, varied spans, six items per the sample curation in the brief. Real photos do not exist in repo — use `<img>` with placeholder hrefs and an inline data-uri craft-gradient as `background-image` fallback. Treat each item as if real media were on the way: real captions, real alt text, real spans. Audio cards render with a waveform stand-in (CSS-only horizontal stripes are acceptable). Video cards render with a play overlay.
- [ ] **THE STORY** — 680px max width, drop cap on lead, Vietnamese-first, dual blockquote with English translation subline, level-2 toggle ("Xem nguồn gốc") that expands an inline panel showing one or two stub verbatim quotes per paragraph (mark them as placeholder copy clearly — `[Trích đoạn nguồn — sẽ liên kết với transcript]`)
- [ ] **3D HOUSEHOLD LAYOUT** — full-bleed dark section. 3D model files not yet available — use the SVG zone-diagram fallback per the brief. Right sidebar: zone legend + headline stat. Hover state on zones surfaces tooltip with quote.
- [ ] **CRAFT PROCESS** — 3-col grid of step cards, accent number, step name, 25-word description, top-right thumbnail (gradient placeholder for now), time badge top-right of section
- [ ] **MATERIALS & SUPPLY CHAIN** — two-col. Left: vertical material flow with origin-node color coded by supply stability. Right: risk panel + environmental dependencies + waste profile + **upstream/downstream household links** subsection (per brief)
- [ ] **ECONOMIC PORTRAIT** — sentiment word (large Fraunces, color-coded), business model snapshot, tension-forces 2-col, **engage row** at bottom (button selection per economic profile)
- [ ] **SUCCESSION & FUTURE** — 640px max, large Fraunces typographic treatment, faint radial-gradient wash keyed to succession color at 8% opacity, succession quote, subtext, **CTA** (varies by code)
- [ ] **CONNECTIONS** — tab/chip-filtered lens selector (Cùng chuyến đi · Cùng nghề · Cùng vùng · Cùng câu chuyện), default = Cùng câu chuyện, 1–3 cards per lens, each with editorial rationale. Hide a lens if it has zero matches.
- [ ] **Footer** — three-col: methodology disclosure · data gaps list · actions row (Báo lỗi, Tải dữ liệu, Trích dẫn). Citation block collapsed by default.

Plus two cross-cutting elements:
- [ ] **Sticky in-page nav** that appears once hero scrolls out of view. 8 anchors per the brief.
- [ ] **Sticky mobile action bar** below 780px once hero scrolls out of view. Single primary action (Message).

---

## Content Source Rules

The brief contains **fully populated sample content** for both households in the Appendix (`SAMPLE A` and `SAMPLE B`). Use that content **verbatim**. Do not paraphrase. Do not translate Vietnamese. Do not edit the artisan quotes. Do not invent new sentences.

If a section is described in the brief but the appendix does not give you that exact slot for one of the two households, look up the data in:

- `trips/2026-04-01/outputs/basket_weaving/` for Lê Thị Huých — `heritage.md`, `economics.md`, `environment.md`, `schema.json`
- `trips/2026-04-01/outputs/nangs_ceramics/` for Huỳnh Xuân Huỳnh — same four files

Cross-household connections (the CONNECTIONS section) draw from `trips/2026-04-01/outputs/cross/comparator.md` and `synthesis.md` — those documents contain the editorial connective tissue.

If a piece of content is genuinely missing from all sources, **render the empty-state treatment from the brief's "Handling Data Variance" table**. Do not fabricate. Do not show a "TODO" string.

---

## Design System Rules (Non-Negotiable)

- Inherit CSS variables, fonts, type scale, and component vocabulary from `village-ren-phu-my.html` exactly. Do not introduce new colors outside `--accent` per craft.
- Per-household color identity is set by overriding `--accent` on `<body>` (or a top-level wrapper). One variable change must propagate everywhere.
- Fraunces for serif (headings, quotes, story prose). Manrope for sans (UI, metadata, buttons). No third font family.
- Vietnamese text always typographically primary; English secondary, muted, smaller. Never replace.
- Dark theme only. `--bg: #17130e` baseline. No light-mode toggle.

---

## Media Handling for This Build

Real Trip 1 photographs exist in mapme's field-trip archive but are **not in this repo**. For this prototype:

- The HERO uses the craft-gradient background. No `<img>` in the hero.
- The MEDIA GALLERY renders six items per the brief's sample curation. For each:
  - Photographs: `<img src="placeholder/{slug}.jpg" alt="{Vietnamese alt text}">` — the `src` will 404, that is fine. The CSS must show a craft-gradient `background-image` as a fallback, with a small `Ảnh sẽ được liên kết` corner chip in muted text.
  - Audio: a CSS-only waveform stand-in (a row of vertical bars varying in height) + a play button + the editorial caption.
  - Video: a `background-image` gradient + a centered play-button overlay + duration badge.
- The Artisan signature-quote audio button is a stub `<button>` with `aria-label` set; clicking does nothing. Style it as if active.
- Process step thumbnails: 56×56px gradient placeholder with a small icon — same icon family across all six steps.

When the real assets land, dropping them into the marked slots should require no structural change. Build with this swap in mind.

---

## Action Forms Behavior

Action buttons should support connection, not checkout. No direct ordering flow belongs on this page.

Action buttons (Message, Collaborate/Commission, Visit/Learn, etc.) open a modal containing a 3–5 field stub form:
- Tên (name)
- Email
- Loại liên hệ (radio — auto-selected based on which button was tapped)
- Lời nhắn (textarea)

Form submit does nothing functional — render a confirmation toast: *"Cảm ơn bạn. Mapme sẽ chuyển lời nhắn tới nghệ nhân và phản hồi trong vòng 3 ngày."* Then close the modal.

Backend wiring is not your concern; surface a clean form so the team can swap in the real endpoint later.

---

## Per-Household Specifics

### Lê Thị Huých (`household-le-thi-huych.html`)

- `--accent: #8fad5a`
- Succession badge: `#9a3a3a` red, label "Thế hệ cuối", tooltip "Last-generation artisan — no successor."
- Action triad: **Nhắn tin** · **Hợp tác / đặt làm** · **Học nghề**
- ECONOMIC PORTRAIT engage row: **Hỏi về đặt làm / hợp tác** · **Hợp tác xuất khẩu**
- SUCCESSION CTA: **Bạn muốn học nghề đan lát truyền thống? Liên hệ qua mapme →**
- Sentiment word: **Bấp bênh** (amber)
- Hero gradient: `linear-gradient(135deg, #1a2010 0%, #2d3d18 30%, #4a6124 60%, #6b8a3a 100%)`
- Connections default lens cards: see Sample A in brief
- MATERIALS upstream/downstream link: → Mành tre — Bình Dương

### Huỳnh Xuân Huỳnh (`household-huynh-xuan-huynh.html`)

- `--accent: #c4623a`
- Succession badge: `#6b9a3a` green, label "Đang truyền nghề", tooltip "Apprentices in training — passing the craft on."
- Action triad: **Nhắn tin** · **Hợp tác / đặt làm** · **Tham quan / thực tập**
- ECONOMIC PORTRAIT engage row: **Hỏi về đặt làm** · **Hợp tác xưởng / thực tập**
- SUCCESSION CTA: **Đăng ký thực tập tại Nắng Ceramics →**
- Sentiment word: **Bền vững** (green — sustainable, not rich)
- Hero gradient: `linear-gradient(135deg, #2a1208 0%, #4a2010 30%, #7a3518 60%, #c05028 90%)`
- 7-step process (vs 6 for basket weaving) — verify the grid handles 7 cleanly (3-col → 3-3-1)
- 3D zone diagram has 7 zones (A–G), one more than basket weaving — sidebar legend must accommodate
- Connections default lens cards: see Sample B in brief
- MATERIALS upstream/downstream link: → Gốm Tư Thố — Huê Anh

---

## What to Skip

- **Real photographs.** Use the placeholder treatment described above.
- **Real 3D models.** Use the SVG zone-diagram fallback only.
- **GPS / map integration.** No map in the household page. The village page upstream handles location at the village level.
- **Action form backend.** Stub it.
- **Authentication, household-claim flow.** Out of scope for v2 prototype.
- **Per-section AI provenance badges.** Removed in v2. Do not add them back.
- **Standalone DATA PROVENANCE section.** Removed. Footer disclosure only.
- **"What This Page Is NOT" section.** Removed.

---

## Success Criteria

You are done when:

1. Both HTML files load standalone — no build step, no external deps beyond fonts (Google Fonts is acceptable for Fraunces + Manrope).
2. The two pages diff cleanly: identical structure, content + `--accent` + succession variations.
3. Every section in the 11-section architecture renders with real sample content from the brief.
4. The succession badge tooltip works on hover and tap.
5. The CONNECTIONS lens selector switches between four tabs without page reload; lenses with zero matches are hidden.
6. The sticky in-page nav engages on scroll past the hero.
7. The mobile sticky action bar engages below 780px.
8. The action modal opens, accepts input, and shows a confirmation toast on submit (no real backend).
9. The page passes the **Helly Lens behavioral check**: when you scroll the Lê Thị Huých page past SUCCESSION, you should *want* to tap the CTA. If you don't, the section is not yet doing its job.
10. The page passes a **respect check**: read it as if you were Lê Thị Huých's granddaughter. Nothing should make her wince.

---

## One Last Thing

The brief's closing line is the standard:

> Read it as if you were the artisan's granddaughter. Nothing should make her wince.

That is the test. Apply it to every section before you call the page done.
