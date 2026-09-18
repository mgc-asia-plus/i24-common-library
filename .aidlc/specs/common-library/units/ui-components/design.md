# Design — ui-components

## Summary
- **Architecture**: Modular Monolith — โมดูล `docs/components/` + `prototype/index.html` เป็นแคตตาล็อก UI ของ repo เอกสาร
- **Stack**: Markdown specs / static HTML preview / Tailwind CSS 4.3.3 (อ้างจาก foundation) / `[data-theme]` / ไม่มี DB / ไม่มี package ที่ publish
- **Components**: 3 (SpecIndex, SpecLibrary, PreviewGallery)
- **Entities**: 7 (ComponentSpec, CatalogEntry, Variant, InteractionState, TokenRef, A11yRule, PreviewPage)
- **Endpoints**: 3 document contracts (ไม่มี HTTP API)
- **Integrations**: 1 upstream (`brand-theme`) + 1 downstream (`delivery-guides`)
- **Operations**: Minimal (CHANGELOG + PR)
- **PBT Properties**: 4 (ตรวจตอน review ไม่ใช้ไลบรารี)
- **Testing Strategy**: Included (review checklist)
- **NFR**: WCAG 2.1 AA ของ component (focus / keyboard / touch / aria)

## Architecture

**Pattern**: Modular Monolith (D2) + domain module `ui-components`  
**Rationale**: spec และ preview ต้องเป็นเจ้าของเดียวกัน; อ้าง token จาก `brand-theme` ห้ามสำเนา hex; `delivery-guides` อ้าง spec ไม่คัดลอก anatomy

```
        ┌─────────────────────────┐
        │  brand-theme (SSOT)     │
        │  ชื่อ token / effects    │
        └───────────┬─────────────┘
                    │ Data (token names)
                    ▼
        ┌─────────────────────────┐
        │  ui-components          │
        │  docs/components/*      │
        │  prototype/index.html   │
        └───────────┬─────────────┘
                    │ spec + class names
                    ▼
        ┌─────────────────────────┐
        │  delivery-guides        │
        └─────────────────────────┘
```

**กติกาขอบเขต**
- อ้างชื่อ semantic token และสูตรใน `effects.md` — ห้ามคิด blur/opacity เอง
- hex ใน snippet ได้เฉพาะเมื่อระบุชื่อ token คู่กัน (เช่น `color-primary` / `#0F172A`)
- ล็อกคลาส `.mac-sidebar` / `.mac-table` / `.mac-table-wrap` / `.mac-section`
- Footer "Powered by i24" บังคับทุกระบบที่มี UI
- Snippet สั้น ไม่ใช่ template ครบชุดต่อ stack
- ปล่อยมาตรฐาน = merge เข้า `main`

## Components

### SpecIndex
- **Purpose**: ดัชนีแคตตาล็อก + กฎร่วม (token, focus, touch, glass/gradient)
- **Technology**: Markdown (`docs/components/README.md`)
- **Responsibilities**: รายการ 14 component; เทมเพลต 8 หัวข้อ; มาตรฐาน footer บังคับ; ชี้ `design-tokens.md` / `effects.md`
- **Exposes**: รายชื่อ ComponentSpec + กฎร่วม
- **Consumes**: brand-theme (token names)

### SpecLibrary
- **Purpose**: spec รายตัวตามเทมเพลตเดียวกัน
- **Technology**: Markdown หนึ่งไฟล์ต่อ component ใน `docs/components/`
- **Responsibilities**: ครอบคลุม 14 ไฟล์ — button, badge, card, input, table, nav-header, sidebar, alert, theme-mode, footer, modal, select, toast, pagination; แต่ละไฟล์มี Purpose / Anatomy / Variants / Sizes / States / Tokens used / Accessibility / Reference snippet
- **Exposes**: ComponentSpec (anatomy, variants, states, TokenRef, A11yRule)
- **Consumes**: SpecIndex (เทมเพลต), brand-theme (tokens + effects)

### PreviewGallery
- **Purpose**: หน้าเดียวให้เห็น token + component ตาม spec
- **Technology**: Static HTML (`prototype/index.html`)
- **Responsibilities**: gallery ของแคตตาล็อก; `[data-theme]` สลับโหมด; แสดง `.mac-sidebar` / `.mac-table`; มี footer "Powered by i24"; คลาสตรง spec
- **Exposes**: PreviewPage
- **Consumes**: SpecLibrary (class/anatomy), brand-theme (สี/token/effects)

## Data Model

| Entity | Fields | Constraints | Relationships |
|--------|--------|-------------|----------------|
| CatalogEntry | name, file, kind (basic/layout/form/data/navigation/feedback/utility/complex), summary | name unique; ต้องมีไฟล์ spec | 1 CatalogEntry → 1 ComponentSpec |
| ComponentSpec | name, purpose, anatomy, sizes | ครบ 8 หัวข้อเทมเพลต | 1 spec → N Variant, N InteractionState, N TokenRef, N A11yRule |
| Variant | name, when_to_use, visual | ชื่อไม่ซ้ำใน spec | N:1 ComponentSpec |
| InteractionState | name (`default`\|`hover`\|`focus`\|`active`\|`disabled`\|`loading` …) | อย่างน้อย default + focus + disabled สำหรับ control ที่โต้ตอบได้ | N:1 ComponentSpec |
| TokenRef | token_name, role | ต้องเป็นชื่อที่มีใน `design-tokens.md` | N:1 ComponentSpec |
| A11yRule | role, keyboard, aria, touch_min | touch ≥ 40×40 สำหรับ control; ต้องมี focus ที่มองเห็น | N:1 ComponentSpec |
| PreviewPage | path, theme_attr, sections | path คงที่ `prototype/index.html`; ต้องมี footer | อ้าง CatalogEntry ทุกตัวที่แสดง |

**Indexes (logical)**: `CatalogEntry.name`, `ComponentSpec.name` — unique

**แคตตาล็อกที่ล็อก (14)**

| Spec | ไฟล์ | หมายเหตุ |
|------|------|----------|
| Button | `button.md` | primary Navy Solid |
| Badge | `badge.md` | Pill |
| Card | `card.md` | glass |
| Input | `input.md` | form |
| Table | `table.md` | `.mac-table` ใน `.mac-table-wrap` / `.mac-section` |
| Nav / Header | `nav-header.md` | |
| Sidebar | `sidebar.md` | `.mac-sidebar` พื้น `color-sidebar-bg` ไม่สลับ theme |
| Alert | `alert.md` | |
| Theme mode | `theme-mode.md` | `[data-theme]` |
| Footer | `footer.md` | บังคับทุก UI |
| Modal | `modal.md` | |
| Select | `select.md` | |
| Toast | `toast.md` | |
| Pagination | `pagination.md` | |

## API Specification

ไม่มี HTTP API. สัญญาที่ downstream ใช้คือ **document contracts**:

| Contract | Path | Auth | Request | Response | Errors |
|----------|------|------|---------|----------|--------|
| Read catalog | `docs/components/README.md` | git read | — | รายการ + กฎร่วม + footer mandate | ขาด component ในตาราง = ผิดสัญญา |
| Read spec | `docs/components/{name}.md` | git read | — | 8 หัวข้อ + TokenRef | ไม่ครบหัวข้อ / hex โดยไม่มีชื่อ token = ผิดสัญญา |
| View preview | `prototype/index.html` | เปิดไฟล์ / static server | — | gallery + theme toggle | คลาสไม่ตรง spec / ไม่มี footer = ผิดสัญญา |

**Conventions**
- Versioning: git + `CHANGELOG.md`
- Pagination / rate limit: ไม่มี
- Publish: merge `main` = ปล่อย (D3-12)
- Snippet: HTML สั้น; ใส่ชื่อคลาส React/Tailwind ได้; ห้ามเป็น template ครบชุดต่อ Go/Next/Nest/Express

## Integration Points

| System | Protocol | Purpose | Error handling |
|--------|----------|---------|----------------|
| `brand-theme` | Data (token names) | TokenRef + สูตร effects | ถ้าเจอ hex ล้วนใน spec → ใส่ชื่อ token หรือชี้ `docs/brand/` |
| `delivery-guides` | Docs | stack guide / scaffolding อ้าง spec (รวม footer บังคับ) | ห้ามสำเนา anatomy ยาว — ลิงก์กลับ `docs/components/` |

## Implementation

**Directory**
```
docs/components/
  README.md
  button.md
  badge.md
  card.md
  input.md
  table.md
  nav-header.md
  sidebar.md
  alert.md
  theme-mode.md
  footer.md
  modal.md
  select.md
  toast.md
  pagination.md
prototype/index.html
CHANGELOG.md
```

**Dev setup**: เปิด Markdown + เปิด `prototype/index.html` (หรือ static server) — ไม่มี package manager / build (ยึด foundation D3-8)

**Conventions**
- เทมเพลต 8 หัวข้อทุก spec
- สี = semantic token; effects = `effects.md`
- Shell: `.mac-sidebar` / `.mac-table` / `.mac-table-wrap` / `.mac-section`
- งานค้างของ unit นี้: ให้ 14 spec + README + prototype สอดคล้องเทมเพลต / token / คลาส / footer / a11y — ไฟล์ส่วนใหญ่มีอยู่แล้ว ตรวจแล้วปะช่องว่าง ไม่เขียนแคตตาล็อกใหม่

## Testing Strategy

- **Pyramid**: ไม่มี unit/e2e runtime — ชั้นเดียวคือ **review properties** ตอน PR
- **Frameworks**: ไม่มี test runner (D3-8 ไม่เลือกสคริปต์/CI)
- **Coverage**: ทุก spec มี Tokens used + States; prototype แสดงคลาสที่ spec ล็อก; gallery มี footer
- **Mock**: ไม่มี
- **Test data**: ไฟล์ spec + `prototype/index.html` คือข้อมูลจริง
- **Run**: checklist ใน PR (ดู Correctness)

## NFR

- **Accessibility**: WCAG 2.1 AA — `color-focus-ring` ที่มองเห็น, keyboard, แตะขั้นต่ำ 40×40px, role/aria ในแต่ละ spec; contrast ของสียึด foundation
- **Performance / security runtime**: ไม่มี — ไม่ใช่ service
- **Maintainability**: แก้ spec ที่ `docs/components/` ที่เดียว; prototype ต้องตาม

## Operations

**Level**: Minimal

| Signal | ที่ไหน | เมื่อไหร่ |
|--------|--------|-----------|
| Logging | `CHANGELOG.md` + git history | ทุกการเปลี่ยน spec / prototype / กฎร่วม |
| Error tracking | commit message / PR description | เมื่อพบ hex ล้วน, spec ไม่ครบหัวข้อ, prototype คลาด spec |
| Health | ไม่มี endpoint | ความพร้อม = README ครบ 14 แถว + preview เปิดได้ + มี footer |
| Lifecycle | merge `main` | ไม่มี graceful shutdown |
| Config/secrets | ไม่มี | — |

## Correctness

| Property | Description | Validates |
|----------|-------------|-----------|
| SpecSectionComplete | ทุก spec มี Tokens used และ States (อย่างน้อย default + focus + disabled เมื่อเป็น control) | SpecLibrary |
| NoOrphanHex | hex แบรนด์ใน spec/prototype ต้องมีชื่อ token คู่กัน | TokenRef / foundation downstream rule |
| PrototypeClassMatch | คลาสที่ spec ล็อก (รวม `.mac-sidebar` / `.mac-table`) ปรากฏใน preview | PreviewGallery |
| FooterPresent | gallery และกฎร่วมระบุ footer "Powered by i24" | SpecIndex, PreviewGallery |

## Traceability

| Requirement | Component(s) | Endpoint(s) | Entity | Status |
|-------------|--------------|-------------|--------|--------|
| F-components | SpecIndex, SpecLibrary | Read catalog, Read spec | ComponentSpec, CatalogEntry, Variant, InteractionState, TokenRef, A11yRule | Covered |
| F-prototype | PreviewGallery | View preview | PreviewPage | Covered |

**Coverage**: 2/2 — ไม่มี gap

**Components without requirement**: ไม่มี

## External References

| Source | Type | Used in |
|--------|------|---------|
| `docs/components/README.md` | แคตตาล็อกปัจจุบัน | SpecIndex |
| `docs/brand/design-tokens.md` | Token SSOT (foundation) | TokenRef |
| `docs/brand/effects.md` | Effect recipes (foundation) | SpecLibrary / PreviewGallery |
| `prototype/index.html` | Live gallery | PreviewGallery |
| WCAG 2.1 | A11y spec | A11yRule |
| Tailwind CSS 4.3.3 | Version pin (foundation) | snippet / preview theme |
