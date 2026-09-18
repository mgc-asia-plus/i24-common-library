# Units of Work

## Summary
- **Units**: 3 units — `brand-theme` (foundation), `ui-components`, `delivery-guides`
- **Strategy**: Domain-Driven
- **Architecture**: Modular Monolith (repo เอกสารเดียว แยกโมดูลตามหมวด)
- **Story Distribution**: brand-theme: 4 (F-brand, F-tokens, F-theme, F-effects); ui-components: 2 (F-components, F-prototype); delivery-guides: 3 (F-stacks, F-conventions, F-scaffolding)
- **Key Dependencies**: brand-theme → ui-components (Data); brand-theme → delivery-guides (Data); ui-components → delivery-guides (API/docs)
- **Development Sequence**: Phase 1: brand-theme → Phase 2: ui-components → Phase 3: delivery-guides

## Overview
Feature ถูกแยกเป็น 3 units ตามโดเมนเอกสาร เพื่อ ownership ชัดและส่งมอบเป็นชุดที่ทีมอื่นนำไปใช้ได้ โดยยังอยู่ใน repo เดียว (Modular Monolith)

**Strategy**: Domain-Driven
**Rationale**: ค่าสี/token เป็น SSOT ที่ต้องนิ่งก่อน; component spec อ้าง token; stack/convention/scaffolding อธิบายวิธีนำไปใช้ — เปลี่ยน token ไม่ควรบังคับแก้ขอบเขต component ทั้งหมดใน unit เดียวกัน

> หมายเหตุ: ไม่มี `requirements.md` — ใช้ Key Features (F-*) จาก D1/product เป็น stories

---

## Unit 1: brand-theme (Foundation)

**Purpose**: เป็น SSOT ของอัตลักษณ์ภาพ — palette จากโลโก้, design tokens (รวม semantic light/dark), วิธี map ไป theme, และ effects (gradient/glass) ให้ทุก unit อ้างอิงที่เดียว
**Priority**: High
**Complexity**: Medium
**Stories**: 4 stories — F-brand, F-tokens, F-theme, F-effects
**Type**: Foundation (domain) — มี stories; ไม่ใช่ infra-only แยกชุด

### Responsibilities
- Lock ค่าสีแบรนด์และกฎ usage / do-don't
- นิยาม design tokens + semantic tokens (light/dark)
- อธิบายการ map tokens → theme (ไม่ล็อก stack ในเฟสนี้)
- นิยาม effects tokens และข้อจำกัด a11y
- เป็นผู้เดียวที่มีสิทธิ์เปลี่ยนค่า token — unit อื่นอ้างอิง ห้ามสำเนาค่า

### Commands
| Command | Description | Actor |
|---------|-------------|-------|
| PublishPalette | ยืนยัน/ปล่อยชุดสีจากโลโก้เป็นมาตรฐาน | Maintainer |
| DefineToken | เพิ่มหรือแก้ design/semantic token | Maintainer |
| PublishThemeMapping | ปล่อยวิธี map token → theme | Maintainer |
| PublishEffects | ปล่อยสูตร gradient/glass และข้อจำกัด | Maintainer |

### Domain Model
**Aggregates**: BrandSystem (root: Palette)
**Entities**: Palette, TokenSet, ThemeMapping, EffectRecipe
**Value Objects**: HexColor, TokenName, ContrastRatio, ThemeMode (light/dark)

### Domain Events
**Publishes**: PaletteLocked — เมื่อค่าสีหลักถูกยืนยัน; TokensPublished — เมื่อชุด token พร้อมให้ unit อื่นอ้าง; ThemeMappingPublished — เมื่อสูตร map theme พร้อมใช้
**Subscribes**: (none) — foundation ไม่มี upstream

### Dependencies
| Depends On | Type | Description |
|------------|------|-------------|
| (none) | — | Foundation ไม่มี upstream |

---

## Unit 2: ui-components

**Purpose**: spec ของ UI components (anatomy, variants, states, a11y) และหน้า preview ที่แสดง token + component ตามมาตรฐานภาพจาก `brand-theme`
**Priority**: High
**Complexity**: Medium
**Stories**: 2 stories — F-components, F-prototype

### Commands
| Command | Description | Actor |
|---------|-------------|-------|
| PublishComponentSpec | ปล่อย/อัปเดต spec ของ component หนึ่งตัว | Maintainer |
| AddComponentVariant | เพิ่ม variant/state โดยอ้าง token ที่มีอยู่ | Maintainer |
| PublishPreview | อัปเดตหน้า preview ให้ตรง spec + token ปัจจุบัน | Maintainer |

### Domain Model
**Aggregates**: ComponentCatalog (root: ComponentSpec)
**Entities**: ComponentSpec, PreviewPage
**Value Objects**: Anatomy, Variant, InteractionState, A11yRule, TokenRef

### Domain Events
**Publishes**: ComponentSpecReleased — spec พร้อมให้ stack guide อ้าง; PreviewUpdated — gallery สะท้อน token/spec ล่าสุด
**Subscribes**: TokensPublished, ThemeMappingPublished จาก `brand-theme` — ปรับ TokenRef / preview ให้ตรง SSOT

### Dependencies
| Depends On | Type | Description |
|------------|------|-------------|
| brand-theme | Data | อ้างชื่อ token, สี, semantic light/dark, effects — ห้ามใส่ hex ซ้ำใน spec |

---

## Unit 3: delivery-guides

**Purpose**: แนวทางนำไปใช้จริง — stack setup guides, coding conventions, และ scaffolding checklist ให้ทีมเริ่มโปรเจกต์ใหม่ยึดมาตรฐานเดียวกัน
**Priority**: Medium
**Complexity**: Medium
**Stories**: 3 stories — F-stacks, F-conventions, F-scaffolding

### Commands
| Command | Description | Actor |
|---------|-------------|-------|
| PublishStackGuide | ปล่อย/อัปเดตแนวทาง setup ต่อ stack | Maintainer |
| PublishConvention | ปล่อยกฎ naming / structure / git / JSON API | Maintainer |
| PublishScaffolding | ปล่อย checklist เริ่มโปรเจกต์ใหม่ | Maintainer / Team lead |

### Domain Model
**Aggregates**: DeliveryKit (root: StackGuide)
**Entities**: StackGuide, ConventionSet, ScaffoldingChecklist
**Value Objects**: StackName, ChecklistStep, NamingRule, JsonEnvelope

### Domain Events
**Publishes**: StackGuideReleased — ทีมเริ่มโปรเจกต์ตาม guide ได้; ScaffoldingPublished — checklist พร้อมใช้
**Subscribes**: TokensPublished จาก `brand-theme`; ComponentSpecReleased จาก `ui-components` — อัปเดตตัวอย่าง/ขั้นตอนให้ชี้กลับ SSOT

### Dependencies
| Depends On | Type | Description |
|------------|------|-------------|
| brand-theme | Data | วิธีต่อ theme/tokens ในแต่ละ stack — อ้าง token ไม่คัดลอกค่า |
| ui-components | API | อ้าง component spec (รวม footer บังคับ) ใน checklist และตัวอย่าง stack |

---

## Context Map

| Upstream | Downstream | Pattern |
|----------|------------|---------|
| brand-theme | ui-components | Customer/Supplier |
| brand-theme | delivery-guides | Customer/Supplier |
| ui-components | delivery-guides | Customer/Supplier |

**Patterns**: Customer/Supplier ทางเดียว — downstream ต้อง conform ชื่อ token/spec ของ upstream; ไม่มีวงวน; ไม่มี Shared Kernel สำเนาค่า

---

## Development Sequence

### Phase 1: Foundation
- [ ] Unit 1: brand-theme — lock SSOT สี/token/theme/effects ก่อน unit อื่นอ้างอิง

### Phase 2: Core
- [ ] Unit 2: ui-components — spec + preview ยึด token จาก Phase 1

### Phase 3: Supporting
- [ ] Unit 3: delivery-guides — stack/convention/scaffolding ชี้กลับ token + component spec
