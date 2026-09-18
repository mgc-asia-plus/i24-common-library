# Tasks — brand-theme

## Summary
- **Total Tasks**: 7 across 5 phases
- **Execution Waves**: 5 waves (1 parallel)
- **Strategy**: ตามไฟล์ SSOT · เขียนก่อน แล้ว review checklist
- **Testing**: review properties (ไม่มี unit/e2e/load runner)
- **Derived from**: `units/brand-theme/design.md` + D4 recommendations + design edit (Navy `#0F172A`, sidebar/table tokens)

## Overview
แตกงานตามไฟล์ใน `docs/brand/` ตามลำดับ Palette → Tokens แล้วขนาน Theme กับ Effects จากนั้นตรวจ 4 properties แล้วค่อย sync blueprint

**Legend**: `- [ ]` ยังไม่ทำ · `- [x]` เสร็จแล้ว

---

## Task Phases

- [x] 1. Palette SSOT
  - [x] 1.1 Lock palette Navy `#0F172A` + sidebar + table colors
    - **Deps**: — | **Ref**: design.md — PaletteSSOT, Data Model (Palette, ContrastPair)
    - ยืนยัน `docs/brand/palette.md`: primary `#0F172A`, canvas `#F5F5F7`, sidebar tokens (พื้นไม่สลับ theme), Cool Slate, row-hover gradient, contrast AA ของขาวบน Navy
    - Document contract: Read palette

- [x] 2. Token registry
  - [x] 2.1 นิยาม Primitive → Semantic รวม sidebar / table / radius
    - **Deps**: 1.1 | **Ref**: design.md — TokenRegistry, Data Model (PrimitiveToken, SemanticToken, ThemeModeBinding)
    - `docs/brand/design-tokens.md`: ชื่อไม่ซ้ำ; semantic มี light/dark (sidebar-bg ค่าเดียวทั้งสองโหมด); `radius-table` 14px, `radius-card` 20px, `radius-sidebar-item` 6px, `sidebar-width` 260px
    - Document contract: Read tokens

- [x] 3. Theme mapping + Effects (ขนานได้)
  - [x] 3.1 Map tokens → Tailwind v4 `@theme` + `[data-theme]`
    - **Deps**: 2.1 | **Ref**: design.md — ThemeMappingGuide
    - `docs/brand/theme-tailwind.md`: pin `tailwindcss@4.3.3`; `--i24-primary: #0F172A`; snippet สั้น ไม่เป็น template เต็ม
    - Document contract: Read theme map
  - [x] 3.2 อัปเดตสูตร effects / ปุ่ม Navy
    - **Deps**: 2.1 | **Ref**: design.md — EffectsSSOT
    - `docs/brand/effects.md`: ปุ่ม primary ใช้ `#0F172A`; glass navy `rgba(15,23,42,…)`; component อ้างสูตร ห้ามคิด blur เอง
    - Document contract: Read effects

- [x] 4. Correctness review
  - [x] 4.1 Review 4 properties + ตัด hex leak
    - **Deps**: 3.1, 3.2 | **Ref**: design.md — Correctness, Testing Strategy
    - UniqueTokenNames · SemanticPairComplete · ContrastAA · NoHexLeak
    - ไล่ไฟล์นอก `docs/brand/` ที่ยัง hardcode `#0A2540` (เช่น snippet ใน button/modal/select/toast) ให้ชี้ token หรืออัปเป็น `#0F172A` ตาม SSOT
    - ไม่เพิ่มสคริปต์/CI

- [x] 5. Integrations + operations
  - [x] 5.1 Sync blueprints ให้ชี้ palette ปัจจุบัน
    - **Deps**: 4.1 | **Ref**: design.md — Integration Points
    - `.aidlc/blueprints/product.md` และ `resources.md` ตัดชุดโลโก้แดงเก่า ให้ชี้ `docs/brand/palette.md` (Navy `#0F172A`)
  - [x] 5.2 บันทึก CHANGELOG
    - **Deps**: 5.1 | **Ref**: design.md — Operations
    - `CHANGELOG.md` ระบุ Navy `#0F172A`, sidebar tokens, `.mac-sidebar` / `.mac-table`

---

## Task Summary

| ID | Title | Deps | Status |
|----|-------|------|--------|
| 1.1 | Lock palette | — | Complete |
| 2.1 | Token registry | 1.1 | Complete |
| 3.1 | Theme mapping | 2.1 | Complete |
| 3.2 | Effects recipes | 2.1 | Complete |
| 4.1 | Review properties | 3.1, 3.2 | Complete |
| 5.1 | Sync blueprints | 4.1 | Complete |
| 5.2 | CHANGELOG | 5.1 | Complete |

## Requirements Coverage

| Requirement | Tasks | Status |
|-------------|-------|--------|
| F-brand | 1.1, 4.1 | Complete |
| F-tokens | 2.1, 4.1 | Complete |
| F-theme | 3.1, 4.1 | Complete |
| F-effects | 3.2, 4.1 | Complete |

**Coverage**: 4/4

## Design Coverage

| Element | Type | Tasks |
|---------|------|-------|
| PaletteSSOT | component | 1.1 |
| TokenRegistry | component | 2.1 |
| ThemeMappingGuide | component | 3.1 |
| EffectsSSOT | component | 3.2 |
| Palette, ContrastPair | entity | 1.1 |
| PrimitiveToken, SemanticToken, ThemeModeBinding | entity | 2.1 |
| EffectRecipe | entity | 3.2 |
| Read palette | contract | 1.1 |
| Read tokens | contract | 2.1 |
| Read theme map | contract | 3.1 |
| Read effects | contract | 3.2 |
| ui-components / delivery-guides (token names) | integration | 2.1, 4.1 |
| blueprints sync | integration | 5.1 |
| CHANGELOG | operations | 5.2 |

## Testing Coverage

- **unit_test_tasks**: ไม่มี test runner — ใช้ 4.1 แทนทุก component
- **integration_test_tasks**: 4.1 ตรวจ document contracts + NoHexLeak
- **e2e_test_tasks**: Skipped (D3 ไม่เลือก E2E)
- **load_test_tasks**: Skipped
- **pbt_tasks**: 4.1 (UniqueTokenNames, SemanticPairComplete, ContrastAA, NoHexLeak)
- **coverage_summary**: 4/4 components มี review task; 4/4 contracts มี impl + review

## Definition of Done
- [x] 4 ไฟล์ `docs/brand/` สอดคล้อง Navy `#0F172A` + sidebar/table tokens
- [x] 4 properties ผ่านตอน review
- [x] blueprints ไม่ชี้ชุดโลโก้แดงเก่า
- [x] CHANGELOG อัปเดต
- [x] F-brand / F-tokens / F-theme / F-effects ครบ

## Execution Waves

| Wave | Phases | Parallel | Resolved deps |
|------|--------|----------|---------------|
| 1 | 1 Palette | no | — |
| 2 | 2 Tokens | no | 1.1 |
| 3 | 3 Theme + Effects | **yes** (3.1 ∥ 3.2) | 2.1 |
| 4 | 4 Review | no | 3.1, 3.2 |
| 5 | 5 Blueprints + CHANGELOG | no | 4.1 |

**File ownership**
| Wave | Task | Files |
|------|------|-------|
| 1 | 1.1 | `docs/brand/palette.md` |
| 2 | 2.1 | `docs/brand/design-tokens.md` |
| 3 | 3.1 | `docs/brand/theme-tailwind.md` |
| 3 | 3.2 | `docs/brand/effects.md` |
| 4 | 4.1 | อ่าน `docs/brand/*` + แก้ hex leak นอก brand (button/modal/select/toast ถ้ายัง `#0A2540`) |
| 5 | 5.1 | `.aidlc/blueprints/product.md`, `resources.md` |
| 5 | 5.2 | `CHANGELOG.md` |

ไม่มีไฟล์ซ้อนใน wave ขนาน

## Notes
- งานส่วนใหญ่ใน `docs/brand/` และ prototype ถูก sync ตอน design edit แล้ว — implement ตรวจความครบแล้วปิด checkbox ไม่ต้องเขียนซ้ำถ้าผ่าน review
- spec `.mac-sidebar` / `.mac-table` อยู่ที่ `docs/components/` (unit `ui-components`) แต่ token เป็นของ foundation นี้
- Technical debt: `context.md` และ `aidlc-manifest.yaml` `colorSoT` ยังอ้างโลโก้แดง `#EC2129` (นอกขอบเขต 5.1)
