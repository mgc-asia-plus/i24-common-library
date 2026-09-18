# Design Decisions (D3) — unit: brand-theme

## Context Summary
- Unit: `brand-theme` (foundation) — stories: F-brand, F-tokens, F-theme, F-effects
- Deliverable ของ unit นี้ = เอกสาร SSOT ใน `docs/brand/` (ไม่ใช่ runtime service)
- Architecture จาก D2: Modular Monolith / Domain-Driven / Customer/Supplier ทางเดียว
- Stack ของ repo: Markdown docs (ไม่มี build)
- เอกสาร brand มีอยู่แล้ว — D3 ใช้ล็อกวิธีคง SSOT ไม่ใช่เลือกสแตกแอป
- **Drift ที่ต้องตัดสิน**: `docs/brand/palette.md` ปัจจุบัน = Navy Solid `#0A2540` + Frosted Gray Glass + Deep Crimson `#B0141B` แต่ `blueprints/` / resources ยังมีชุดโลโก้เก่า `brand-red-500 #EC2129` + coral

---

## Decision Questions

### D3-1: Canonical palette (SSOT ของสี)
**Question**: ชุดสีที่เป็นทางการของ `brand-theme` คือชุดไหน?
- 1) Lock ตาม `docs/brand/palette.md` ปัจจุบัน — Navy Solid + Frosted Gray Glass + Deep Crimson **(Recommended)**
- 2) ย้อนกลับไปชุดจากโลโก้ SVG — `brand-red-500 #EC2129` + coral `#F48569`
- 3) เก็บสองชุด (logo red สำหรับ mark, navy/glass สำหรับ UI) แยกตารางชัด
- 4) Other (please specify): _______

**Answer**: 1) Lock ตาม `docs/brand/palette.md` ปัจจุบัน — Navy Solid + Frosted Gray Glass + Deep Crimson

---

### D3-2: ชั้น token
**Question**: โครงสร้าง token ที่ unit อื่นต้อง conform เป็นแบบไหน?
- 1) 2 ชั้น: Primitive → Semantic (light/dark) **(Recommended)**
- 2) ชั้นเดียว: ใช้ hex ในเอกสารโดยตรง ไม่แยก semantic
- 3) 3 ชั้น: Primitive → Alias → Semantic (เพิ่มชั้น map ชื่อ)
- 4) Other (please specify): _______

**Answer**: 1) 2 ชั้น: Primitive → Semantic (light/dark)

---

### D3-3: Theme mapping ที่เอกสารนี้รับรอง
**Question**: วิธี map token → โค้ดที่ `theme-*.md` ควรรับรองอะไร?
- 1) Tailwind v4 `@theme` + CSS variables + `[data-theme]` **(Recommended)** — snippet อ้างอิงสั้น ๆ ไม่ใช่ template เต็ม
- 2) CSS variables ล้วน (ไม่ระบุ Tailwind)
- 3) รับรองหลายตัวพร้อมกัน (Tailwind v4 + CSS-in-JS + native CSS)
- 4) Other (please specify): _______

**Answer**: 1) Tailwind v4 `@theme` + CSS variables + `[data-theme]` — snippet อ้างอิงสั้น ๆ ไม่ใช่ template เต็ม

---

### D3-4: กติกาอ้างอิงของ downstream (ui-components, delivery-guides)
**Question**: unit อื่นอ้างค่าสี/token อย่างไร?
- 1) อ้างชื่อ token เท่านั้น ห้ามคัดลอก hex ใน spec/stack guide **(Recommended)**
- 2) คัดลอก hex ได้ถ้าใส่ footnote ชี้ `palette.md`
- 3) อนุญาตสำเนาตารางสีย่อในแต่ละ component
- 4) Other (please specify): _______

**Answer**: 1) อ้างชื่อ token เท่านั้น ห้ามคัดลอก hex ใน spec/stack guide

---

### D3-5: Light / dark
**Question**: มาตรฐานสลับธีมที่ brand กำหนดให้ทุก UI ยึด?
- 1) `[data-theme="light"|"dark"]` บน root + semantic token แยกค่าต่อโหมด **(Recommended)**
- 2) class `.dark` (Tailwind default) เป็นหลัก
- 3) รองรับแค่ light ก่อน dark ทีหลัง
- 4) Other (please specify): _______

**Answer**: 1) `[data-theme="light"|"dark"]` บน root + semantic token แยกค่าต่อโหมด

---

### D3-6: ไฟล์ SSOT ใน `docs/brand/`
**Question**: แยกไฟล์อย่างไรใน foundation นี้?
- 1) คง 4 ไฟล์: `palette.md` + `design-tokens.md` + `theme-tailwind.md` + `effects.md` **(Recommended)**
- 2) รวมเป็นไฟล์เดียว `brand.md`
- 3) แยกเพิ่ม `contrast.md` / `typography.md` เป็นไฟล์ใหม่
- 4) Other (please specify): _______

**Answer**: 1) คง 4 ไฟล์: `palette.md` + `design-tokens.md` + `theme-tailwind.md` + `effects.md`

---

### D3-7: Effects (glass / gradient) ขอบเขตใน unit นี้
**Question**: F-effects อยู่ใน foundation นี้แค่ไหน?
- 1) `effects.md` เป็น SSOT ของสูตร glass/gradient; component อ้างสูตร ห้ามคิดค่า blur/opacity เอง **(Recommended)**
- 2) effects เป็นแนวทางหลวม — component กำหนดสูตรเองได้
- 3) ย้าย effects ไป unit `ui-components` ทั้งหมด
- 4) Other (please specify): _______

**Answer**: 1) `effects.md` เป็น SSOT ของสูตร glass/gradient; component อ้างสูตร ห้ามคิดค่า blur/opacity เอง

---

### D3-8: Repository Structure
**Question**: โครงสร้าง repo ของ common library (foundation กำหนดให้ทุก unit)?
- 1) Single repo เอกสาร — ไม่มี package manager / monorepo tool **(Recommended)**
- 2) Single repo แต่เพิ่ม package (เช่น npm) สำหรับ publish token JSON
- 3) Monorepo แยก package `brand` / `docs`
- 4) Other (please specify): _______

**Answer**: 1) Single repo เอกสาร — ไม่มี package manager / monorepo tool

---

### D3-9: Correctness & Property-Based Testing
**Question**: ตรวจว่า token/สี “ถูกเสมอ” อย่างไร?
- 1) คุณสมบัติในเอกสาร: ชื่อ token ไม่ซ้ำ, semantic ครบทั้ง light/dark, contrast ผ่าน WCAG AA ตามตารางใน `palette.md` — ตรวจตอน review **(Recommended)**
- 2) สคริปต์ตรวจ (parse markdown → ตรวจ hex / คู่ contrast) รันใน CI
- 3) Property-based testing ด้วยไลบรารี (fast-check / Hypothesis) บนไฟล์ token
- 4) ไม่ตรวจเชิงคุณสมบัติ — พึ่งสายตาอย่างเดียว
- 5) Other (please specify): _______

**Answer**: 1) คุณสมบัติในเอกสาร: ชื่อ token ไม่ซ้ำ, semantic ครบทั้ง light/dark, contrast ผ่าน WCAG AA ตามตารางใน `palette.md` — ตรวจตอน review

---

### D3-10: มาตรฐาน contrast / a11y ของสี
**Question**: เกณฑ์ contrast ที่ palette ต้องผ่าน?
- 1) WCAG 2.1 AA สำหรับข้อความบนพื้นหลัก (primary+on-primary, text+canvas) **(Recommended)**
- 2) WCAG 2.1 AAA ทั้งชุด
- 3) ไม่ล็อกตัวเลข — ดูสวยเป็นหลัก
- 4) Other (please specify): _______

**Answer**: 1) WCAG 2.1 AA สำหรับข้อความบนพื้นหลัก (primary+on-primary, text+canvas)

---

### D3-11: Observability Strategy
**Question**: unit เอกสารนี้ต้องมี observability ระดับไหน? (ไม่ใช่ runtime service)
- 1) Minimal — CHANGELOG + บันทึกการเปลี่ยน token ใน PR **(Recommended)**
- 2) Standard — logging + metrics + health + readiness
- 3) Full — logging + metrics + tracing + alerting + dashboards
- 4) None — ไม่ติดตามการเปลี่ยนมาตรฐาน
- 5) Other (please specify): _______

**Answer**: 1) Minimal — CHANGELOG + บันทึกการเปลี่ยน token ใน PR

---

### D3-12: Error Tracking
**Question**: จับ error ของมาตรฐานนี้อย่างไร?
- 1) Log-based only — บันทึกใน git history / CHANGELOG **(Recommended)**
- 2) Dedicated error tracking service — Sentry / Datadog / Rollbar
- 3) Cloud-native — CloudWatch Insights / GCP Error Reporting / Azure Monitor
- 4) None — ไม่ติดตาม
- 5) Other (please specify): _______

**Answer**: 1) Log-based only — บันทึกใน git history / CHANGELOG

---

### D3-13: Health & Lifecycle Management
**Question**: lifecycle ของ “การปล่อยมาตรฐาน brand” ต้องการอะไร?
- 1) Basic — merge เข้า main = ปล่อย (พอสำหรับเอกสารภายใน) **(Recommended)**
- 2) Health + readiness + graceful shutdown (สำหรับ container)
- 3) Health + readiness + graceful shutdown + startup probe + drain delay
- 4) Other (please specify): _______

**Answer**: 1) Basic — merge เข้า main = ปล่อย (พอสำหรับเอกสารภายใน)

---

## Decisions Summary
<!-- Machine-readable compact summary. Downstream phases: read ONLY this section. -->
- D3-1 Canonical Palette: Lock `docs/brand/palette.md` — Navy Solid + Frosted Gray Glass + Deep Crimson
- D3-2 Token Layers: Primitive → Semantic (light/dark)
- D3-3 Theme Mapping: Tailwind v4 `@theme` + CSS variables + `[data-theme]` (snippet อ้างอิงสั้น)
- D3-4 Downstream Reference Rule: อ้างชื่อ token เท่านั้น ห้ามคัดลอก hex
- D3-5 Light/Dark: `[data-theme="light"|"dark"]` บน root + semantic แยกค่าต่อโหมด
- D3-6 Brand File Split: palette.md + design-tokens.md + theme-tailwind.md + effects.md
- D3-7 Effects Scope: effects.md เป็น SSOT ของสูตร glass/gradient
- D3-8 Repository Structure: Single repo เอกสาร — ไม่มี package manager / monorepo tool
- D3-9 Correctness: คุณสมบัติในเอกสาร ตรวจตอน review (ชื่อไม่ซ้ำ, semantic ครบ light/dark, contrast AA)
- D3-10 Contrast/A11y: WCAG 2.1 AA สำหรับข้อความบนพื้นหลัก
- D3-11 Observability: Minimal — CHANGELOG + บันทึกการเปลี่ยน token ใน PR
- D3-12 Error Tracking: Log-based only — git history / CHANGELOG
- D3-13 Health/Lifecycle: Basic — merge เข้า main = ปล่อย

---

**Instructions**: Fill in your answers above and respond with "done"
