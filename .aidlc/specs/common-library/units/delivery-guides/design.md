# Design — delivery-guides

## Summary
- **Architecture**: Modular Monolith — โมดูลเอกสาร `docs/stacks/` + `docs/conventions/` + `docs/scaffolding.md`
- **Stack**: Markdown guides / Tailwind CSS 4.3.3 (อ้างจาก foundation) / ไม่มี generator / ไม่มี DB / ไม่มี runtime
- **Components**: 3 (StackGuideSet, ConventionSet, ScaffoldingChecklist)
- **Entities**: 6 (StackGuide, ConventionDoc, ChecklistStep, NamingRule, JsonEnvelope, StackName)
- **Endpoints**: 3 document contracts (ไม่มี HTTP API)
- **Integrations**: 2 upstream (`brand-theme`, `ui-components`)
- **Operations**: Minimal (CHANGELOG + PR)
- **PBT Properties**: 5 (ตรวจตอน review ไม่ใช้ไลบรารี)
- **Testing Strategy**: Included (review checklist)
- **NFR**: JSON `snake_case` + ยึด a11y/footer จาก upstream

## Architecture

**Pattern**: Modular Monolith (D2) + domain module `delivery-guides`  
**Rationale**: ทีมนำไปใช้จริงต้องมีเจ้าของชุดเดียวกัน; อ้าง SSOT ของสี/spec ไม่สำเนาค่า

```
  brand-theme          ui-components
  (token / theme)      (14 spec + footer)
           \              /
            \            /
             ▼          ▼
        ┌─────────────────────┐
        │  delivery-guides    │
        │  stacks / conv /    │
        │  scaffolding.md     │
        └─────────────────────┘
```

**กติกาขอบเขต**
- ลิงก์กลับ `docs/brand/` และ `docs/components/` — ห้ามสำเนาตารางสีหรือ anatomy
- snippet สั้นพออธิบาย setup — ไม่ใช่ skeleton โปรเจกต์เต็ม
- ไม่มี CLI generator
- stack ที่มี UI ต้องมีขั้น footer "Powered by i24"
- ปล่อยมาตรฐาน = merge เข้า `main`

## Components

### StackGuideSet
- **Purpose**: แนวทาง setup ต่อ stack + วิธีต่อ theme/tokens + ลิงก์ spec
- **Technology**: Markdown ใน `docs/stacks/`
- **Responsibilities**: รับรอง 4 stack — Go monolith (Chi+HTMX+Tailwind), Next.js, Nest.js, Express.js; แต่ละไฟล์ชี้ `theme-tailwind.md`; UI stack (Go, Next) กล่าวถึง footer และ component catalog
- **Exposes**: StackGuide ต่อ `StackName`
- **Consumes**: brand-theme, ui-components

### ConventionSet
- **Purpose**: กฎเขียนโค้ดร่วมทุก stack
- **Technology**: Markdown ใน `docs/conventions/`
- **Responsibilities**: 4 ไฟล์ — `project-structure.md`, `naming.md`, `git.md`, `json-api.md` (envelope + `snake_case`)
- **Exposes**: ConventionDoc, NamingRule, JsonEnvelope
- **Consumes**: ไม่มีค่าสี — อ้างโครงสร้างอย่างเดียว

### ScaffoldingChecklist
- **Purpose**: ขั้นตอนเริ่มโปรเจกต์ใหม่ด้วยมือ
- **Technology**: Markdown (`docs/scaffolding.md`)
- **Responsibilities**: ขั้นร่วมทุก stack + checklist แยก 4 stack; ห้าม hex ล้วน; UI ต้องมี footer; ชี้ stacks/ + conventions/ + brand/ + components/
- **Exposes**: ChecklistStep
- **Consumes**: StackGuideSet, ConventionSet, brand-theme, ui-components

## Data Model

| Entity | Fields | Constraints | Relationships |
|--------|--------|-------------|----------------|
| StackName | id (`go-monolith`\|`nextjs`\|`nestjs`\|`expressjs`) | ชุดล็อก 4 ค่า | 1:1 StackGuide |
| StackGuide | name, path, layer, has_ui, theme_pointer | ต้องมีลิงก์ `theme-tailwind.md` เมื่อ stack มี UI หรือต่อ CSS | N:1 StackGuideSet |
| ConventionDoc | name, path | ต้องมีครบ 4 ไฟล์ | — |
| NamingRule | pattern | ใช้ใน naming.md | N:1 ConventionDoc |
| JsonEnvelope | success_shape, error_shape, field_case | field_case = `snake_case`; pagination ใน `meta` | 1:1 `json-api.md` |
| ChecklistStep | stack, text, required | ทุก StackName มี ≥1 ขั้น; UI stack มีขั้น footer | N:1 ScaffoldingChecklist |

**Indexes (logical)**: `StackName.id`, `ConventionDoc.path` — unique

**ชุดที่ล็อก**

| Stack | ไฟล์ | has_ui |
|-------|------|--------|
| Go monolith | `docs/stacks/go-monolith.md` | ใช่ |
| Next.js | `docs/stacks/nextjs.md` | ใช่ |
| Nest.js | `docs/stacks/nestjs.md` | ไม่ (backend) |
| Express.js | `docs/stacks/expressjs.md` | ไม่ (backend) |

## API Specification

ไม่มี HTTP API. สัญญาที่ทีมอ่านคือ **document contracts**:

| Contract | Path | Auth | Request | Response | Errors |
|----------|------|------|---------|----------|--------|
| Read stack guide | `docs/stacks/{name}.md` | git read | — | ขั้นตอน setup + ลิงก์ theme/spec | เป็น template เต็ม / ไม่ชี้ brand = ผิดสัญญา |
| Read convention | `docs/conventions/{name}.md` | git read | — | กฎ naming/structure/git/JSON | ขาด 1 ใน 4 ไฟล์ = ผิดสัญญา |
| Read scaffolding | `docs/scaffolding.md` | git read | — | ขั้นร่วม + checklist ต่อ stack | ไม่มีขั้นต่อ stack / ไม่มี footer สำหรับ UI = ผิดสัญญา |

**Conventions**
- Versioning: git + `CHANGELOG.md`
- Publish: merge `main` = ปล่อย (D3-12)
- Snippet: สั้น; ห้ามกลายเป็น template ครบชุดต่อ stack

## Integration Points

| System | Protocol | Purpose | Error handling |
|--------|----------|---------|----------------|
| `brand-theme` | Data (links) | วิธีต่อ `@theme` / token — อ้างชื่อ ไม่คัดลอก hex | ถ้าเจอ hex ล้วน → แทนด้วยลิงก์ `docs/brand/` |
| `ui-components` | Docs (links) | UI stack/checklist อ้าง spec + footer บังคับ | ห้ามสำเนา anatomy — ลิงก์ `docs/components/` |

## Implementation

**Directory**
```
docs/stacks/
  go-monolith.md
  nextjs.md
  nestjs.md
  expressjs.md
docs/conventions/
  project-structure.md
  naming.md
  git.md
  json-api.md
docs/scaffolding.md
docs/README.md          สารบัญชี้ scaffolding (มีอยู่แล้ว)
CHANGELOG.md
```

**Dev setup**: เปิด Markdown — ไม่มี package manager / build / generator

**Conventions**
- 4 stack ตามตาราง; Go = Chi+HTMX+Tailwind v4; Next = App Router; backend = layering + JSON envelope
- งานค้างของ unit นี้: ให้ 4 guide + 4 convention + scaffolding สอดคล้อง D3 (ชี้ theme, ไม่มี hex ล้วน, footer ใน UI path) — ไฟล์มีอยู่แล้ว ตรวจแล้วปะช่องว่าง

## Testing Strategy

- **Pyramid**: ไม่มี unit/e2e runtime — ชั้นเดียวคือ **review properties** ตอน PR
- **Frameworks**: ไม่มี test runner
- **Coverage**: ทุก stack ชี้ theme; convention ครบ; scaffolding ครบ 4 stack; UI มี footer
- **Mock / test data**: ไฟล์เอกสารคือข้อมูลจริง
- **Run**: checklist ใน PR (ดู Correctness)

## NFR

- **API consistency**: JSON envelope + `snake_case` ตาม `json-api.md`
- **Accessibility / footer**: ไม่กำหนดสูตรใหม่ — ลิงก์ spec ของ `ui-components`
- **Performance / security runtime**: ไม่มี — ไม่ใช่ service

## Operations

**Level**: Minimal

| Signal | ที่ไหน | เมื่อไหร่ |
|--------|--------|-----------|
| Logging | `CHANGELOG.md` + git | ทุกการเปลี่ยน stack/convention/checklist |
| Error tracking | commit / PR | เมื่อพบ hex ล้วน, guide ไม่ชี้ SSOT, checklist ขาด footer |
| Health | ไม่มี endpoint | ความพร้อม = 4 stack + 4 convention + scaffolding เปิดได้ |
| Lifecycle | merge `main` | — |
| Config/secrets | ไม่มี | — |

## Correctness

| Property | Description | Validates |
|----------|-------------|-----------|
| StackThemePointer | ทุก stack guide ชี้ `docs/brand/theme-tailwind.md` (หรือ brand/) เมื่อต่อ CSS/theme | StackGuideSet |
| ConventionSetComplete | มีครบ 4 ไฟล์ conventions | ConventionSet |
| ScaffoldingPerStack | scaffolding มีขั้นสำหรับทั้ง 4 StackName | ScaffoldingChecklist |
| DeliveryNoOrphanHex | ไม่มี hex แบรนด์ล้วนใน stacks/conventions/scaffolding | ทุกไฟล์ unit |
| FooterStepForUI | Go + Next (และขั้นร่วมที่มี UI) กล่าวถึง footer "Powered by i24" | StackGuideSet, ScaffoldingChecklist |

## Traceability

| Requirement | Component(s) | Endpoint(s) | Entity | Status |
|-------------|--------------|-------------|--------|--------|
| F-stacks | StackGuideSet | Read stack guide | StackGuide, StackName | Covered |
| F-conventions | ConventionSet | Read convention | ConventionDoc, NamingRule, JsonEnvelope | Covered |
| F-scaffolding | ScaffoldingChecklist | Read scaffolding | ChecklistStep | Covered |

**Coverage**: 3/3 — ไม่มี gap

**Components without requirement**: ไม่มี

## External References

| Source | Type | Used in |
|--------|------|---------|
| `docs/brand/theme-tailwind.md` | Theme map (foundation) | StackGuide |
| `docs/components/README.md` + `footer.md` | UI catalog (upstream) | UI stacks / scaffolding |
| `docs/stacks/*.md` | guides ปัจจุบัน | StackGuideSet |
| `docs/conventions/*.md` | conventions ปัจจุบัน | ConventionSet |
| `docs/scaffolding.md` | checklist ปัจจุบัน | ScaffoldingChecklist |
| Tailwind CSS 4.3.3 | Version pin (foundation) | theme wiring |
