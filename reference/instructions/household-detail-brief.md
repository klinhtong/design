# Craft Household Detail Page — Design Brief
**For:** Claude Design  
**From:** Mapme Data Team  
**Date:** 2026-05-10  
**Reference prototype:** `village-ren-phu-my.html`

---

## What This Page Is

A **household-level** portrait of one artisan and their craft. Not a village directory entry — a story that can be felt. The artisan is the protagonist. The craft is the context. The economics and ecology are the tension.

This page sits one level deeper than the village map. User arrives from tapping a dot on the map or a household card. They leave knowing a person, not just a craft type.

**Audience:** Designers seeking authentic provenance, researchers documenting heritage, heritage officials tracking viability, curious travelers, and the artisan's own family.

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
1.  HERO                    — Identity + emotional hook
2.  QUICK FACTS STRIP       — 6 scannable data points
3.  THE ARTISAN             — Person card + signature quote
4.  MEDIA STRIP             — Photo/video placeholders (future-ready)
5.  THE STORY               — Heritage narrative (prose)
6.  3D HOUSEHOLD LAYOUT     — Spatial portrait of the workshop
7.  CRAFT PROCESS           — Step-by-step visual
8.  MATERIALS & SUPPLY      — Where things come from
9.  ECONOMIC PORTRAIT       — Viability, income, markets
10. SUCCESSION STATUS       — Future of the craft
11. RELATED HOUSEHOLDS      — Navigation out
```

**Removed:** DATA PROVENANCE — inline AI-generation badges (✦ Tạo bởi heritage-analyst) on each section handle provenance signal adequately. A full section reads as internal documentation, not user value.

---

## Section Specs

---

### 1. HERO

**Emotional intent:** You are entering someone's world, not reading a database entry.

**Layout:** Full-bleed, min-height 80vh. Content aligned bottom-left. Background is a craft-specific gradient — no photos (Trip 1 has none). Gradients must feel like the material itself.

**Background gradient per craft:**
- Basket weaving: `linear-gradient(135deg, #1a2010 0%, #2d3d18 30%, #4a6124 60%, #6b8a3a 100%)` — bamboo at dusk
- Nắng Ceramics: `linear-gradient(135deg, #2a1208 0%, #4a2010 30%, #7a3518 60%, #c05028 90%)` — kiln glow
- Incense: `linear-gradient(135deg, #1a0f18 0%, #2e1428 40%, #5a2848 70%, #8a4060 100%)` — smoke at dawn

**Content:**

```
[Pill: craft type in Vietnamese]   [Province · Region]

[h1 — Fraunces italic]
Artisan full name
"Memorable short tagline" ← from artisan_memorable_memory or signature quote

[Dek — Fraunces light]
2–3 sentence emotional hook. Written from heritage narrative.
Not facts — the WHY this person matters.

[Meta strip — bottom, above border]
Năm sinh  |  Kinh nghiệm  |  Vật liệu chính  |  Trạng thái
1954       |  70+ năm      |  Tre trúc         |  Đang hoạt động
```

**Succession state badge:** Top-right corner of hero. Subtle pill:
- Code 1 (passing on): `#6b9a3a` green pill — "Đang truyền nghề"
- Code 2 (desired but rejected): `#c49a30` amber — "Chưa có người kế"  
- Code 3 (resigned/last): `#9a3a3a` muted red — "Thế hệ cuối"

This is the one piece of data that orients the reader emotionally before they read anything else.

**h1 structure:** Always `<br>` between artisan name and tagline — never run them together inline:
```html
<h1 class="title">Lê Thị Huých<br><em>"Phải làm cho liền. Làm cho đẹp."</em></h1>
```

---

### 2. QUICK FACTS STRIP

**Layout:** 6-column grid, same as prototype. Full-width, max 880px centered.

**Fields (from schema.json):**

| Label | Field | Example |
|-------|-------|---------|
| Tỉnh/TP | province | TP. Hồ Chí Minh |
| Nghề | craft type (VI) | Đan lát |
| Sinh năm | artisan_year_of_birth | 1954 |
| Kinh nghiệm | artisan_years_of_experience | 70+ năm |
| Xưởng | workshop_size_sqm | 4.000 m² |
| Kế nghiệp | succession_intent_code (text) | Chưa có |

If `workshop_size_sqm` is null, show "Không có dữ liệu" in muted style — do not hide the cell.

---

### 3. THE ARTISAN

**Emotional intent:** This is a person, not a profile.

**Layout:** Two-column card (same as `.artisan-card` in prototype). Left: portrait placeholder. Right: name, role, signature quote, actions.

**Portrait placeholder:** Craft-specific gradient with subtle texture overlay. No silhouette or icon — the gradient IS the portrait until photos exist. Add a small corner label: "Ảnh: chưa có · Chuyến thực địa tiếp theo".

**Content:**

```
[Pill: Nghệ nhân]

[h2 — Fraunces 28px]
Lê Thị Huých

[Subhead — Manrope 13px muted]
Đan lát · 70 năm kinh nghiệm · sinh 1954

[Signature quote — Fraunces italic 20px]
"Phải làm cho liền. Làm cho đẹp."
← This is the artisan's "soul" from heritage.md

[Source line — Manrope 12px muted]
Ghi âm ngày 01/04/2026 · Phiên A004 · Phiên dịch: mapme

[Actions row]
[Primary: Nhắn tin]  [Secondary: Nghe bản ghi âm]
```

---

### 4. MEDIA STRIP

**Emotional intent:** Photos are the most wanted thing on this page. This section holds the slot — gracefully — until they exist.

**Layout:** Full-width horizontal strip, `bg-2` background, no vertical padding waste. Cards overflow-scroll on mobile. No section heading — it flows visually between the Artisan card above and The Story below.

**Five placeholder cards, left to right:**

| Slot | Aspect | Label | Gradient (basket weaving example) |
|------|--------|-------|-----------------------------------|
| Chân dung nghệ nhân | 3:4 (portrait) | Ảnh chân dung | Same as artisan portrait — craft gradient |
| Ảnh xưởng sản xuất | 16:9 (wide) | Không gian xưởng | Darker craft gradient |
| Sản phẩm đặc trưng | 1:1 (square) | Sản phẩm | Mid-tone craft gradient |
| Quy trình thực tế | 16:9 (wide) | Quy trình | Darker variant |
| Ghi âm / Video | 16:9 (wide) | Audio · Video | Darkest + ▶ icon centered |

**Per card:**
- Craft-specific gradient fill (same family as hero, darker variants)
- Manrope 11px label centered vertically
- Corner chip top-right: `📷 Chuyến thực địa tiếp theo` — Manrope 9px, bg-muted pill
- When photo available: `<img>` fills the card, chip removed, label becomes caption below

**When photos exist:** Drop the corner chip. Show a caption line below the card: artisan name + date taken, Manrope 11px muted. The layout does not change — slots are pre-sized.

**Audio/Video slot (rightmost):** Show a ▶ play button overlay (40px circle, accent-colored, centered). When audio exists, clicking plays the transcript recording in-page. The "Nghe bản ghi âm" button in the Artisan card is the primary CTA for this — the video slot here is the preview surface.

---

### 5. THE STORY

**Emotional intent:** The reader should feel the weight of what this person has built and what might be lost.

**Layout:** Full-width prose article, max 680px, centered. Same as `article.story` in prototype. Drop cap on first paragraph.

**Content structure:**

```
[h2 — Fraunces 40px]
Section title — derived from heritage narrative. E.g.:
"Bốn thế hệ, một đôi tay"

[Lead paragraph — Fraunces 22px, drop cap]
The craft origin story. Where it began, how long it's been in the family.
Source: heritage.md → Craft Origin Story section.

[Body paragraphs — Fraunces 18.5px]
The artisan's life in the craft. Include:
- Years started, how learned (from father/mother/self-taught)
- The peak years (e.g. 200+ containers/year, President visited 2014)
- The turn — when things changed (Taiwan market, urbanization)
- How they feel about continuing

[Blockquote — centered, italic Fraunces 28px]
The memorable memory.
Source: artisan_memorable_memory_source_quote (Vietnamese verbatim)
With translated subtitle in Manrope 13px.

[h3 — Fraunces 22px]
"Kỹ thuật" or "Tinh hoa nghề"

[Body]
The mark of mastery. What only an expert can do.
Source: heritage.md → "The Artisan's Soul" section.
```

**Vietnamese quotes:** Always show Vietnamese original first, English translation below in smaller muted text. Never replace — both languages live together.

---

### 5. 3D HOUSEHOLD LAYOUT

**Emotional intent:** The reader understands the physical world this artisan inhabits — scale, flow, which zones matter, how space and craft are inseparable.

**When available (current state):** Embed an interactive 3D model (Spline or Three.js). The model shows the household plot from above at a slight isometric angle — not photorealistic, but warm and schematic. Same palette as the page: dark ground, accent-colored zone highlights, paper-white labels.

**When not available:** Graceful fallback — a labeled zone diagram (SVG, same visual style). Dashed outlines for zones, Manrope labels, small dimension badges. Never hide the section entirely — the spatial context always matters.

**Layout:** Full-bleed section, dark bg-2. Model/diagram takes 70% of width. Right sidebar: zone legend + headline stat ("~4.000 m² · Củ Chi, TP.HCM").

**Interaction (3D state):**
- Hover/tap a zone → tooltip slides in: zone name + what happens here + one artisan quote about that zone
- Camera starts at overview; user can orbit
- Zone highlight uses `--accent` color on hover

**Zone data per craft (inferred from tech_specs_notes + economics):**

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

**Fallback diagram spec:** Zones as rounded rectangles, proportional to area, arranged spatially (not a flowchart). Each zone: accent-border, zone letter badge, name label. A simple compass indicator (N/S) bottom-right. No GPS coordinates needed — this is a schematic, not a map.

**Data source:** `tech_specs_notes` field + economics.md inference. If `workshop_size_sqm` is null, omit the dimension badge; show zones without scale.

---

### 7. CRAFT PROCESS

**Layout:** Dark background section (`bg-2`), 3-column step grid (same as `.process` in prototype).

**Content:** Derived from `tech_specs_notes` in schema.json — split into discrete numbered steps.

**Per step card:**
```
[Number — Fraunces 42px accent color]
01

[Step name — Manrope 500 15px]
Cắt trúc

[Description — Manrope 13.5px muted]
Short description of what happens at this stage.
```

**Step count varies by craft:**
- Basket weaving: ~6 steps (cut, dry, split, weave, cement-coat, QC)
- Nắng Ceramics: ~7 steps (clay prep, throwing, bisque, glaze, paint, fire, finish)
- Incense: ~5 steps (bamboo prep, paste mixing, roll, dry, bundle)

**If steps are ambiguous in data:** Show what's confirmed, add one card at the end with dashed border — "Ghi chú: Một số công đoạn chưa được ghi lại đầy đủ." This is better than inventing steps.

**Time badge:** Top of section, right-aligned: "Thời gian sản xuất: 1–2 ngày / sản phẩm" — from `_schema_gaps.production_time_per_item`.

**Step card thumbnail:** Each step card has a 48×48px square placeholder in top-right corner — craft gradient, dashed border, `📷` icon centered. When process photos from future trips arrive, the image fills this slot. Keeps cards from feeling text-only and reserves space for rich media.

---

### 8. MATERIALS & SUPPLY CHAIN

**Emotional intent:** The reader understands that making this object requires a supply chain that's quietly fracturing.

**Layout:** Two-column, left = flow diagram, right = supply risk panel.

**Left — Material Flow (visual):**
A simple vertical flow from source → workshop:

```
[Origin node]
Lâm Đồng / Miền Tây
(province/region pill)
↓  [distance indicator: ~300km]
[Transport node]
Thương lái thu gom
Specialized collectors
↓
[Workshop node]
Xưởng của bà Huých
Củ Chi, TP.HCM
```

Color-code the origin node by supply stability:
- Local (code 0): green — `#6b9a3a`
- Regional (code 1): amber — `#c49a30`
- Distant/at risk (code 2+): red-amber — `#c46030`

All five Trip 1 households are code 1 or higher — local supply is effectively gone for everyone.

**Right — Risk Panel:**
```
[Header: Rủi ro nguồn cung]

[Risk level indicator — text + color dot]
● Cao   ← from material_supply_risk tag

[Bullet list — Manrope 13.5px]
• Tre trúc địa phương đã bị phá để làm đường
• Phải mua từ miền Tây, vận chuyển xa
• Không có nhà cung cấp ổn định tại chỗ

[Environmental dependencies]
Phụ thuộc: nắng, nhiệt độ phơi
Rủi ro: mùa mưa → mốc sản phẩm

[Waste profile — small]
Phế liệu: đốt / thu gom đô thị
```

---

### 9. ECONOMIC PORTRAIT

**Emotional intent:** Honest, not pitying. These people are running businesses. Show the real shape of those businesses.

**Layout:** Full-width section with dark gradient. Three visual components.

**Component A — Sentiment Indicator:**
Not a bar chart. A single large typographic signal:

```
[Label: Cảm nhận kinh tế]
[Large Fraunces word — craft-accent color]

Income sentiment codes:
1 = "Ổn định"      (stable)      → cool green
2 = "Bấp bênh"     (precarious)  → amber  
3 = "Căng thẳng"   (stressed)    → warm red
4 = "Tăng trưởng"  (growth)      → bright green

Below: short verbatim quote explaining their economic situation
```

**Component B — Business Model Snapshot:**
3-cell mini-grid:

| Kênh bán hàng | Lao động | Thị trường |
|---------------|----------|------------|
| Xuất khẩu qua công ty | 40+ lao động thời vụ | Đức, Đài Loan |

Data from `_schema_gaps.primary_sales_channels` and economics.md.

**Component C — Tension Points:**
2-column, each side labeled. NOT a pro/con — it's "forces in tension":

```
[Left: Sức mạnh]                [Right: Áp lực]
• 30 năm xuất khẩu              • Thuế cao, không nhất quán
• Thương hiệu uy tín            • Nguyên liệu ngày càng xa
• Xưởng 4.000m² tự có          • Không có người kế nghiệp
• Hợp đồng bao tiêu             • Lao động già đi
```

Source: economics.md body text — extract the key forces.

**Sensitive data handling:** Never show specific tax amounts (VND) or specific financial losses. Show: "gánh nặng thuế cao" not "26 triệu VND". Show: "thiệt hại lớn khi thị trường thay đổi" not the container count × price. The detail lives in the protected transcript, not the public page.

---

### 8. SUCCESSION STATUS

**Emotional intent:** This section should feel like standing at a crossroads.

**Layout:** Full-width, centered content, max 640px. Large typographic treatment.

**Code 1 — Truyền nghề (Passing on):**
```
[Large Fraunces — green accent]
"Đang truyền nghề"

Subtext: Who is learning, their relation to artisan, how far along.
E.g.: "Con và con rể đã cùng tham gia kinh doanh. 
       47 hộ hàng xóm được đào tạo."
```

**Code 2 — Chưa có người kế (Desired but none):**
```
[Large Fraunces — amber]
"Chưa có người kế"

Subtext: Why. The factory pull explanation. Their feeling about it.
E.g.: "Người trẻ chọn xí nghiệp vì có bảo hiểm xã hội.
       Nghệ nhân hiểu lựa chọn đó, dù không đồng ý."
```

**Code 3 — Thế hệ cuối (Last generation):**
```
[Large Fraunces — muted red, softer tone]
"Thế hệ cuối"

Subtext: Artisan's own words about this. From succession quote.
E.g.: "Con gái không theo nghề. 
       Bà làm bao lâu còn sức thì làm."

[Below: soft call to action]
Nếu bạn muốn học nghề này → [Liên hệ qua mapme]
```

This is the most emotionally sensitive section. Words do the work — but give them a room to sit in.

**Background treatment:** Apply a very faint full-width radial gradient wash keyed to succession color at 8% opacity. Code 3 → `rgba(154,58,58,.08)` centered ellipse. Code 2 → `rgba(196,154,48,.06)`. Code 1 → `rgba(107,154,58,.06)`. Subtle — not a color block. Makes the section feel like the temperature of the page shifted slightly.

---

### 9. DATA PROVENANCE

**Emotional intent:** Radical transparency. The reader should feel safe trusting this data — and know exactly where it comes from and what's missing.

**Layout:** Dark card section, same `.transparency` pattern from prototype. Two sub-sections.

**Sub-section A — Nguồn dữ liệu:**
```
[Grid: 3 cells]

[Cell 1: Thu thập]
Ngày phỏng vấn: 01/04/2026
Phiên: A004 / A005
Phương pháp: Phỏng vấn trực tiếp
Phiên âm: faster-whisper large-v3

[Cell 2: Xử lý]  
Schema: stg__craft_survey v1
Phân tích: Claude Sonnet 4.6
Kiểm tra: Nhóm Mapme

[Cell 3: Độ tin cậy]
Trích dẫn nguồn: ✓ đầy đủ
Xác minh thực địa: ✗ chưa
Ảnh thực tế: ✗ chưa có
GPS chính xác: ✗ chưa có
```

**Sub-section B — Khoảng trống dữ liệu:**
Show the gaps honestly. This builds trust.

```
[Header: Dữ liệu còn thiếu]

[List — Manrope 13px, each gap with a small icon]
📍 Tọa độ GPS chính xác — chưa ghi lại trong chuyến này
📷 Ảnh xưởng và nghệ nhân — chưa có
📏 Diện tích xưởng — ước tính, chưa đo chính xác
💰 Doanh thu cụ thể — ẩn để bảo vệ nghệ nhân

[Footer note]
Dữ liệu này sẽ được bổ sung trong các chuyến thực địa tiếp theo.
Bạn có thể đóng góp thông tin: [Liên hệ]
```

**Sub-section C — Sử dụng dữ liệu:**
Same `transparency-grid` from prototype:
- Left (green): Được sử dụng tự do — tên làng nghề, loại nghề, thông tin chung, trích dẫn học thuật
- Right (amber): Cần xin phép — giọng nói nghệ nhân, ảnh chân dung, sử dụng thương mại

**Citation block:**
```
mapme. (2026). Lê Thị Huých — Đan lát, TP. Hồ Chí Minh.
Craft Village Field Record. Retrieved from mapme.vn/c/basket-weaving-le-thi-huych
[BibTeX]  [APA]  [Chicago]
```

---

### 10. RELATED HOUSEHOLDS

**Layout:** 3-column card grid, same `.related-grid` from prototype.

**What to show:**
1. Other households from the **same trip** (same date, different craft)
2. Other households with the **same succession code** (thematic connection)
3. One **contrasting household** from same craft family (e.g. Nắng vs adjacent ceramics = divergence story)

**Card content:**
```
[Pill: craft type]
[h4: Artisan name]
[Subtext: Succession status · Income sentiment]
[Bottom: Trip date]
```

---

## Content Mapping: All 5 Households

| Household | Artisan | Accent | Succession | Sentiment | Key Story |
|-----------|---------|--------|------------|-----------|-----------|
| basket_weaving | Lê Thị Huých, b.1954 | bamboo green | Code 3 — last | Stable/precarious | Last of 1,000+ households. Paid 100M VND to widen road. Exports to Germany. |
| bamboo_curtain | Artisan Đại + Thai Thi Thanh | amber | Code 2 — none | Declining | Last major exporter in district. 80%+ of neighbors closed due to tax policy. |
| nangs_ceramics | Huỳnh Xuân Huỳnh, b.~1997 | terracotta | Code 1 — active | Sustainable | Revival founder at ~29. Trained interns, built brand, sells internationally. |
| adjacent_ceramics | Huê Anh (Tư Thố), since 1981 | deep clay | Code 2 — none | Precarious | Same craft as Nắng, neighbor. Sells through traders only. No brand. Contrast case. |
| incense | Nguyễn Cát Phụi Thuý, 30+ yrs | rose smoke | Code 1 — growing | Stressed/growing | Built a 47-household cooperative. TikTok + wholesale. Supply chain most fragile. |

---

## Signature Quotes by Household

These are first-class content. Large, centered, verbatim Vietnamese:

- **basket_weaving:** *"Phải làm cho liền. Làm cho đẹp."* — mastery = seamless cement coat
- **bamboo_curtain:** *"Giá trị cốt lõi vẫn là con người. Handmade mà."* — human value of handmade
- **nangs_ceramics:** *"Một nét vẽ tạo nên hình dáng — hỏi cái sự dứt khoát của người thợ."* — decisiveness in the brushstroke
- **adjacent_ceramics:** *"Sản phẩm ra tốt, ra đạt. Thì mình vui."* — quiet pride in the work
- **incense:** *"Không có tâm thì làm không được đâu."* — heart is the prerequisite

---

## Missing Data: Graceful Handling

This page must look intentionally honest, not broken, when data is absent.

| Situation | Treatment |
|-----------|-----------|
| No GPS coordinates | Show province-level map with dashed circle and note "Tọa độ chính xác chưa được ghi lại" |
| No photos | Craft gradient portrait placeholder with corner label "Ảnh: chuyến thực địa tiếp theo" |
| No workshop size | Show dash `—` in facts strip, not 0 or empty |
| Sensitive financial data | Show sentiment word + qualitative range, never specific VND amounts |
| Partial process steps | Show known steps + one dashed "incomplete" card |

---

## Responsive Behavior

Follow prototype breakpoints:
- `< 780px`: Single column. Steps stack. Artisan card stacks (portrait above text). Facts strip 2-column.
- `< 500px`: Hero text scales down. Meta strip scrolls horizontally. Related cards single column.

---

## The Helly Lens (required check)

Before finalizing any section, ask: *does this connect to the River layer? Can it be felt, not just read?*

Specifically:
- The material origin section must show that materials travel from rivers, forests, highlands — this is the River layer made visible in supply chains
- The succession section should feel like watching something precious about to go underwater, not a data field
- The quote sections are where Helly's voice lives — they are not decorative. They are the whole point.

---

## What This Page Is NOT

- Not a tourism promotion — no "visit us!" energy
- Not a pity portrait — artisans are skilled professionals running complex operations
- Not a data dump — every field shown must earn its place emotionally
- Not static — gaps are named, updates are invited, the page is alive

---

## Readability & Scalability

Content is AI-agent-generated (heritage-analyst, economics-analyst, etc.) but read by humans. These rules keep the page coherent across all households regardless of data richness.

### Content Length Constraints

Each agent-generated text slot has a max. Claude Design should size containers around these, not let content overflow.

| Slot | Max length | If exceeded |
|------|-----------|-------------|
| Hero dek | 2 sentences, ~40 words | Truncate with "..." — the full text lives in The Story |
| Artisan signature quote | 15 words | Shorten to most memorable fragment |
| Story lead paragraph | 60 words | Hard cap — agents must respect this |
| Story body paragraphs | 3 paragraphs max | Further detail collapses behind "Đọc thêm" |
| Process step description | 25 words | Trim to action + reason only |
| Economic tension forces | 4 bullets per side | Fifth bullet hidden, reveal on tap |
| Succession subtext | 2 sentences | Hard cap — emotional weight, not detail |

### In-Page Navigation

Once hero scrolls out of view, a sticky tab bar appears with section anchors:

```
[Nghệ nhân]  [Câu chuyện]  [Xưởng 3D]  [Quy trình]  [Vật liệu]  [Kinh tế]  [Kế nghiệp]
```

Manrope 12px, muted unless active. Active = accent color + underline. This solves the long-scroll problem for researchers and officials who skip to specific sections.

### Progressive Disclosure

Three levels of detail. Default shows level 1. Level 2 expands on tap. Level 3 is raw data download.

| Level | What's shown | Trigger |
|-------|-------------|---------|
| 1 (default) | Prose narrative, signature quotes, key facts | Page load |
| 2 (expanded) | Verbatim Vietnamese source quotes, full process notes, schema gap fields | "Xem nguồn gốc" toggle |
| 3 (raw) | Download JSON / CSV / BibTeX | "Tải dữ liệu" button |

Level 2 is critical for researchers — they want the verbatim Vietnamese, not just the summary. Surfacing the `_source_quote` fields at level 2 means the page serves both casual readers and scholars without overwhelming either.

### AI-Generation Quality Signals

Every agent-generated prose block carries a small provenance badge (Manrope 10px, muted, top-right of section):

```
✦ Tạo bởi heritage-analyst · 01/04/2026
```

This signals "AI-generated from interview transcript" — not human-written journalism. The distinction matters for trust. Heritage officials need to know what to verify; researchers need to know what to cite.

### Handling Data Variance Across Households

Some households have rich data; others have gaps. The design must be robust to both.

| Scenario | Treatment |
|----------|-----------|
| No process steps extracted | Show "Quy trình chưa được ghi lại đầy đủ" placeholder card with dashed border |
| No memorable memory quote | Skip blockquote entirely — do not show empty blockquote chrome |
| Economic sentiment = null | Show "Chưa đánh giá" in muted gray — never impute a sentiment |
| Workshop size unknown | Facts strip shows "—" not "0 m²" |
| No 3D model yet | Zone diagram fallback (always available from tech_specs_notes) |
| Succession code unclear | Show "Chưa rõ" badge in neutral gray |

The rule: **silence is better than fabrication**. An empty slot with a clear label is more trustworthy than a filled slot with guessed data.

---

## Implementation Notes for Claude Design

1. Start with `basket_weaving` (Lê Thị Huých) as the reference household — richest data, most dramatic arc
2. All schema fields map to sections above — no new fields needed
3. The `_tags` block in schema.json drives the "Related" section matching logic
4. `_schema_gaps` block contains important content (production time, supply risk, sales channels, policy impact) — surface these in sections 5, 6, 7
5. Cross-household data lives in `trips/2026-04-01/outputs/cross/` — the comparator and synthesis inform "Related" section editorial angles
6. The page accent color (`--accent`) must be set per household via a data attribute or CSS override on `<body>` — one variable change should propagate everywhere

---

## Appendix: Sample Content for Design Injection

Two households fully populated. Use these verbatim in mockups — no placeholder text.

---

### SAMPLE A — Basket Weaving · Lê Thị Huých

**Accent color:** `#8fad5a` (bamboo green)  
**Succession badge:** `#9a3a3a` — "Thế hệ cuối"

---

**HERO**

*Craft pill:* Đan lát  
*Location:* Củ Chi · TP. Hồ Chí Minh · Đồng bằng sông Cửu Long

*h1:*
> Lê Thị Huých  
> *"Phải làm cho liền. Làm cho đẹp."*

*Dek:*  
Bảy mươi năm gắn bó với tre trúc, bà Huých là người thợ đan lát cuối cùng trong một ngôi làng từng có hơn một nghìn hộ làm nghề. Hôm nay, xưởng bà xuất khẩu sang Đức — và không có ai kế nghiệp.

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
*Signature quote (Fraunces italic):*
> "Khó thì bây giờ chỉ cái gia công xi măng. Mình tráng xi măng là cái đó là khó... Phải làm cho liền. Làm cho đẹp."

*Source line:* Ghi âm ngày 01/04/2026 · Phiên A004 · Phiên dịch: mapme

*Buttons:* [Nhắn tin] [Nghe bản ghi âm] [Tải dữ liệu]

---

**THE STORY**

*h2:* Bốn thế hệ, một đôi tay

*Lead paragraph (drop cap B):*  
Bà nội của bà Huých bắt đầu đan. Mẹ bà tiếp tục. Bà lớn lên trong xưởng, tay cầm nan trúc trước khi biết đọc. Làng Thái Mỹ, Củ Chi, từng có hơn một nghìn hộ làm nghề đan lát. Hôm nay chỉ còn một — bà.

*Paragraph 2:*  
Đỉnh cao là những năm xuất khẩu: hơn 200 container 40 feet mỗi năm, bán đi Đài Loan, mang về cả tỷ đồng. Năm 2014, chủ tịch nước đến thăm xưởng. Bà nhớ ngày đó như nhớ một giấc mơ sáng — không phải vì danh dự, mà vì lúc đó nghề còn sống.

*Paragraph 3:*  
Rồi Đài Loan chuyển sang nhựa. Mười sáu container hàng tồn — trị giá ba tỷ đồng — phải đốt theo lệnh. Bà kể chuyện này không có nước mắt, chỉ có cái giọng phẳng của người đã qua nhiều lần không ngờ mình vẫn đứng lại được.

*Blockquote (Fraunces italic 28px centered):*
> "Năm 2005, chồng mới mất. Tôi mượn tiền trả một trăm triệu để mở rộng đường cho xe container vào. Hai mươi cây vàng. Lúc đó tôi không có lựa chọn — hàng đang chờ."
> 
> *— Lê Thị Huých, Củ Chi, 01/04/2026*

*Translation sub:* *(In 2005, husband just passed. Borrowed and paid 100M VND — 20 taels of gold — to widen the road so export containers could reach the workshop. No choice. Goods were waiting.)*

*h3:* Tráng xi măng — dấu ấn của người thợ bậc thầy

*Paragraph:*  
Đan nan là kỹ năng ai cũng học được sau vài tháng. Tráng xi măng bên trong sản phẩm — lớp lót giữ hình dáng, chống thấm, làm cho vật liệu sống lâu — là thứ mất hàng chục năm mới thành thạo. Bà mô tả nó bằng hai chữ: liền và đẹp. Không có chữ thứ ba.

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

- Trúc tre địa phương bị phá hết để làm đường (*"họ phá hết... họ làm đường làm xá"*)
- Phải mua từ tận miền Tây, vận chuyển xa hàng trăm km
- Không có nhà cung cấp ổn định — phụ thuộc vào thương lái đi thu gom

*Environmental dependencies:*  
Phụ thuộc: nắng (phơi khô 60–70%)  
Rủi ro: mùa mưa → mốc trên trúc đã xử lý

*Waste profile:*  
Phế liệu tre: đốt | Nhựa: xe rác đô thị thu gom | Xi măng thừa: đổ bỏ tại chỗ

---

**ECONOMIC PORTRAIT**

*Sentiment word:* **Bấp bênh**  
*Sentiment color:* `#c49a30` (amber)  
*Sentiment quote:*
> "Làm nghề này cực lắm... muốn nghỉ làm nhưng ráng duy trì."

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

---

**SUCCESSION STATUS**

*Code 3 — Thế hệ cuối*

> *"Con gái không theo nghề. Người trẻ đi học hết. Tôi làm bao lâu còn sức thì làm."*
> 
> *— Lê Thị Huých*

*Subtext:* Các con và cháu bà đã tốt nghiệp đại học, làm hiệu trưởng và thạc sĩ. Bà không oán giận điều đó — bà tự hào. Nhưng khi bà dừng, kỹ thuật dừng cùng.

*Soft CTA:* Bạn muốn học nghề đan lát truyền thống? → [Liên hệ qua mapme]

---

### SAMPLE B — Nắng Ceramics · Huỳnh Xuân Huỳnh

**Accent color:** `#c4623a` (terracotta)  
**Succession badge:** `#6b9a3a` — "Đang truyền nghề"

---

**HERO**

*Craft pill:* Gốm Lái Thiêu  
*Location:* Lái Thiêu · Bình Dương · Đồng bằng sông Cửu Long

*h1:*
> Huỳnh Xuân Huỳnh  
> *"Một nét vẽ tạo nên hình dáng"*

*Dek:*  
Năm 29 tuổi, Huỳnh dùng toàn bộ tiết kiệm của mình để đặt 500 chiếc chén đầu tiên. Hôm nay, Nắng Ceramics là một trong số ít thương hiệu đang khôi phục gốm Lái Thiêu — loại gốm từng định hình cái đẹp của Nam Bộ suốt một thế kỷ.

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
*Signature quote (Fraunces italic):*
> "Nó là một nét vẽ tạo nên một cái hình dáng... hỏi cái sự dứt khoát của người thợ."

*Source line:* Ghi âm ngày 01/04/2026 · Phiên A005 · Phiên dịch: mapme

*Buttons:* [Nhắn tin] [Xem sản phẩm] [Tải dữ liệu]

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

---

**SUCCESSION STATUS**

*Code 1 — Đang truyền nghề*

> *"Nắng Ceramics hỗ trợ truyền nghề cho các bạn sinh viên — sinh viên có thể trở thành nhân viên, hay mở thương hiệu riêng. Mình muốn chia sẻ kỹ thuật, không giữ cho riêng mình."*
> 
> *— Huỳnh Xuân Huỳnh*

*Subtext:* Tại 29 tuổi, Huỳnh vừa là nghệ nhân trẻ nhất trong mẫu vừa là người duy nhất chủ động xây dựng tương lai cho nghề. Mô hình của anh — truyền nghề như dự án cộng đồng, không phải di sản gia đình — là điểm khác biệt quan trọng nhất trong cả chuyến thực địa.

