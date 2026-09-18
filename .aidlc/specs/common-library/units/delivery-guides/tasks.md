# Tasks — delivery-guides

## Summary
- **Total Tasks**: 5 across 5 phases
- **Execution Waves**: 4 waves (1 parallel)
- **Strategy**: ตาม design component · เขียนก่อน แล้ว review checklist
- **Testing**: review properties (ไม่มี unit/e2e/load runner)
- **Derived from**: `units/delivery-guides/design.md` + D4 recommendations

## Overview
แตกงานตาม StackGuideSet ∥ ConventionSet แล้วค่อย ScaffoldingChecklist จากนั้นตรวจ 5 properties แล้ว CHANGELOG

**Legend**: `- [ ]` ยังไม่ทำ · `- [x]` เสร็จแล้ว

---

## Task Phases

- [x] 1. StackGuideSet
  - [x] 1.1 จัด 4 stack guides ให้ชี้ SSOT
    - **Deps**: — | **Ref**: design.md — StackGuideSet, Data Model (StackGuide, StackName)
    - ไฟล์: `docs/stacks/{go-monolith,nextjs,nestjs,expressjs}.md`
    - setup + วิธีต่อ theme/tokens + ลิงก์ `theme-tailwind.md` / components; snippet สั้น ไม่ใช่ template เต็ม
    - Go + Next (has_ui) กล่าวถึง footer "Powered by i24"
    - Document contract: Read stack guide

- [x] 2. ConventionSet (ขนานกับ 1.1 ได้)
  - [x] 2.1 ยืนยัน 4 ไฟล์ conventions
    - **Deps**: — | **Ref**: design.md — ConventionSet, JsonEnvelope
    - ไฟล์: `docs/conventions/{project-structure,naming,git,json-api}.md`
    - JSON envelope + `snake_case`; ไม่สำเนาตารางสี
    - Document contract: Read convention

- [x] 3. ScaffoldingChecklist
  - [x] 3.1 จัด checklist ต่อ 4 stack
    - **Deps**: 1.1, 2.1 | **Ref**: design.md — ScaffoldingChecklist, ChecklistStep
    - `docs/scaffolding.md`: ขั้นร่วม + ขั้นต่อ Go/Next/Nest/Express; ห้าม hex ล้วน; UI มี footer; ชี้ stacks/conventions/brand/components
    - Document contract: Read scaffolding

- [x] 4. Correctness review
  - [x] 4.1 Review 5 properties
    - **Deps**: 3.1 | **Ref**: design.md — Correctness, Testing Strategy
    - StackThemePointer · ConventionSetComplete · ScaffoldingPerStack · DeliveryNoOrphanHex · FooterStepForUI
    - ไม่เพิ่มสคริปต์/CI; ไม่แก้ `docs/brand/` หรือ `docs/components/`

- [x] 5. Operations
  - [x] 5.1 บันทึก CHANGELOG
    - **Deps**: 4.1 | **Ref**: design.md — Operations
    - `CHANGELOG.md` ระบุ 4 stack, 4 convention, scaffolding checklist, ไม่มี generator
    - ไม่เขียนไฟล์ stack/convention ซ้ำ

---

## Task Summary

| ID | Title | Deps | Status |
|----|-------|------|--------|
| 1.1 | Four stack guides | — | Complete |
| 2.1 | Four conventions | — | Complete |
| 3.1 | Scaffolding checklist | 1.1, 2.1 | Complete |
| 4.1 | Review properties | 3.1 | Complete |
| 5.1 | CHANGELOG | 4.1 | Complete |

## Requirements Coverage

| Requirement | Tasks | Status |
|-------------|-------|--------|
| F-stacks | 1.1, 4.1 | Covered |
| F-conventions | 2.1, 4.1 | Covered |
| F-scaffolding | 3.1, 4.1 | Covered |

**Coverage**: 3/3

## Design Coverage

| Element | Type | Tasks |
|---------|------|-------|
| StackGuideSet | component | 1.1 |
| ConventionSet | component | 2.1 |
| ScaffoldingChecklist | component | 3.1 |
| StackGuide, StackName | entity | 1.1 |
| ConventionDoc, NamingRule, JsonEnvelope | entity | 2.1 |
| ChecklistStep | entity | 3.1 |
| Read stack guide | contract | 1.1 |
| Read convention | contract | 2.1 |
| Read scaffolding | contract | 3.1 |
| brand-theme / ui-components (links) | integration | 1.1, 3.1, 4.1 |
| CHANGELOG | operations | 5.1 |

## Testing Coverage

- **unit_test_tasks**: ไม่มี test runner — ใช้ 4.1 แทนทุก component
- **integration_test_tasks**: 4.1 ตรวจ document contracts + DeliveryNoOrphanHex
- **e2e_test_tasks**: Skipped
- **load_test_tasks**: Skipped
- **pbt_tasks**: 4.1 (StackThemePointer, ConventionSetComplete, ScaffoldingPerStack, DeliveryNoOrphanHex, FooterStepForUI)
- **coverage_summary**: 3/3 components มี review task; 3/3 contracts มี impl + review

## Definition of Done
- [x] 4 stack guides ชี้ theme/spec และ UI กล่าวถึง footer
- [x] 4 ไฟล์ conventions ครบ รวม JSON envelope + `snake_case`
- [x] scaffolding มีขั้นทั้ง 4 stack + footer สำหรับ UI
- [x] 5 properties ผ่านตอน review
- [x] CHANGELOG อัปเดต
- [x] F-stacks / F-conventions / F-scaffolding ครบ

## Execution Waves

| Wave | Phases | Parallel | Resolved deps |
|------|--------|----------|---------------|
| 1 | 1 Stack + 2 Conventions | **yes** (1.1 ∥ 2.1) | — |
| 2 | 3 Scaffolding | no | 1.1, 2.1 |
| 3 | 4 Review | no | 3.1 |
| 4 | 5 CHANGELOG | no | 4.1 |

**File ownership**
| Wave | Task | Files |
|------|------|-------|
| 1 | 1.1 | `docs/stacks/{go-monolith,nextjs,nestjs,expressjs}.md` |
| 1 | 2.1 | `docs/conventions/{project-structure,naming,git,json-api}.md` |
| 2 | 3.1 | `docs/scaffolding.md` |
| 3 | 4.1 | อ่าน stacks + conventions + scaffolding — แก้เฉพาะจุดที่ property ไม่ผ่านใน 3 โฟลเดอร์นี้ |
| 4 | 5.1 | `CHANGELOG.md` |

ไม่มีไฟล์ซ้อนใน wave ขนาน

## Notes
- ไฟล์มีอยู่แล้ว — implement ตรวจความครบแล้วปะช่องว่าง ไม่เขียน guide ใหม่ทั้งชุดถ้าผ่าน review
- ไม่แก้ `docs/brand/` หรือ `docs/components/` ใน unit นี้
- ไม่สร้าง CLI generator
- Technical debt นอกขอบเขต: `context.md` / manifest `colorSoT` ยังอ้างโลโก้แดง `#EC2129`
