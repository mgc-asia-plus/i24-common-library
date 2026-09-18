# Tasks — ui-components

## Summary
- **Total Tasks**: 7 across 5 phases
- **Execution Waves**: 5 waves (1 parallel)
- **Strategy**: ตาม design component · เขียนก่อน แล้ว review checklist
- **Testing**: review properties (ไม่มี unit/e2e/load runner)
- **Derived from**: `units/ui-components/design.md` + D4 recommendations

## Overview
แตกงานตาม SpecIndex → กลุ่ม SpecLibrary (ขนานได้) → PreviewGallery จากนั้นตรวจ 4 properties แล้วค่อย CHANGELOG

**Legend**: `- [ ]` ยังไม่ทำ · `- [x]` เสร็จแล้ว

---

## Task Phases

- [x] 1. SpecIndex
  - [x] 1.1 ล็อกดัชนี + กฎร่วมใน README
    - **Deps**: — | **Ref**: design.md — SpecIndex, Data Model (CatalogEntry)
    - ยืนยัน `docs/components/README.md`: ตาราง 14 component; เทมเพลต 8 หัวข้อ; footer "Powered by i24" บังคับ; ชี้ `design-tokens.md` / `effects.md`; ห้าม hex ล้วน
    - Document contract: Read catalog

- [x] 2. SpecLibrary (ขนานได้)
  - [x] 2.1 Basic + form specs
    - **Deps**: 1.1 | **Ref**: design.md — SpecLibrary, Data Model (ComponentSpec, Variant, InteractionState, TokenRef, A11yRule)
    - ไฟล์: `button.md`, `badge.md`, `card.md`, `input.md`, `alert.md`, `theme-mode.md`
    - ครบ 8 หัวข้อ; States อย่างน้อย default + focus + disabled เมื่อเป็น control; Tokens used อ้างชื่อจาก `docs/brand/`; snippet HTML สั้น; a11y focus/keyboard/40×40
    - Document contract: Read spec
  - [x] 2.2 Navigation + layout specs
    - **Deps**: 1.1 | **Ref**: design.md — SpecLibrary, shell classes
    - ไฟล์: `table.md`, `nav-header.md`, `sidebar.md`, `footer.md`
    - ล็อก `.mac-table` / `.mac-table-wrap` / `.mac-section` และ `.mac-sidebar` (พื้น `color-sidebar-bg` ไม่สลับ theme); footer บังคับทุก UI
    - Document contract: Read spec
  - [x] 2.3 Complex specs
    - **Deps**: 1.1 | **Ref**: design.md — SpecLibrary
    - ไฟล์: `modal.md`, `select.md`, `toast.md`, `pagination.md`
    - ครบ 8 หัวข้อ; hex ต้องมีชื่อ token คู่กัน; snippet ไม่เป็น template เต็มต่อ stack
    - Document contract: Read spec

- [x] 3. PreviewGallery
  - [x] 3.1 จัด `prototype/index.html` ให้ตรง spec
    - **Deps**: 2.1, 2.2, 2.3 | **Ref**: design.md — PreviewGallery, Data Model (PreviewPage)
    - gallery มี `[data-theme]`; `.mac-sidebar` / `.mac-table`; footer "Powered by i24"; คลาสตรง spec
    - Document contract: View preview

- [x] 4. Correctness review
  - [x] 4.1 Review 4 properties
    - **Deps**: 3.1 | **Ref**: design.md — Correctness, Testing Strategy
    - SpecSectionComplete · NoOrphanHex · PrototypeClassMatch · FooterPresent
    - ไม่เพิ่มสคริปต์/CI

- [x] 5. Operations
  - [x] 5.1 บันทึก CHANGELOG
    - **Deps**: 4.1 | **Ref**: design.md — Operations, Integration Points
    - `CHANGELOG.md` ระบุแคตตาล็อก 14 spec, `.mac-sidebar` / `.mac-table`, footer บังคับ, gallery
    - ไม่เขียน stack guide (ของ `delivery-guides`)

---

## Task Summary

| ID | Title | Deps | Status |
|----|-------|------|--------|
| 1.1 | SpecIndex README | — | Complete |
| 2.1 | Basic + form specs | 1.1 | Complete |
| 2.2 | Navigation + layout specs | 1.1 | Complete |
| 2.3 | Complex specs | 1.1 | Complete |
| 3.1 | Preview gallery | 2.1, 2.2, 2.3 | Complete |
| 4.1 | Review properties | 3.1 | Complete |
| 5.1 | CHANGELOG | 4.1 | Complete |

## Requirements Coverage

| Requirement | Tasks | Status |
|-------------|-------|--------|
| F-components | 1.1, 2.1, 2.2, 2.3, 4.1 | Complete |
| F-prototype | 3.1, 4.1 | Complete |

**Coverage**: 2/2

## Design Coverage

| Element | Type | Tasks |
|---------|------|-------|
| SpecIndex | component | 1.1 |
| SpecLibrary | component | 2.1, 2.2, 2.3 |
| PreviewGallery | component | 3.1 |
| CatalogEntry | entity | 1.1 |
| ComponentSpec, Variant, InteractionState, TokenRef, A11yRule | entity | 2.1, 2.2, 2.3 |
| PreviewPage | entity | 3.1 |
| Read catalog | contract | 1.1 |
| Read spec | contract | 2.1, 2.2, 2.3 |
| View preview | contract | 3.1 |
| brand-theme (token names) | integration | 2.1, 2.2, 2.3, 4.1 |
| delivery-guides | integration | ข้าม — unit อื่น |
| CHANGELOG | operations | 5.1 |

## Testing Coverage

- **unit_test_tasks**: ไม่มี test runner — ใช้ 4.1 แทนทุก component
- **integration_test_tasks**: 4.1 ตรวจ document contracts + NoOrphanHex + PrototypeClassMatch
- **e2e_test_tasks**: Skipped (D3 ไม่เลือก E2E)
- **load_test_tasks**: Skipped
- **pbt_tasks**: 4.1 (SpecSectionComplete, NoOrphanHex, PrototypeClassMatch, FooterPresent)
- **coverage_summary**: 3/3 components มี review task; 3/3 contracts มี impl + review

## Definition of Done
- [x] README ครบ 14 แถว + เทมเพลต 8 หัวข้อ + footer บังคับ
- [x] 14 spec ครบหัวข้อ / TokenRef / a11y
- [x] prototype มี `.mac-sidebar` / `.mac-table` / `[data-theme]` / footer
- [x] 4 properties ผ่านตอน review
- [x] CHANGELOG อัปเดต
- [x] F-components / F-prototype ครบ

## Execution Waves

| Wave | Phases | Parallel | Resolved deps |
|------|--------|----------|---------------|
| 1 | 1 SpecIndex | no | — |
| 2 | 2 SpecLibrary | **yes** (2.1 ∥ 2.2 ∥ 2.3) | 1.1 |
| 3 | 3 Preview | no | 2.1, 2.2, 2.3 |
| 4 | 4 Review | no | 3.1 |
| 5 | 5 CHANGELOG | no | 4.1 |

**File ownership**
| Wave | Task | Files |
|------|------|-------|
| 1 | 1.1 | `docs/components/README.md` |
| 2 | 2.1 | `docs/components/{button,badge,card,input,alert,theme-mode}.md` |
| 2 | 2.2 | `docs/components/{table,nav-header,sidebar,footer}.md` |
| 2 | 2.3 | `docs/components/{modal,select,toast,pagination}.md` |
| 3 | 3.1 | `prototype/index.html` |
| 4 | 4.1 | อ่าน `docs/components/*` + `prototype/index.html` — แก้เฉพาะจุดที่ property ไม่ผ่าน |
| 5 | 5.1 | `CHANGELOG.md` |

ไม่มีไฟล์ซ้อนใน wave ขนาน

## Notes
- ไฟล์ spec และ prototype มีอยู่แล้ว — implement ตรวจความครบแล้วปะช่องว่าง ไม่เขียนแคตตาล็อกใหม่ถ้าผ่าน review
- ไม่เขียน `docs/stacks/` หรือ conventions ใน unit นี้ (ของ `delivery-guides`)
- Technical debt นอกขอบเขต: `context.md` / manifest `colorSoT` ยังอ้างโลโก้แดง `#EC2129`
