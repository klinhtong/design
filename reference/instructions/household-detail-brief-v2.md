# Craft Household Detail Page — Design Brief v2
**For:** Claude Design
**From:** Mapme Data Team
**Date:** 2026-05-10
**Reference prototype:** `village-ren-phu-my.html`
**Supersedes:** `household-detail-brief.md` (v1)

---

## What Changed in v2

This brief is a response to a council review of v1. The bones of v1 were sound — what was missing was the soul. v2 keeps the structure (sections, design system, accent colors, dual-language, progressive disclosure) and rebuilds three things that were quietly broken:

1. **Mental model: storefront, not detail page.** This page is the household's online presence — eventually claimable by the household themselves. Visitors arrive to *do* something: connect, commission, visit, learn, support. v1 designed for comprehension and stopped. v2 designs for action threaded through every section.
2. **Media: real, curated, mixed.** v1 specified five gradient placeholders. v2 specifies a real media gallery — photographs from the field, audio clips from the interview, short video where it exists. Placeholders are a transitional state, not a launch state.
3. **Connections: multi-axis network, not a related-cards stub.** v1's "Related Households" was a 3-card afterthought. v2 makes Connections the platform's connective tissue: same trip, same craft, same region, same narrative theme. Households become nodes in an advocacy atlas.

Cut from v1: per-section AI-provenance badges, the standalone DATA PROVENANCE section, and the "What This Page Is NOT" defensive section. AI was a tool to produce the content, not a co-author the page needs to credit per paragraph. A single methodology disclosure in the footer is enough.

---

## What This Page Is

The **storefront** for one craft household. One artisan, their craft, their workshop, their economics, their succession story — and their open door.

The artisan is the protagonist. The craft is the context. The economics and ecology are the tension. The actions a visitor can take are the point.

This page sits one level deeper than the village map. A user arrives from tapping a dot on the map or a household card. They leave knowing a person — and able to connect with them through mapme, request a visit, discuss collaboration or commissioning, or express interest in learning/supporting the craft.

**Audiences served simultaneously:**
- **The household itself** — this is their page. Eventually, theirs to claim and edit. It must feel like *their* presence, not a profile written about them.
- **Heritage funders / NGOs** — they need to feel the weight and find a way to support.
- **Researchers / officials** — they need to verify, cite, and understand the structural pattern.
- **Buyers, designers, brands** — they need to see provenance and reach out to commission.
- **Travelers, apprentices, the curious** — they need to find a way in: visit, learn, listen.

### Upstream journey: craft map to household page

Before a visitor opens this page, they are on the craft households map. That upstream surface has a distinct job:
- orient the visitor geographically
- help them filter and compare households
- help them decide which household is worth opening

The craft map should therefore surface, at minimum, for each household preview:
- artisan name
- craft type
- village / province context
- succession signal
- one-line emotional or practical hook
- detail-page entry CTA

The household detail page should assume that basic geographic orientation has already happened upstream. It should not spend its highest-value real estate re-explaining the map.

---

## Design System (from prototype)

Inherit everything from `village-ren-phu-my.html`. Do not diverge.

```css
--bg: #17130e          /* near-black warm */
--bg-2: #1e1913        /* card backgrounds */
--bg-3: #26201a        /* nested cards */
--paper: #f5ecde       /* primary text */
--paper-dim: #d8cfbe   /* body text */
--paper-mute: #9a9081  /* labels, metadata */
--ink: #1a1410         /* dark on light */
--border: rgba(245,236,222,.1)
--border-strong: rgba(245,236,222,.22)
```

**Fonts:** Fraunces (serif) for headings, quotes, story prose. Manrope for UI labels, metadata, buttons.

**Accent color is per craft type** — not a single global accent. Each household has its own color identity:

| Craft | Accent | Rationale |
|-------|--------|-----------|
| Basket weaving (đan lát) | `#8fad5a` warm bamboo green | Split bamboo, dried in sun |
| Bamboo curtain (mành tre) | `#c4924a` amber | Lacquered bamboo |
| Nắng Ceramics (gốm) | `#c4623a` terracotta | Lái Thiêu clay, wood-fired |
| Adjacent Ceramics (gốm) | `#9e5030` deep clay rust | Older tradition, more subdued |
| Incense (nhang) | `#a0607e` rose smoke | Incense smoke, ritual color |

CSS override per household: `--accent: {craft-color}`. Every accent-colored element adapts automatically.

---

## Page Architecture

Scroll-based single page. 11 sections in order:

```
1.  HERO                  — Identity + succession signal + primary actions
2.  QUICK FACTS STRIP     — 6 scannable data points
3.  THE ARTISAN           — Person card + signature quote (audio-playable)
4.  MEDIA GALLERY         — Real photos, audio, video
5.  THE STORY             — Heritage narrative (prose)
6.  3D HOUSEHOLD LAYOUT   — Spatial portrait of the workshop
7.  CRAFT PROCESS         — Step-by-step
8.  MATERIALS & SUPPLY    — Where things come from + supply-chain links to other households
9.  ECONOMIC PORTRAIT     — Viability, income, markets
10. SUCCESSION & FUTURE   — Future of the craft + apprenticeship pathway
11. CONNECTIONS           — Multi-axis links to other households
```

**Footer (not a numbered section):** A single methodology disclosure (how content was produced, schema version, data freshness, citation block, "report a correction" link).

**Actions are threaded through the page**, not concentrated in one section:
- HERO carries the **primary action triad**: Message · Collaborate · Visit
- THE ARTISAN card surfaces a **direct message** affordance
- ECONOMIC PORTRAIT surfaces **commission / partnership** if relevant
- SUCCESSION surfaces **apprenticeship / learn this craft** if data warrants
- A **sticky action bar** appears on mobile once the hero scrolls out of view
- The footer always carries **Message · Visit · Tải dữ liệu · Báo lỗi**

---

## Section Specs

---

### 1. HERO

**Emotional intent:** You are entering someone's workshop, not opening a database entry. The first thing you feel is the person. The second thing you feel is the urgency — is this craft passing on, or passing away?

**Layout:** Full-bleed, min-height 80vh. Content aligned bottom-left. Background: a craft-specific gradient when no hero photograph exists; a real photograph (with gradient overlay for legibility) when one does.

**Background gradients per craft (fallback when no hero photo yet):**
- Basket weaving: `linear-gradient(135deg, #1a2010 0%, #2d3d18 30%, #4a6124 60%, #6b8a3a 100%)`
- Nắng Ceramics: `linear-gradient(135deg, #2a1208 0%, #4a2010 30%, #7a3518 60%, #c05028 90%)`
- Incense: `linear-gradient(135deg, #1a0f18 0%, #2e1428 40%, #5a2848 70%, #8a4060 100%)`

**Content layout:**

```
[Top-left]    [Pill: craft type in Vietnamese]   [Province · Region]
[Top-right]   [Succession state badge]

[h1 — Fraunces italic, 56–72px responsive]
Lê Thị Huých
"Phải làm cho liền. Làm cho đẹp."

[Dek — Fraunces light, 20px, max 40 words]
2–3 sentence emotional hook from heritage narrative. The why this person matters.

[Action triad — Manrope buttons, accent-bordered]
[ Nhắn tin ]   [ Hợp tác / đặt làm ]   [ Tham quan / học nghề ]

[Meta strip — bottom, above border]
Năm sinh  |  Kinh nghiệm  |  Vật liệu chính  |  Trạng thái
1954       |  70+ năm      |  Tre trúc         |  Đang hoạt động
```

**Succession state badge** (top-right corner of hero). Subtle pill — the page's first emotional signal:

| Code | Color | Vietnamese label | English subtitle on hover |
|------|-------|------------------|---------------------------|
| 1 — Passing on | `#6b9a3a` green | Đang truyền nghề | Apprentices in training |
| 2 — Desired but rejected | `#c49a30` amber | Chưa có người kế | No successor yet |
| 3 — Resigned / last | `#9a3a3a` muted red | Thế hệ cuối | Last generation |
| Unknown | `#5a544a` muted gray | Chưa rõ | Status unconfirmed |

The badge is hoverable / tappable. The tooltip explains what the code means in one sentence — solving the "curse of knowledge" problem from the council review. A first-time visitor must not have to decode it.

**Action triad selection rules:**
- Always show *Message*. Always.
- Show *Collaborate / commission* when economics indicate the household can realistically take custom work, institutional partnerships, design collaboration, or made-to-order inquiries. This is a relationship CTA, not a cart or direct-buy CTA.
- Show *Visit / learn craft* when succession code is 1 (apprentice pathway) or 3 (last-generation urgency). Hide for code 2 unless economics indicate workshop tourism or hosted visits.
- If only *Message* is appropriate, render it alone, larger. Never pad with greyed-out buttons.

**h1 structure:** Always `<br>` between artisan name and tagline:
```html
<h1 class="title">Lê Thị Huých<br><em>"Phải làm cho liền. Làm cho đẹp."</em></h1>
```

---

### 2. QUICK FACTS STRIP

**Layout:** 6-column grid, full-width, max 880px centered. Same as prototype.

**Fields (from schema.json):**

| Label | Field | Example |
|-------|-------|---------|
| Tỉnh/TP | province | TP. Hồ Chí Minh |
| Nghề | craft type (VI) | Đan lát |
| Sinh năm | artisan_year_of_birth | 1954 |
| Kinh nghiệm | artisan_years_of_experience | 70+ năm |
| Xưởng | workshop_size_sqm | 4.000 m² |
| Kế nghiệp | succession_intent_code (text) | Chưa có |

If a field is null, show `—` (em dash) in muted style. Never hide the cell. Never substitute zero.

---

### 3. THE ARTISAN

**Emotional intent:** This is a person, not a profile. If audio of their voice exists, the visitor should be able to hear it here.

**Layout:** Two-column card (`.artisan-card` from prototype). Left: portrait (photo where available, accent-gradient placeholder otherwise). Right: name, role, signature quote, listen button, action row.

**Portrait treatment:**
- **With photograph:** Crop to 3:4. Subtle accent-color border. Caption underneath: name + date taken.
- **Without:** Craft-specific gradient. No icon, no silhouette — the gradient *is* the portrait. Small corner label: `Ảnh: chuyến thực địa tiếp theo`.

**Content structure:**

```
[Pill: Nghệ nhân]

[h2 — Fraunces 28px]
Lê Thị Huých

[Subhead — Manrope 13px muted]
Đan lát · 70 năm kinh nghiệm · sinh 1954

[Signature quote — Fraunces italic 20px, with inline play button if audio]
" Phải làm cho liền. Làm cho đẹp. "
[ ▶ Nghe nghệ nhân nói ]   ← only when audio clip exists

[Source line — Manrope 12px muted]
Ghi âm ngày 01/04/2026 · Phiên A004 · Phiên dịch: mapme

[Actions row]
[Primary: Nhắn tin nghệ nhân]   [Secondary: Tải dữ liệu]
```

**Listen-to-quote behavior:** When an audio clip of the signature quote exists, the play button is inline with the quote. Tapping plays the verbatim Vietnamese audio in-page (no overlay). 30–60 seconds max. This is the highest-value piece of media on the page after the portrait — a real artisan voice does what no AI-generated prose can.

---

### 4. MEDIA GALLERY

**Emotional intent:** This is what the visitor came to see. Show the place, the hands, the work, the voice. The right mix of media — not five identical placeholder cards.

**Layout:** Full-width section, `bg-2` background. Curated gallery with deliberate variety, not a flat strip. Default desktop layout: a 12-column grid where individual items take varying spans (a hero photograph spans 8, a square detail spans 4, an audio clip spans 6, a video spans 6). Mobile: single-column scroll.

**Required mix per household (target — final selection is editorial):**
- **1 hero photograph** — workshop or artisan-in-context, wide format
- **2–3 supporting photographs** — portrait, product detail, hands-at-work
- **1–2 audio clips** — signature quote (already linked from THE ARTISAN), and ideally one ambient or process clip
- **1 short video** (optional, encouraged) — 30–90 seconds, raw and honest, not produced-feeling

**Per-item treatment:**

| Type | Aspect | Caption | Affordance |
|------|--------|---------|------------|
| Photograph | varies (3:4, 16:9, 1:1) | Subject + date + photographer | Click → lightbox |
| Audio clip | 16:9 visual card with waveform | What you'll hear (1 line) | ▶ inline play |
| Video | 16:9 | Subject + duration | ▶ click-to-play, no autoplay |

**Captions are editorial, not metadata.** Not "Photo of Lê Thị Huých." Yes "Lê Thị Huých at the cement-coating station — the one zone where she still works alone." Captions are a chance for the page to teach.

**Alt text is mandatory** for every image. Vietnamese first, English secondary. Both must describe — not label.

**When media is incomplete:** Reserve the slots in the grid but do not render gradient placeholders. Instead, render a single editorial line in muted text in the place where the missing media would go: *"Video về quy trình tráng xi măng đang được biên tập."* This communicates a commitment with a date, not an absence.

**The default state of this page should not be "no real media."** The brief assumes Trip 1 photographs are in the system. If they are not, this section ships internal-only until they are — the page does not launch publicly with placeholders.

---

### 5. THE STORY

**Emotional intent:** The reader should feel the weight of what this person has built and what might be lost.

**Layout:** Full-width prose article, max 680px, centered. `article.story` from prototype. Drop cap on first paragraph.

**Content structure:**

```
[h2 — Fraunces 40px]
Section title — derived from heritage narrative.
e.g. "Bốn thế hệ, một đôi tay"

[Lead paragraph — Fraunces 22px, drop cap]
The craft origin story. Where it began, how long it has been in the family.
Source: heritage.md → Craft Origin Story.
Hard cap: 60 words.

[Body paragraphs — Fraunces 18.5px, max 3]
The artisan's life in the craft:
  · Years started, how learned (from father / mother / self-taught)
  · The peak years (export volume, recognition, milestones)
  · The turn — when things changed (market shift, urbanization, policy)
  · How they feel about continuing now

[Blockquote — Fraunces italic 28px centered]
The memorable memory.
Source: artisan_memorable_memory_source_quote (Vietnamese verbatim)
With translated subtitle in Manrope 13px.

[h3 — Fraunces 22px]
"Tinh hoa nghề" — what only an expert can do

[Body — 1 paragraph]
The mark of mastery.
Source: heritage.md → "The Artisan's Soul".
```

**Vietnamese first, English second** — always. Vietnamese in the typography hierarchy, English in muted Manrope below. Never replace Vietnamese with translation. Both languages live together.

**Beyond level 1:** A "Xem nguồn gốc" toggle expands inline to reveal verbatim Vietnamese source quotes from the transcript that produced each paragraph. Researchers and officials need to see the source, not just the summary. This is the level-2 progressive disclosure — kept intentional, kept lightweight.

---

### 6. 3D HOUSEHOLD LAYOUT

**Emotional intent:** The reader understands the physical world this artisan inhabits — scale, flow, which zones matter, how space and craft are inseparable.

**State this design must support:**
- **Default (current state):** Embedded interactive 3D model — Spline or Three.js. The model shows the household plot from above at a slight isometric angle, schematic but warm, not photorealistic. Same palette as the page: dark ground, accent-colored zone highlights, paper-white labels.
- **Fallback (when 3D not yet built):** Labeled SVG zone diagram in the same visual style. Dashed outlines for zones, Manrope labels, dimension badges. Always available from `tech_specs_notes`. Section never hides.

**Layout:** Full-bleed section, dark `bg-2`. Model/diagram occupies 70% of width. Right sidebar: zone legend + headline stat (e.g. "~4.000 m² · Củ Chi, TP.HCM").

**Interaction (3D state):**
- Hover or tap a zone → tooltip slides in: zone name + what happens there + one artisan quote about the zone
- Camera starts at overview; user can orbit
- Zone highlight uses `--accent` color on hover

**Zone data per craft** (inferred from `tech_specs_notes` + economics):

*Basket weaving — Lê Thị Huých (4,000 m²):*
```
Zone A  Kho nguyên liệu & phơi trúc    Large outdoor area, sun-critical
Zone B  Xưởng chẻ nan (máy)            Covered shed, splitting machines
Zone C  Khu đan (phân tán)             Distributed to neighbor homes
Zone D  Phòng tráng xi măng            Enclosed, mastery zone
Zone E  Kho thành phẩm & bãi container Loading dock for export
```

*Nắng Ceramics — Huỳnh Xuân Huỳnh (4,000 m² main + 100 m² annex):*
```
Zone A  Xưởng xử lý đất                Clay prep, grinding machines
Zone B  Phòng tạo hình                  Throwing wheels, molds, forming
Zone C  Khu phơi sản phẩm              Open drying racks, sun-dependent
Zone D  Phòng tráng men & vẽ          Glazing + vẽ thảo painting
Zone E  Lò nung củi (vỏ cao su)        Kiln — spiritual center, altar here
Zone F  Lò điện thử men               Small test kiln, adjacent
Zone G  Showroom & kho                 Sales counter + storage
```

**Zone tooltip template:**
```
[Zone name — Manrope 600 14px accent]
Phòng tráng xi măng

[What happens — Manrope 400 13px paper-dim]
Công đoạn hoàn thiện: tráng xi măng bên trong
để sản phẩm không thấm nước. Yêu cầu tay nghề
cao nhất trong toàn bộ quy trình.

[Artisan quote — Fraunces italic 15px]
"Khó thì bây giờ chỉ cái gia công xi măng.
Phải làm cho liền. Làm cho đẹp."
```

**Fallback diagram spec:** Zones as rounded rectangles, proportional to area, arranged spatially (not a flowchart). Each zone: accent border, zone-letter badge, name label. Compass indicator (N/S) bottom-right. No GPS coordinates needed — schematic, not a map.

If `workshop_size_sqm` is null, omit the dimension badge; show zones without scale.

---

### 7. CRAFT PROCESS

**Layout:** Dark-background section (`bg-2`), 3-column step grid (`.process` from prototype).

**Content:** Derived from `tech_specs_notes` in schema.json — split into discrete numbered steps.

**Per step card:**
```
[Number — Fraunces 42px accent color]
01

[Step name — Manrope 500 15px]
Cắt trúc

[Description — Manrope 13.5px muted, 25 words max]
Cây trúc nhập từ miền Tây được cắt thành đoạn theo kích thước sản phẩm.

[Step thumbnail — top-right of card, 56×56px]
Real photograph if available. Otherwise: small accent-bordered placeholder with craft icon.
```

**Step count varies by craft:**
- Basket weaving: ~6 steps
- Nắng Ceramics: ~7 steps
- Incense: ~5 steps

**If steps are ambiguous in data:** Show what is confirmed; add one card at the end with dashed border — "Ghi chú: Một số công đoạn chưa được ghi lại đầy đủ." Better than inventing steps.

**Time badge:** Top of section, right-aligned: "Thời gian sản xuất: 1–2 ngày / sản phẩm" — from `_schema_gaps.production_time_per_item`.

---

### 8. MATERIALS & SUPPLY CHAIN

**Emotional intent:** Making this object requires a supply chain that's quietly fracturing — and other households on this platform feel the same fracture.

**Layout:** Two-column. Left = vertical material flow. Right = supply-risk panel + **upstream / downstream household links**.

**Left — Material flow (visual):**
```
[Origin node]
Lâm Đồng / Miền Tây
(province / region pill)
↓  [distance indicator: ~300km]
[Transport node]
Thương lái thu gom
↓
[Workshop node]
Xưởng của bà Huých
Củ Chi, TP.HCM
```

Color-code the origin node by supply stability:
- Local (code 0): green — `#6b9a3a`
- Regional (code 1): amber — `#c49a30`
- Distant / at risk (code 2+): red-amber — `#c46030`

**Right — Risk panel:**
```
[Header: Rủi ro nguồn cung]
● Cao   ← from material_supply_risk

[Bullets — Manrope 13.5px, max 4]
• Tre trúc địa phương đã bị phá để làm đường
• Phải mua từ miền Tây, vận chuyển xa
• Không có nhà cung cấp ổn định tại chỗ

[Environmental dependencies]
Phụ thuộc: nắng, nhiệt độ phơi
Rủi ro: mùa mưa → mốc sản phẩm

[Waste profile — small]
Phế liệu: đốt / thu gom đô thị
```

**Upstream / downstream household links** (new in v2):

A small subsection inside the right column:
```
[Heading — Manrope 11px muted]
Hộ khác có chuỗi cung tương tự

[Link card · 1–2 max]
Mành tre — Bình Dương
Cùng phụ thuộc vào trúc nhập từ miền Tây
→
```

This is the supply-chain edge of the household network. When two households share a fragile supply line (e.g. all bamboo households depend on one corridor of imported `tre` from Lâm Đồng / the Mekong), the page makes that visible *here*, in the place a researcher or funder is already thinking about supply risk. The same link logic appears in CONNECTIONS at the bottom, but here it is contextual — the supply chain of Household A literally points to Household B because they share the chain.

If no upstream/downstream connections exist in the corpus yet, omit the subsection. Do not show a "no connections" placeholder.

---

### 9. ECONOMIC PORTRAIT

**Emotional intent:** Honest, not pitying. These people are running businesses. Show the real shape of those businesses — and where appropriate, give the visitor a way in.

**Layout:** Full-width section with dark gradient. Three components.

**A — Sentiment indicator:**
A single large typographic signal, not a chart:

```
[Label: Cảm nhận kinh tế]
[Large Fraunces word — craft-accent color]

Sentiment codes:
1 = "Ổn định"      (stable)      → cool green
2 = "Bấp bênh"     (precarious)  → amber
3 = "Căng thẳng"   (stressed)    → warm red
4 = "Tăng trưởng"  (growth)      → bright green

Below: short verbatim quote explaining the situation.
```

**B — Business model snapshot:**

| Kênh bán hàng | Lao động | Thị trường |
|---------------|----------|------------|
| Xuất khẩu qua công ty | 40+ lao động thời vụ | Đức, Đài Loan |

Data from `_schema_gaps.primary_sales_channels` + economics.md.

**C — Tension forces (forces in tension, not pros/cons):**
```
[Left: Sức mạnh]                [Right: Áp lực]
• 30 năm xuất khẩu              • Thuế cao, không nhất quán
• Thương hiệu uy tín            • Nguyên liệu ngày càng xa
• Xưởng 4.000m² tự có           • Không có người kế nghiệp
• Hợp đồng bao tiêu             • Lao động già đi
```

Source: economics.md body text — extract the key forces. 4 bullets per side max.

**D — Engage row (new in v2):**
A single inline row at the bottom of the section:

```
[ Hỏi về đặt làm / hợp tác ]   [ Hợp tác xuất khẩu ]
```

The buttons that surface depend on the economic profile:
- Active custom or wholesale relationship → "Hỏi về đặt làm / hợp tác"
- Existing exporter → "Hợp tác xuất khẩu"
- Cooperative / training operation → "Tham gia hợp tác xã"

If the household has no active commercial channel surfaced in the data, render no row. Do not invent a path.

**Sensitive data handling (unchanged from v1):** Never show specific tax amounts (VND) or specific financial losses. Show: *"gánh nặng thuế cao"*, not "26 triệu VND". Show: *"thiệt hại lớn khi thị trường thay đổi"*, not the container count × price. The detail lives in the protected transcript, not the public page.

---

### 10. SUCCESSION & FUTURE

**Emotional intent:** This section should feel like standing at a crossroads. And it should give the visitor a way to step toward it, not just look at it.

**Layout:** Full-width, centered content, max 640px. Large typographic treatment.

**Code 1 — Đang truyền nghề (Passing on):**
```
[Large Fraunces — green accent]
"Đang truyền nghề"

Subtext: who is learning, their relation to the artisan, how far along.
e.g. "Con và con rể đã cùng tham gia kinh doanh. 47 hộ hàng xóm được đào tạo."

[Soft CTA]
Bạn muốn học nghề này hoặc tham gia mạng lưới? → [ Liên hệ qua mapme ]
```

**Code 2 — Chưa có người kế (Desired but none):**
```
[Large Fraunces — amber]
"Chưa có người kế"

Subtext: why. Their feeling about it.
e.g. "Người trẻ chọn xí nghiệp vì có bảo hiểm xã hội.
       Nghệ nhân hiểu lựa chọn đó, dù không đồng ý."

[Soft CTA]
Bạn quan tâm đến việc gìn giữ nghề này? → [ Liên hệ qua mapme ]
```

**Code 3 — Thế hệ cuối (Last generation):**
```
[Large Fraunces — muted red, softer tone]
"Thế hệ cuối"

Subtext: artisan's own words.
e.g. "Con gái không theo nghề.
       Bà làm bao lâu còn sức thì làm."

[Soft CTA — emotionally weighted]
Bạn muốn học nghề này trước khi nó dừng? → [ Liên hệ qua mapme ]
```

**Background treatment:** A very faint full-width radial gradient wash keyed to succession color at 8% opacity. Subtle — not a color block. Makes the section feel like the temperature of the page shifted.

The CTA in this section is the most emotionally consequential on the page. It is the moment the visitor is most ready to do something. The button must look like a door, not a footnote.

---

### 11. CONNECTIONS

**Emotional intent:** No household exists alone. The visitor leaves understanding this household as a node in a wider story — connected to others by the trip, the craft, the region, and the structural pressures they share.

**Layout:** Full-width section, dark `bg-2`. Tabbed or chip-filtered, with each lens surfacing 1–3 household cards.

**Four connection lenses:**

| Lens | Vietnamese label | What it surfaces |
|------|------------------|------------------|
| Same trip | Cùng chuyến đi | Households visited on the same field date |
| Same craft | Cùng nghề | Other households practicing the same craft (e.g. Nắng vs adjacent ceramics — the "divergence" pairing) |
| Same region | Cùng vùng | Other households in the same province / Mekong sub-region |
| Same theme | Cùng câu chuyện | Households linked by a structural pattern — succession code, supply-chain pressure, cooperative model, recognition history |

**Default selected lens** is *Same theme* — the most editorially interesting and the lens that makes the platform feel like an atlas, not an archive.

**Card content:**
```
[Pill: lens-specific label]
e.g. "Cũng là 'Thế hệ cuối'"

[h4: Artisan name]
Lê Thị Huých

[Subtext: craft + location]
Đan lát · Củ Chi, TP.HCM

[1-line connection rationale — Manrope 13px muted]
Bốn thế hệ một nghề. Không có người kế.

[Bottom: Trip date]
01/04/2026
```

**Connection rationale is editorial.** The lens is structural, but the line of text under each card is a sentence written by the heritage-analyst — it explains *why this household, on this lens*. This is the connective tissue the council was asking for.

**No more than 3 cards per lens.** If fewer than 3 connections exist on a lens, show what exists. If a lens has zero connections (e.g. "Same craft" when no other ceramicists are in the corpus yet), hide that lens entirely. Do not show empty states.

**Theme tags driving "Same theme" matching** (from `_tags` in schema.json):
- `succession_intent_code` (last-generation, no-successor, passing-on, growing)
- `material_supply_risk` (high, distant, fragile-corridor)
- `recognition_history` (state-recognized, presidential visit, certified artisan)
- `business_model` (cooperative, exporter, revival-founder, traditional-only)

**This is also the platform's atlas surface.** As the corpus grows beyond 5 households, this section becomes the primary cross-trip navigation. v1 treated it as a stub; v2 treats it as the gateway between profile and platform.

---

## Footer (not numbered)

A single horizontal section, dark `bg-3`. Contains:

**Left column — Methodology disclosure (single, not per-section):**
```
Trang này được biên soạn từ phỏng vấn ngày 01/04/2026 (Phiên A004),
phiên âm bằng faster-whisper large-v3, và biên tập với hỗ trợ
của Claude Sonnet 4.6 từ Mapme. Trích dẫn nguồn đầy đủ ở mỗi đoạn.
Bản gốc tiếng Việt được lưu giữ.
```

**Middle column — Data gaps (honest list):**
```
Khoảng trống dữ liệu:
📍 Tọa độ GPS chính xác — chưa ghi lại
📷 Một số ảnh quy trình — chưa có
📏 Diện tích xưởng — ước tính
💰 Số liệu tài chính — ẩn để bảo vệ nghệ nhân
```

**Right column — Actions:**
```
[ Báo lỗi / chỉnh sửa ]
[ Tải dữ liệu (JSON/CSV) ]
[ Trích dẫn (BibTeX, APA) ]
```

**Citation block (collapsed by default, expand on tap):**
```
mapme. (2026). Lê Thị Huých — Đan lát, TP. Hồ Chí Minh.
Craft Village Field Record. Retrieved from mapme.vn/c/basket-weaving-le-thi-huych
```

This is the entirety of the data-provenance treatment. v1's full DATA PROVENANCE section is gone — its content lives here in compact form. Researchers who need more get the level-3 raw download.

---

## The Action Layer

Actions are not a section — they are a layer threaded through the page. This is how the storefront framing manifests in design.

**Where actions appear:**

| Section | Action(s) | When shown |
|---------|-----------|------------|
| HERO | Message · Collaborate / commission · Visit | Always |
| THE ARTISAN | Direct message | Always |
| ECONOMIC PORTRAIT | Commission / partnership / cooperative inquiry | When commercial or institutional channel exists |
| SUCCESSION & FUTURE | Apprenticeship / Support | Always (varies by code) |
| FOOTER | Report correction · Download · Cite | Always |

**Sticky mobile action bar:** Once the hero scrolls out of view on mobile, a sticky bottom bar appears with the household's primary action (usually Message). 56px tall, accent-colored, single-action by default. Researchers and funders are mostly on desktop; the sticky bar serves visitors, partners, and travelers on phones.

**All actions route through mapme.** No direct artisan contact details are exposed on the page. Mapme relays. This protects the artisan and creates a structured response loop.

**This page does not support direct product ordering.** No cart, no checkout, no instant buy flow. When a visitor wants a product, they are expressing interest or opening a conversation through mapme.

**Action confirmation:** Every action button leads to a short form (3–5 fields max) that captures intent + visitor info. After submission, a confirmation message in the artisan's voice register: *"Cảm ơn bạn. Mapme sẽ chuyển lời nhắn tới nghệ nhân và phản hồi trong vòng 3 ngày."*

---

## Helly Lens — Behavioral Check (not aesthetic)

Before finalizing any section, ask: *does this connect to the River layer? Does it move the visitor toward action, not just understanding?*

Specifically:
- The materials section must show that materials travel from rivers, forests, highlands — this is the River layer made visible in supply chains.
- The succession section should feel like watching something precious about to go underwater, *and* offer a way to keep it afloat.
- The quote sections are where Helly's voice lives — they are not decorative.
- Every section that produces an emotional response must offer a next step within that response. *Feeling* without *doing* is the failure mode. The Helly Lens is satisfied only when the page makes the visitor *move*.

---

## Content Length Constraints

Each agent-generated text slot has a maximum. Containers should be sized to these caps; agents must respect them.

| Slot | Max length | If exceeded |
|------|-----------|-------------|
| Hero dek | 2 sentences, ~40 words | Truncate with "…", full text in The Story |
| Artisan signature quote | 15 words | Shorten to most memorable fragment |
| Story lead paragraph | 60 words | Hard cap |
| Story body paragraphs | 3 paragraphs max | Further detail collapses behind "Đọc thêm" |
| Process step description | 25 words | Trim to action + reason only |
| Economic tension forces | 4 bullets per side | Fifth bullet hidden, reveal on tap |
| Succession subtext | 2 sentences | Hard cap — emotional weight, not detail |
| Connection card rationale | 1 sentence, ~15 words | Trim mercilessly |

---

## In-Page Navigation

Once the hero scrolls out of view, a sticky tab bar appears with section anchors:

```
[Nghệ nhân]  [Câu chuyện]  [Xưởng 3D]  [Quy trình]  [Vật liệu]  [Kinh tế]  [Kế nghiệp]  [Kết nối]
```

Manrope 12px, muted unless active. Active = accent color + underline. Solves the long-scroll problem for researchers and officials who skip to specific sections.

---

## Progressive Disclosure

Three levels of detail. Default shows level 1.

| Level | What's shown | Trigger |
|-------|-------------|---------|
| 1 (default) | Prose narrative, signature quotes, key facts | Page load |
| 2 (expanded) | Verbatim Vietnamese source quotes, full process notes, schema gap fields | "Xem nguồn gốc" toggle (per section) |
| 3 (raw) | Download JSON / CSV / BibTeX | Footer "Tải dữ liệu" button |

Level 2 is critical for researchers — they want the verbatim Vietnamese, not just the summary. Surfacing the `_source_quote` fields at level 2 means the page serves both casual readers and scholars without overwhelming either. Level 3 is positioned as a researcher tool — clearly labeled, with schema documentation linked.

---

## Handling Data Variance Across Households

| Scenario | Treatment |
|----------|-----------|
| No process steps extracted | Show "Quy trình chưa được ghi lại đầy đủ" placeholder card with dashed border |
| No memorable memory quote | Skip the blockquote — do not show empty blockquote chrome |
| Economic sentiment = null | Show "Chưa đánh giá" in muted gray — never impute a sentiment |
| Workshop size unknown | Facts strip shows `—`, not `0 m²` |
| No 3D model yet | Zone diagram fallback (always available from tech_specs_notes) |
| Succession code unclear | Show "Chưa rõ" badge in neutral gray |
| No commercial channel data | Hide ECONOMIC PORTRAIT engage row entirely |
| Single connection lens has zero matches | Hide that lens tab |
| Audio of signature quote missing | Hide the inline play button — the quote remains |

The rule: **silence is better than fabrication.** An empty slot with a clear label is more trustworthy than a filled slot with guessed data.

---

## Responsive Behavior

Follow prototype breakpoints:
- `< 780px`: Single column. Steps stack. Artisan card stacks (portrait above text). Facts strip 2-column. Connections lenses become a horizontal-scroll chip bar.
- `< 500px`: Hero text scales down. Meta strip scrolls horizontally. Connection cards single column. Sticky bottom action bar engages.

---

## Implementation Notes for Claude Design

1. Start with `basket_weaving` (Lê Thị Huých) as the reference household — richest data, most dramatic arc, code-3 succession (the most emotionally consequential CTA path).
2. All schema fields map to sections above — no new fields needed.
3. The `_tags` block in `schema.json` drives the "Same theme" lens in CONNECTIONS.
4. `_schema_gaps` block contains important content (production time, supply risk, sales channels, policy impact) — surface these in sections 7, 8, 9.
5. Cross-household data lives in `trips/2026-04-01/outputs/cross/` — the comparator and synthesis inform CONNECTIONS editorial angles.
6. The page accent color (`--accent`) is set per household via a data attribute or CSS override on `<body>` — one variable change should propagate everywhere.
7. **Real media is required for public launch.** Trip 1 photographs exist in the field-trip archive but are not in the prototype repo. Building the prototype with placeholders is acceptable for internal review only. The first public-facing household page must ship with real photographs, audio, and (where it exists) video — placeholders are a transitional state, not a launch state.
8. **The action forms (Message / Collaborate / Visit) need a real backend endpoint** before launch. Stubbing the form in the design is fine; shipping a non-functional form is not. Mapme team to confirm the relay endpoint before public release.

---

## What Got Cut from v1, and Why

| Cut | Reason |
|-----|--------|
| Per-section AI provenance badges (`✦ Tạo bởi heritage-analyst`) | Council unanimous: created a trust problem while solving a transparency problem. Single footer disclosure is enough. |
| Standalone DATA PROVENANCE section | Read as internal documentation, not user value. Compressed into the footer. |
| "What This Page Is NOT" section | Defensive disclaimers signal uncertainty about whether the design works. If the page feels right, it does not need to apologize in advance. |
| Five-card gradient placeholder Media Strip | A wound, not a design. Replaced with a real media gallery; placeholders allowed only as a transitional state, never as a launch state. |
| Related Households as 3-card grid | Too thin to be the connective tissue the platform's claim to authority depends on. Replaced with multi-axis CONNECTIONS. |

---

## Appendix: Sample Content for Design Injection

Two households fully populated. Use these verbatim in mockups.

---

### SAMPLE A — Basket Weaving · Lê Thị Huých

**Accent color:** `#8fad5a` (bamboo green)
**Succession badge:** `#9a3a3a` — "Thế hệ cuối"
**Action triad shown:** Message · *Collaborate / đặt làm* · *Learn this craft* (code 3 emphasis)

---

**HERO**

*Craft pill:* Đan lát
*Location:* Củ Chi · TP. Hồ Chí Minh · Đồng bằng sông Cửu Long

*h1:*
> Lê Thị Huých
> *"Phải làm cho liền. Làm cho đẹp."*

*Dek:*
Bảy mươi năm gắn bó với tre trúc, bà Huých là người thợ đan lát cuối cùng trong một ngôi làng từng có hơn một nghìn hộ làm nghề. Hôm nay, xưởng bà xuất khẩu sang Đức — và không có ai kế nghiệp.

*Action triad:* [ Nhắn tin ] [ Hợp tác / đặt làm ] [ Học nghề ]

*Hero meta:*

| Sinh năm | Kinh nghiệm | Vật liệu | Trạng thái |
|----------|-------------|----------|------------|
| 1954 | 70+ năm | Tre, trúc | Đang hoạt động |

---

**QUICK FACTS STRIP**

| Tỉnh/TP | Nghề | Sinh năm | Kinh nghiệm | Xưởng | Kế nghiệp |
|---------|------|----------|-------------|-------|-----------|
| TP. Hồ Chí Minh | Đan lát | 1954 | 70+ năm | 4.000 m² | Chưa có |

---

**THE ARTISAN CARD**

*Name:* Lê Thị Huých
*Sub:* Đan lát · 70 năm kinh nghiệm · sinh 1954
*Signature quote:*
> "Khó thì bây giờ chỉ cái gia công xi măng. Mình tráng xi măng là cái đó là khó… Phải làm cho liền. Làm cho đẹp."
> [ ▶ Nghe nghệ nhân nói — 38s ]

*Source line:* Ghi âm ngày 01/04/2026 · Phiên A004 · Phiên dịch: mapme

*Buttons:* [ Nhắn tin nghệ nhân ] [ Tải dữ liệu ]

---

**MEDIA GALLERY (sample curation)**

| Slot | Media | Caption |
|------|-------|---------|
| Hero (col-span 8) | Photograph: bà Huých at the cement-coating station | "Lê Thị Huých tại khu tráng xi măng — nơi bà vẫn làm việc một mình." |
| Detail (col-span 4) | Photograph: hands holding split bamboo | "Tre đã phơi đủ độ ẩm — sẵn sàng vào máy chẻ nan." |
| Audio (col-span 6) | 38s clip — signature quote | "Bà Huých nói về công đoạn khó nhất." |
| Workshop (col-span 6) | Photograph: drying yard with stacked bamboo | "Khoảng 1.500 m² của xưởng dành cho phơi trúc." |
| Process (col-span 4) | Photograph: container being loaded | "Một trong 200+ container 40 feet xuất sang Đức mỗi năm." |
| Video (col-span 8) | 60s clip — workshop walk-through | "Đi qua xưởng từ kho phơi đến phòng tráng xi măng." |

---

**THE STORY**

*h2:* Bốn thế hệ, một đôi tay

*Lead paragraph (drop cap B):*
Bà nội của bà Huých bắt đầu đan. Mẹ bà tiếp tục. Bà lớn lên trong xưởng, tay cầm nan trúc trước khi biết đọc. Làng Thái Mỹ, Củ Chi, từng có hơn một nghìn hộ làm nghề đan lát. Hôm nay chỉ còn một — bà.

*Paragraph 2:*
Đỉnh cao là những năm xuất khẩu: hơn 200 container 40 feet mỗi năm, bán đi Đài Loan, mang về cả tỷ đồng. Năm 2014, chủ tịch nước đến thăm xưởng. Bà nhớ ngày đó như nhớ một giấc mơ sáng — không phải vì danh dự, mà vì lúc đó nghề còn sống.

*Paragraph 3:*
Rồi Đài Loan chuyển sang nhựa. Mười sáu container hàng tồn — trị giá ba tỷ đồng — phải đốt theo lệnh. Bà kể chuyện này không có nước mắt, chỉ có cái giọng phẳng của người đã qua nhiều lần không ngờ mình vẫn đứng lại được.

*Blockquote:*
> "Năm 2005, chồng mới mất. Tôi mượn tiền trả một trăm triệu để mở rộng đường cho xe container vào. Hai mươi cây vàng. Lúc đó tôi không có lựa chọn — hàng đang chờ."
>
> *— Lê Thị Huých, Củ Chi, 01/04/2026*

*Translation sub:* *(In 2005, husband had just passed. Borrowed and paid 100M VND — 20 taels of gold — to widen the road so export containers could reach the workshop. No choice. Goods were waiting.)*

*h3:* Tráng xi măng — dấu ấn của người thợ bậc thầy

*Paragraph:*
Đan nan là kỹ năng ai cũng học được sau vài tháng. Tráng xi măng bên trong sản phẩm — lớp lót giữ hình dáng, chống thấm, làm cho vật liệu sống lâu — là thứ mất hàng chục năm mới thành thạo. Bà mô tả nó bằng hai chữ: *liền* và *đẹp*. Không có chữ thứ ba.

---

**3D HOUSEHOLD LAYOUT**

*Headline stat:* ~4.000 m² · Củ Chi, TP. Hồ Chí Minh

*Zone legend:*

| Zone | Tên | Mô tả |
|------|-----|-------|
| A | Kho & phơi trúc | Khu vực lớn nhất. Trúc nhập về phơi nắng đến độ ẩm 60–70%. Không có nắng = không có sản xuất. |
| B | Xưởng chẻ nan | Mái che. Máy chẻ nan điện, máy cưa, máy khoan. Tiếng ồn chính trong xưởng. |
| C | Khu đan (phân tán) | Công đoạn đan được giao đến nhà hàng xóm đã qua đào tạo. Không tập trung tại xưởng. |
| D | Phòng tráng xi măng | Không gian kín. Công đoạn đòi hỏi tay nghề cao nhất. Chỉ bà Huých và một vài thợ lành nghề thực hiện. |
| E | Kho & bãi container | Khu xuất hàng. Container 40 feet vào được nhờ con đường bà đã trả 100 triệu để mở rộng. |

*Zone D tooltip quote:*
> "Phải làm cho liền. Làm cho đẹp."

---

**CRAFT PROCESS**

*Section header:* Quy trình làm một chiếc chậu tre
*Time badge:* 1–2 ngày gia công + 10–14 ngày hoàn thiện tại công ty

| # | Bước | Mô tả |
|---|------|-------|
| 01 | Cắt trúc | Cây trúc nhập từ miền Tây được cắt thành đoạn theo kích thước sản phẩm. |
| 02 | Phơi khô | Phơi nắng đến khi đạt độ ẩm 60–70%. Bỏ qua bước này → nan bị nứt trong máy. |
| 03 | Chẻ nan | Máy chẻ chia trúc thành nan mỏng đều. Trước kia làm tay, nay máy hóa để đáp ứng xuất khẩu. |
| 04 | Đan theo khuôn | Nan được đan quanh khuôn mẫu do công ty cung cấp. Tiêu chuẩn đồng đều — KCS kiểm tra. |
| 05 | Tráng xi măng | Lớp xi măng tráng bên trong. Phải liền mạch, không bong tróc. Đây là công đoạn phân biệt thợ giỏi. |
| 06 | Giao công ty hoàn thiện | Công ty xử lý phần ngoài, kiểm định, đóng gói xuất khẩu sang Đức. |

---

**MATERIALS & SUPPLY**

*Origin flow:*
```
Lâm Đồng / Miền Tây  (~300–400 km)
↓  Thương lái thu gom
↓  Vận chuyển xe tải
Xưởng bà Huých — Củ Chi
```

*Origin node color:* `#c46030` (distant / at risk)

*Supply risk:* ● Cao

- Trúc tre địa phương bị phá hết để làm đường (*"họ phá hết… họ làm đường làm xá"*)
- Phải mua từ tận miền Tây, vận chuyển xa hàng trăm km
- Không có nhà cung cấp ổn định — phụ thuộc vào thương lái đi thu gom

*Environmental dependencies:*
Phụ thuộc: nắng (phơi khô 60–70%)
Rủi ro: mùa mưa → mốc trên trúc đã xử lý

*Waste profile:*
Phế liệu tre: đốt | Nhựa: xe rác đô thị thu gom | Xi măng thừa: đổ bỏ tại chỗ

*Hộ khác có chuỗi cung tương tự:*
- **Mành tre — Bình Dương** · Cùng phụ thuộc vào trúc nhập từ miền Tây →

---

**ECONOMIC PORTRAIT**

*Sentiment word:* **Bấp bênh**
*Sentiment color:* `#c49a30` (amber)
*Sentiment quote:*
> "Làm nghề này cực lắm… muốn nghỉ làm nhưng ráng duy trì."

*Business model:*

| Kênh bán hàng | Lao động | Thị trường |
|---------------|----------|------------|
| Xuất khẩu qua một công ty lớn | ~40 lao động thời vụ (đan tại nhà) | Đức (chính), trước đây Đài Loan |

*Tension forces:*

| Sức mạnh | Áp lực |
|----------|--------|
| 30 năm kinh nghiệm xuất khẩu | Phụ thuộc một khách hàng duy nhất |
| Xưởng 4.000 m² tự có | Thuế cao, tự động trừ từ tài khoản ngân hàng |
| Hợp đồng bao tiêu ổn định | Nguyên liệu ngày càng đắt và xa |
| Thương hiệu được nhà nước ghi nhận (2014) | Không có người kế nghiệp |

*Engage row:* [ Hỏi về đặt làm / hợp tác ] [ Hợp tác xuất khẩu ]

---

**SUCCESSION & FUTURE**

*Code 3 — Thế hệ cuối*

> *"Con gái không theo nghề. Người trẻ đi học hết. Tôi làm bao lâu còn sức thì làm."*
>
> *— Lê Thị Huých*

*Subtext:* Các con và cháu bà đã tốt nghiệp đại học, làm hiệu trưởng và thạc sĩ. Bà không oán giận điều đó — bà tự hào. Nhưng khi bà dừng, kỹ thuật dừng cùng.

*CTA:* [ Bạn muốn học nghề đan lát truyền thống? Liên hệ qua mapme → ]

---

**CONNECTIONS**

*Default lens: Cùng câu chuyện*

| Card | Why connected |
|------|---------------|
| **Mành tre — artisan Đại / Thai Thi Thanh** (Bình Dương) | Cũng là người xuất khẩu cuối cùng còn lại trong khu vực. 80%+ hàng xóm đã đóng cửa. |
| **Gốm Tư Thố — Huê Anh** (Lái Thiêu) | Cùng câu chuyện "không có người kế." Cùng cảm nhận: nghề sống bao lâu thì sống. |
| **Đan lát — không có** | (Lens "Cùng nghề" ẩn — chưa có hộ đan lát khác trong dữ liệu.) |

---

### SAMPLE B — Nắng Ceramics · Huỳnh Xuân Huỳnh

**Accent color:** `#c4623a` (terracotta)
**Succession badge:** `#6b9a3a` — "Đang truyền nghề"
**Action triad shown:** Message · *Collaborate / đặt làm* · *Apprenticeship / partner workshop* (code 1 emphasis)

---

**HERO**

*Craft pill:* Gốm Lái Thiêu
*Location:* Lái Thiêu · Bình Dương · Đồng bằng sông Cửu Long

*h1:*
> Huỳnh Xuân Huỳnh
> *"Một nét vẽ tạo nên hình dáng"*

*Dek:*
Năm 29 tuổi, Huỳnh dùng toàn bộ tiết kiệm của mình để đặt 500 chiếc chén đầu tiên. Hôm nay, Nắng Ceramics là một trong số ít thương hiệu đang khôi phục gốm Lái Thiêu — loại gốm từng định hình cái đẹp của Nam Bộ suốt một thế kỷ.

*Action triad:* [ Nhắn tin ] [ Hợp tác / đặt làm ] [ Tham quan / thực tập ]

*Hero meta:*

| Sinh năm | Kinh nghiệm | Vật liệu | Trạng thái |
|----------|-------------|----------|------------|
| 1997 | 8 năm | Đất cao lanh, men tro, men đá | Đang hoạt động |

---

**QUICK FACTS STRIP**

| Tỉnh/TP | Nghề | Sinh năm | Kinh nghiệm | Xưởng | Kế nghiệp |
|---------|------|----------|-------------|-------|-----------|
| Bình Dương | Gốm Lái Thiêu | 1997 | 8 năm | 4.000 m² | Đang truyền |

---

**THE ARTISAN CARD**

*Name:* Huỳnh Xuân Huỳnh
*Sub:* Gốm Lái Thiêu · 8 năm kinh nghiệm · sinh 1997 · Người sáng lập Nắng Ceramics
*Signature quote:*
> "Nó là một nét vẽ tạo nên một cái hình dáng… hỏi cái sự dứt khoát của người thợ."
> [ ▶ Nghe nghệ nhân nói — 42s ]

*Source line:* Ghi âm ngày 01/04/2026 · Phiên A005 · Phiên dịch: mapme

*Buttons:* [ Nhắn tin nghệ nhân ] [ Tải dữ liệu ]

---

**MEDIA GALLERY (sample curation)**

| Slot | Media | Caption |
|------|-------|---------|
| Hero | Photograph: Huỳnh at the throwing wheel | "Huỳnh Xuân Huỳnh trên bàn xoay — một trong ba kỹ thuật tạo hình của xưởng." |
| Detail | Photograph: brush on ceramic | "Vẽ thảo: một nét, không sửa." |
| Audio | 42s clip — signature quote | "Triết học của một nét cọ." |
| Workshop | Photograph: kiln with altar | "Bàn thờ Ông thần lò trước cửa lò nung — trung tâm tinh thần của xưởng." |
| Product | Photograph: finished bowls in showroom | "Sản phẩm hoàn thiện — chuẩn bị xuất xưởng." |
| Video | 75s — vẽ thảo demonstration | "Vẽ con gà Lái Thiêu — kỹ thuật truyền lại từ thợ Triều Châu." |

---

**THE STORY**

*h2:* Khôi phục gốm Lái Thiêu — một nét vẽ dứt khoát

*Lead paragraph (drop cap N):*
Nắng Ceramics bắt đầu từ 500.000 đồng — toàn bộ tiết kiệm của Huỳnh khi còn là sinh viên. Đủ để đặt 500 chiếc chén tại một lò gốm già ở Lái Thiêu. Anh không biết chúng sẽ bán được không. Nhưng anh biết gốm Lái Thiêu truyền thống đang biến mất khỏi các tiệm bán đồ, khỏi bàn ăn của người Sài Gòn — và điều đó không ổn.

*Paragraph 2:*
Lái Thiêu từng là trung tâm gốm Nam Bộ, mang theo kỹ thuật của người Triều Châu, Phúc Kiến, Quảng Đông di cư qua nhiều thế kỷ. Mỗi dòng người mang một kỹ năng: vẽ xanh trắng, đắp nổi, men tro. Cái con gà trống vẽ trên chén — con gà không có ở đâu giống gà Lái Thiêu — là kết quả của những cuộc gặp gỡ văn hóa đó, được chắt lọc qua nhiều đời thợ.

*Paragraph 3:*
Anh tiếp nhận lại lò từ một người chủ lò lớn tuổi không còn người kế. Hiện Nắng đào tạo sinh viên thực tập, hợp tác với các lò khác trong làng, và bán sản phẩm đến nhà hàng và nhà sưu tầm trong nước. Không giàu — anh nói thẳng điều đó. Nhưng nghề sống.

*Blockquote:*
> "Nhà mình có truyền thống nấu ăn cầu kỳ. Hồi nhỏ hay dùng gốm Lái Thiêu. Rồi ra tiệm không thấy bán nữa. Đó là lúc mình nghĩ phải làm điều gì đó."
>
> *— Huỳnh Xuân Huỳnh, Lái Thiêu, 01/04/2026*

*h3:* Vẽ thảo — triết học của sự không hoàn hảo

*Paragraph:*
Kỹ thuật vẽ thảo là vẽ một nét liên tục, không sửa. Nét cọ tiếp xúc đất ướt — nếu do dự, nét sẽ loang. Nếu vội, nét sẽ gãy. Huỳnh gọi đây là triết học: *"không hoàn hảo"* không phải lỗi — đó là dấu vết của con người thật sự làm ra vật. Máy không thể tạo ra điều đó. Đó là lý do gốm thủ công có giá trị.

---

**3D HOUSEHOLD LAYOUT**

*Headline stat:* ~4.000 m² (xưởng chính) + 100 m² (xưởng phụ) · Lái Thiêu, Bình Dương

*Zone legend:*

| Zone | Tên | Mô tả |
|------|-----|-------|
| A | Xưởng xử lý đất | Máy nghiền đất, trộn cao lanh từ Tây Nguyên. Bắt đầu của mọi sản phẩm. |
| B | Phòng tạo hình | Bàn xoay điện, khuôn, be chạch tay. Ba kỹ thuật tạo hình khác nhau trong cùng một phòng. |
| C | Khu phơi sản phẩm | Giàn phơi ngoài trời. Mùa nắng: ưu tiên chén dĩa. Mùa mưa: chuyển sang đồ đắp nổi. |
| D | Phòng tráng men & vẽ | Vẽ thảo được thực hiện ở đây. Ánh sáng tự nhiên. Yên tĩnh — công đoạn đòi hỏi tập trung cao. |
| E | Lò nung củi (vỏ cao su) | Trung tâm tinh thần của xưởng. Bàn thờ Ông thần lò đặt tại cửa lò. Đốt bằng vỏ cây cao su. |
| F | Lò điện thử men | Lò nhỏ, thử nghiệm công thức men mới từ Pháp, Nhật, Trung Quốc, Đài Loan. |
| G | Showroom & kho | Bán sỉ cho thương lái và khách trực tiếp. Sản phẩm bị bể → bán làm vật liệu xây dựng. |

*Zone E tooltip quote:*
> "Lò chén kị nung có đâm tiêu — chữ tiêu nghe như tiêu tán. Người chủ lò không được đi đám tang khi lò đang đốt."

---

**CRAFT PROCESS**

*Section header:* Quy trình làm một chiếc chén gốm Lái Thiêu
*Time badge:* Chén, dĩa: 1 ngày · Sản phẩm cầu kỳ: nhiều ngày hơn

| # | Bước | Mô tả |
|---|------|-------|
| 01 | Xử lý đất | Cao lanh từ Tây Nguyên nghiền mịn, trộn tỷ lệ. Đất Lái Thiêu gốc đã cạn kiệt — nay lấy từ xa. |
| 02 | Tạo hình | Ba cách: xoay tay (thủ công nhất), khuôn (nhanh, đồng đều), be chạch (cho hình dạng phức tạp). |
| 03 | Phơi và sửa | Để khô sơ. Kiểm tra, sửa lỗi nhỏ. Mùa mưa giai đoạn này kéo dài hơn. |
| 04 | Nhúng men ướt | Nhúng cả sản phẩm vào men. Men tro, men đá, men da lươn — mỗi loại cho màu sắc khác nhau. |
| 05 | Vẽ trang trí | Vẽ thảo bằng cọ — một nét, không sửa. Chim, gà, hoa lan, điên điển. Dấu ấn của người thợ. |
| 06 | Nung củi | Lò nung vỏ cây cao su. Nhiệt độ và thời gian kiểm soát bằng kinh nghiệm, không bằng máy. |
| 07 | Kiểm tra & phân loại | Sản phẩm đạt → bán. Bể, nứt → làm vật liệu xây dựng. Gần như không có rác thải. |

---

**MATERIALS & SUPPLY**

*Origin flow:*
```
Tây Nguyên / Đà Lạt  (~250 km) — đất cao lanh
Pháp / Nhật / Đài Loan — men oxit nhập khẩu
↓  Thương lái + nhập khẩu trực tiếp
Xưởng Nắng Ceramics — Lái Thiêu, Bình Dương
```

*Origin node color:* `#c46030` (distant / imported)

*Supply risk:* ● Trung bình–Cao

- Đất Lái Thiêu truyền thống khai thác hết, bị chôn vùi dưới khu dân cư
- Giá nguyên liệu tăng 10 lần trong 8 năm
- Men oxit nhập từ 4 quốc gia — dễ bị ảnh hưởng tỷ giá

*Waste profile (gần như khép kín):*
Đất thừa/bể: tái dùng để vẽ hoặc trộn lại | Nước rửa màu: lắng lọc dùng lại | Chén bể: bán làm vật liệu xây dựng

*Hộ khác có chuỗi cung tương tự:*
- **Gốm Tư Thố — Huê Anh** (Lái Thiêu) · Cùng làng, cùng nguyên liệu, kết quả khác →

---

**ECONOMIC PORTRAIT**

*Sentiment word:* **Bền vững**
*Sentiment color:* `#6b9a3a` (green — sustainable, not rich)
*Sentiment quote:*
> "Làm nghề gốm bấp bênh, nghề không đói mà cũng không giàu. Thu nhập đủ ăn — khó khăn nhưng không phải vấn đề bận tâm lớn."

*Business model:*

| Kênh bán hàng | Lao động | Thị trường |
|---------------|----------|------------|
| Thương lái tại lò (chính), cửa hàng lưu niệm, xuất khẩu gián tiếp | Nhân viên cố định + thực tập sinh | Trong nước (nhà hàng, nhà sưu tầm), một phần xuất khẩu |

*Tension forces:*

| Sức mạnh | Áp lực |
|----------|--------|
| Thương hiệu rõ ràng, có câu chuyện | Chính sách cấm xây lò mới |
| Doanh nghiệp hóa (có kế toán) | Lò cũ phải hoạt động liên tục — ngừng = mất giấy phép |
| Đào tạo sinh viên, kết nối mạng lưới | Giá đất và nguyên liệu tăng liên tục |
| Workshop + nghiên cứu bổ sung thu nhập | Khu dân cư mới xung quanh gây áp lực môi trường |

*Engage row:* [ Hỏi về đặt làm ] [ Hợp tác xưởng / thực tập ]

---

**SUCCESSION & FUTURE**

*Code 1 — Đang truyền nghề*

> *"Nắng Ceramics hỗ trợ truyền nghề cho các bạn sinh viên — sinh viên có thể trở thành nhân viên, hay mở thương hiệu riêng. Mình muốn chia sẻ kỹ thuật, không giữ cho riêng mình."*
>
> *— Huỳnh Xuân Huỳnh*

*Subtext:* Tại 29 tuổi, Huỳnh vừa là nghệ nhân trẻ nhất trong mẫu vừa là người duy nhất chủ động xây dựng tương lai cho nghề. Mô hình của anh — truyền nghề như dự án cộng đồng, không phải di sản gia đình — là điểm khác biệt quan trọng nhất trong cả chuyến thực địa.

*CTA:* [ Đăng ký thực tập tại Nắng Ceramics → ]

---

**CONNECTIONS**

*Default lens: Cùng câu chuyện*

| Card | Why connected |
|------|---------------|
| **Nhang — Nguyễn Cát Phụi Thuý** (Bến Tre) | Cùng câu chuyện "đang truyền nghề" — xây dựng hợp tác xã 47 hộ. |
| **Gốm Tư Thố — Huê Anh** (Lái Thiêu) | Cùng nghề, cùng làng, đường đi khác — Huê Anh làm theo mô hình truyền thống không có thương hiệu. So sánh trực tiếp. |
| **Đan lát — Lê Thị Huých** (Củ Chi) | Cùng vùng (Đông Nam Bộ), nhưng đối lập về kế nghiệp — Code 1 vs Code 3. |
