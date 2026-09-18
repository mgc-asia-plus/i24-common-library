# Design Decisions (D3) — unit: delivery-guides

## Context Summary
- Unit: `delivery-guides` (domain) — stories: F-stacks, F-conventions, F-scaffolding
- Deliverable = แนวทางใน `docs/stacks/` + `docs/conventions/` + `docs/scaffolding.md` — ไม่ใช่ runtime / ไม่ใช่ code generator
- Upstream ล็อกแล้ว: `brand-theme` (Navy `#0F172A`, token names, Tailwind 4.3.3 `@theme` + `[data-theme]`) และ `ui-components` (14 spec, footer บังคับ, `.mac-sidebar` / `.mac-table`)
- ข้ามเรื่อง foundation: repo เอกสารเดียว, ไม่มี HTTP API/DB/auth, อ้างชื่อ token ห้ามสำเนา hex, merge `main` = ปล่อย
- มีไฟล์อยู่แล้ว: `docs/stacks/{go-monolith,nextjs,nestjs,expressjs}.md`, `docs/conventions/{project-structure,naming,git,json-api}.md`, `docs/scaffolding.md`
- Product constraint: Markdown เท่านั้น — snippet สั้น ไม่เก็บ template โค้ดครบชุด

---

## Decision Questions

### D3-1: ชุด stack ที่เอกสารรับรอง
**Question**: unit นี้รับรอง stack ไหนใน v1?
- 1) ล็อก 4 ตัวที่มีไฟล์แล้ว: Go monolith, Next.js, Nest.js, Express.js **(Recommended)**
- 2) ย่อเหลือ Go + Next.js ตามเฟส v1 เดิม แล้วค่อยเติม backend
- 3) ขยายชุดใน unit นี้ (เพิ่ม stack ใหม่)
- 4) Other (please specify): _______

**Answer**: 1) ล็อก 4 ตัวที่มีไฟล์แล้ว: Go monolith, Next.js, Nest.js, Express.js

---

### D3-2: ความลึกของ stack guide
**Question**: แต่ละ `docs/stacks/*.md` ควรครอบคลุมแค่ไหน?
- 1) ขั้นตอน setup + วิธีต่อ theme/tokens + ลิงก์ไป spec — ไม่ใช่ template โค้ดครบชุด **(Recommended)**
- 2) เก็บ skeleton โปรเจกต์เต็มต่อ stack ใน repo นี้
- 3) รายการลิงก์อย่างเดียว ไม่มีขั้นตอน
- 4) Other (please specify): _______

**Answer**: 1) ขั้นตอน setup + วิธีต่อ theme/tokens + ลิงก์ไป spec — ไม่ใช่ template โค้ดครบชุด

---

### D3-3: ไฟล์ conventions
**Question**: แยกไฟล์กฎอย่างไร?
- 1) คง 4 ไฟล์: `project-structure.md` + `naming.md` + `git.md` + `json-api.md` **(Recommended)**
- 2) รวมเป็น `conventions.md` ไฟล์เดียว
- 3) เพิ่มไฟล์ใหม่ใน unit นี้ (เช่น `error-handling.md`)
- 4) Other (please specify): _______

**Answer**: 1) คง 4 ไฟล์: `project-structure.md` + `naming.md` + `git.md` + `json-api.md`

---

### D3-4: รูปแบบ scaffolding
**Question**: ทีมเริ่มโปรเจกต์ใหม่ยึดอะไรแทน generator?
- 1) Checklist ใน `docs/scaffolding.md` แยกขั้นต่อ stack **(Recommended)** — สอดคล้อง pivot เอกสารอย่างเดียว
- 2) สร้าง CLI generator (`npx create-i24`)
- 3) ไม่มี scaffolding — มีแค่ stack guide
- 4) Other (please specify): _______

**Answer**: 1) Checklist ใน `docs/scaffolding.md` แยกขั้นต่อ stack

---

### D3-5: การอ้าง upstream
**Question**: stack/convention/checklist อ้าง brand และ component อย่างไร?
- 1) ลิงก์กลับ `docs/brand/` และ `docs/components/` — ห้ามสำเนาตารางสีหรือ anatomy **(Recommended)**
- 2) สำเนาตารางสีย่อในแต่ละ stack guide
- 3) อ้างแค่ brand ไม่ต้องอ้าง component spec
- 4) Other (please specify): _______

**Answer**: 1) ลิงก์กลับ `docs/brand/` และ `docs/components/` — ห้ามสำเนาตารางสีหรือ anatomy

---

### D3-6: Footer ในเส้นทางส่งมอบ
**Question**: checklist / stack ที่มี UI ต้องพูดถึง footer อย่างไร?
- 1) บังคับมีขั้น "Powered by i24" สำหรับทุก stack ที่มี UI **(Recommended)** — ยึด `ui-components`
- 2) แนะนำใน checklist แต่ไม่บังคับ
- 3) ไม่กล่าวถึง footer ใน unit นี้
- 4) Other (please specify): _______

**Answer**: 1) บังคับมีขั้น "Powered by i24" สำหรับทุก stack ที่มี UI

---

### D3-7: JSON API convention
**Question**: มาตรฐาน JSON ที่ `json-api.md` ล็อกแบบไหน?
- 1) ยึดไฟล์ปัจจุบัน — envelope + `snake_case` **(Recommended)**
- 2) เปลี่ยนเป็น `camelCase`
- 3) ไม่กำหนด JSON ใน unit นี้
- 4) Other (please specify): _______

**Answer**: 1) ยึดไฟล์ปัจจุบัน — envelope + `snake_case`

---

### D3-8: Correctness & Property-Based Testing
**Question**: ตรวจว่า delivery docs “ถูกเสมอ” อย่างไร?
- 1) คุณสมบัติตอน review: ทุก stack ชี้ `theme-tailwind.md`; convention ครบ 4 ไฟล์; scaffolding มีขั้นต่อ stack; ไม่มี hex ล้วน; UI stack กล่าวถึง footer **(Recommended)**
- 2) สคริปต์ parse markdown ตรวจใน CI
- 3) Property-based testing ด้วยไลบรารี
- 4) ไม่ตรวจเชิงคุณสมบัติ — พึ่งสายตาอย่างเดียว
- 5) Other (please specify): _______

**Answer**: 1) คุณสมบัติตอน review: ทุก stack ชี้ `theme-tailwind.md`; convention ครบ 4 ไฟล์; scaffolding มีขั้นต่อ stack; ไม่มี hex ล้วน; UI stack กล่าวถึง footer

---

### D3-9: โครงไฟล์
**Question**: จัดไฟล์ของ unit นี้อย่างไร?
- 1) `docs/stacks/` + `docs/conventions/` + `docs/scaffolding.md` **(Recommended)** — โครงปัจจุบัน
- 2) รวมใต้ `docs/delivery/`
- 3) ย้าย scaffolding เข้าแต่ละ stack guide
- 4) Other (please specify): _______

**Answer**: 1) `docs/stacks/` + `docs/conventions/` + `docs/scaffolding.md`

---

### D3-10: Observability Strategy
**Question**: unit เอกสารนี้ต้องมี observability ระดับไหน? (ไม่ใช่ runtime service)
- 1) Minimal — CHANGELOG + บันทึกการเปลี่ยน guide ใน PR **(Recommended)**
- 2) Standard — logging + metrics + health + readiness
- 3) Full — logging + metrics + tracing + alerting + dashboards
- 4) None — ไม่ติดตามการเปลี่ยนมาตรฐาน
- 5) Other (please specify): _______

**Answer**: 1) Minimal — CHANGELOG + บันทึกการเปลี่ยน guide ใน PR

---

### D3-11: Error Tracking
**Question**: จับ error ของมาตรฐาน delivery อย่างไร?
- 1) Log-based only — บันทึกใน git history / CHANGELOG **(Recommended)**
- 2) Dedicated error tracking service — Sentry / Datadog / Rollbar
- 3) Cloud-native — CloudWatch Insights / GCP Error Reporting / Azure Monitor
- 4) None — ไม่ติดตาม
- 5) Other (please specify): _______

**Answer**: 1) Log-based only — บันทึกใน git history / CHANGELOG

---

### D3-12: Health & Lifecycle Management
**Question**: lifecycle ของ “การปล่อย stack/convention/checklist” ต้องการอะไร?
- 1) Basic — merge เข้า main = ปล่อย (พอสำหรับเอกสารภายใน) **(Recommended)**
- 2) Health + readiness + graceful shutdown (สำหรับ container)
- 3) Health + readiness + graceful shutdown + startup probe + drain delay
- 4) Other (please specify): _______

**Answer**: 1) Basic — merge เข้า main = ปล่อย (พอสำหรับเอกสารภายใน)

---

## Decisions Summary
<!-- Machine-readable compact summary. Downstream phases: read ONLY this section. -->
- D3-1 Stack Set: Lock 4 — Go monolith, Next.js, Nest.js, Express.js
- D3-2 Guide Depth: Setup + theme/tokens wiring + links to specs; not full code templates
- D3-3 Convention Files: project-structure.md + naming.md + git.md + json-api.md
- D3-4 Scaffolding: Checklist in docs/scaffolding.md, steps per stack (no generator)
- D3-5 Upstream References: Link to docs/brand/ and docs/components/; no copied palettes/anatomy
- D3-6 Footer In Delivery: Required checklist step for every UI stack — Powered by i24
- D3-7 JSON API: Existing envelope + snake_case
- D3-8 Correctness: Review properties — theme pointer, 4 conventions, scaffolding per stack, no orphan hex, footer on UI stacks
- D3-9 File Layout: docs/stacks/ + docs/conventions/ + docs/scaffolding.md
- D3-10 Observability: Minimal — CHANGELOG + PR notes
- D3-11 Error Tracking: Log-based only — git history / CHANGELOG
- D3-12 Health/Lifecycle: Basic — merge main = release

---

**Instructions**: Fill in your answers above and respond with "done"
