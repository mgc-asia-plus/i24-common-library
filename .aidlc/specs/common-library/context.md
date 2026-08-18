# Context Assessment

## Summary
- **Type**: Greenfield
- **Scope**: new
- **Nature**: documentation-based common library — deliverable เป็นไฟล์ `.md` (ไม่ใช่ code generator / ไม่เก็บ template code หลายชุด)
- **Documented stacks**: Go monolith (Chi+HTMX+Tailwind), Next.js, Nest.js, Express.js (อธิบายเป็นแนวทาง)
- **Architecture**: docs repo — brand/tokens เป็น SSOT → stack guides อ้างอิง
- **Feature**: ชุดเอกสารมาตรฐานกลาง (brand/สีจากโลโก้, tokens, component spec, convention, stack setup guide)
- **Impact**: New standalone
- **Complexity**: Low/Medium — เอกสาร ~15-18 ไฟล์ แยกหมวด
- **Recommendations**: Personas No, Units Yes, NFR No

## Project Overview
- **Type**: Greenfield
- **Assessment Date**: 2026-08-17T09:00:00+07:00

โปรเจกต์นี้ยังว่าง มีเพียง `i24_LOGO.png` และไฟล์ `.kiro/` (skills + steering) เท่านั้น
หมายเหตุ: ไฟล์ `.kiro/steering/{product,tech,structure,session-boot}.md` ที่มีอยู่เป็นของโปรเจกต์ **i24-etax-service** (ถูกก็อปติดมา) ไม่เกี่ยวกับ common library — แนะนำให้ลบ/แทนที่ (รอผู้ใช้ยืนยัน)

## Technology Stack
- **Languages**: N/A — greenfield (ผู้ใช้เสนอ candidate: Go, TypeScript)
- **Frameworks**: N/A — candidate: Chi + HTMX + Tailwind v4 / Next.js + Nest.js
- **Build System**: N/A — จะกำหนดใน D3
- **Testing**: N/A
- **Infrastructure**: N/A

## Feature Impact

**Affected Areas**: New standalone — สร้างจากศูนย์

| Area | Impact | Reason |
|------|--------|--------|
| Design tokens | New | SSOT ของสี/typography/spacing จากแบรนด์ i24 |
| Tailwind theme/preset | New | แปลง tokens → `@theme` ใช้ได้ทั้ง Go และ Next.js |
| Component templates | New | Go `html/template` + HTMX partials |
| React components | New | สำหรับ Next.js consumer |
| Prototype/showcase | New | หน้ารวม demo ทุก component + สีแบรนด์ |

## Recommendations

- Story Count: Medium (6-10)
- Domain Boundaries: (1) Design tokens/theme, (2) Components, (3) Docs & prototype gallery
- User Types: นักพัฒนาที่ import library (Go monolith devs, Next.js/Nest.js devs)
- Integration Points: consumer projects ทั้งสองสแตก
- **Personas**: No — ผู้ใช้เป็น developer กลุ่มเดียว (internal), ไม่ต้องทำ persona
- **Units**: Yes — แยกเป็น units ตาม domain (tokens → components → prototype) เพราะ tokens เป็นฐานให้ทุกอย่าง
- **NFR**: No — เป็น library ไม่มี runtime SLA/scaling ที่ต้องระบุเป็นพิเศษ

## Brand Palette (จากไฟล์ vector ทางการ `i24_LOGO.svg`)

> ✅ red-500/coral-400/white ยืนยันจากโลโก้; เฉดอื่น derived. SSOT อยู่ที่ `docs/brand/palette.md`

| Token | Hex | ใช้กับ |
|-------|------|--------|
| `brand-red-500` (primary) | `#EC2129` ✅ | สีหลักแบรนด์ (พื้นโลโก้), ปุ่ม primary, header |
| `brand-red-600` (hover/dark) | `#C81B22` | hover/active + white text เล็กบนพื้นแดง |
| `brand-red-400` (light) | `#F04E52` | เน้นรอง, border เข้ม, focus ring |
| `brand-red-50` (tint) | `#FDECED` | พื้นหลังอ่อน, badge |
| `brand-coral-400` (accent) | `#F48569` ✅ | สีเน้น (blob ในโลโก้), tag/illustration |
| `brand-coral-300` (accent light) | `#F7A48A` | accent อ่อน |
| `white` | `#FFFFFF` ✅ | ตัวอักษร "i24" บนพื้นแดง, พื้น card |
| `ink-900` (text) | `#1A1A1A` | ข้อความหลักบนพื้นสว่าง |
| `ink-500` (muted) | `#6B7280` | ข้อความรอง |
| `paper-muted` (surface) | `#F7F7F8` | พื้นหลังหน้า/section |

## Scope

- **Detected scope**: new
- **Rationale**: workspace ว่าง (ไม่มี source code), ผู้ใช้ต้องการสร้างโปรเจกต์ common library ตั้งแต่ต้น
- **Phases skipped**: None — full workflow

## Recommended Workflow

```
        ┌─────────────┐
        │   Context   │  ✅ (คุณอยู่ที่นี่)
        └──────┬──────┘
               ▼
        ┌─────────────┐
        │ Requirements│  user stories + EARS (2 consumer stacks)
        └──────┬──────┘
               ▼
        ┌─────────────┐
        │Decomposition│  units: tokens → components → prototype
        └──────┬──────┘
               ▼
     ┌───────────────────┐
     │  per-unit cycle    │
     │  Design → Tasks →  │   ◀── D3 เลือกสแตก (Go+HTMX / Next.js / ทั้งคู่)
     │  Implement         │
     └─────────┬─────────┘
               ▼
        ┌─────────────┐
        │ Build & Test│
        └──────┬──────┘
               ▼
        ┌─────────────┐
        │   Deploy    │  publish (Go module / npm package)
        └─────────────┘

  (option) Prototype spike ควบคู่ Requirements เพื่อ validate สี/component เร็ว ๆ
```

## External References

| Source | Type | What was used |
|--------|------|---------------|
| `i24_LOGO.png` | Design asset | ดึง brand palette (สีแดงหลัก + coral accent + white) |
