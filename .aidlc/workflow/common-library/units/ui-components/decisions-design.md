# Design Decisions (D3) — unit: ui-components

## Context Summary
- Unit: `ui-components` (domain) — stories: F-components, F-prototype
- Deliverable = spec ใน `docs/components/` + หน้า preview (`prototype/index.html`) — ไม่ใช่ runtime service / ไม่ใช่ component library ที่ publish
- Upstream `brand-theme` ล็อกแล้ว (ห้ามถามซ้ำ): Navy `#0F172A` SSOT; Primitive → Semantic; `[data-theme]`; อ้างชื่อ token ห้ามสำเนา hex; `effects.md` เป็นสูตร glass/gradient; WCAG 2.1 AA ของสี; single repo เอกสาร
- มีไฟล์ spec อยู่แล้ว (button, badge, card, input, table, nav-header, sidebar, alert, theme-mode, footer, modal, select, toast, pagination) + prototype `.mac-sidebar` / `.mac-table`
- Architecture จาก D2: Modular Monolith / Customer/Supplier ทางเดียว — brand-theme → ui-components → delivery-guides

---

## Decision Questions

### D3-1: ขอบเขตแคตตาล็อก
**Question**: unit นี้รับรอง component ชุดไหนใน v1?
- 1) ล็อกตาม `docs/components/README.md` ปัจจุบัน (14 spec รวม sidebar, table, modal, select, toast, pagination, footer) **(Recommended)** — ไฟล์มีอยู่แล้ว
- 2) ย่อเหลือชุดพื้นฐาน (button, badge, card, input, table, nav-header, alert, theme-mode, footer)
- 3) ขยายแคตตาล็อกใน unit นี้ (เพิ่ม component ใหม่)
- 4) Other (please specify): _______

**Answer**: 1) ล็อกตาม `docs/components/README.md` ปัจจุบัน (14 spec รวม sidebar, table, modal, select, toast, pagination, footer)

---

### D3-2: เทมเพลต spec
**Question**: ทุกไฟล์ component ต้องมีหัวข้อไหนบ้าง?
- 1) คง 8 หัวข้อ: Purpose → Anatomy → Variants → Sizes → States → Tokens used → Accessibility → Reference snippet **(Recommended)**
- 2) ย่อเหลือ Purpose + Tokens used + Accessibility
- 3) ไม่บังคับโครง — เขียนอิสระต่อไฟล์
- 4) Other (please specify): _______

**Answer**: 1) คง 8 หัวข้อ: Purpose → Anatomy → Variants → Sizes → States → Tokens used → Accessibility → Reference snippet

---

### D3-3: หน้า preview (F-prototype)
**Question**: แสดง token + component ให้ดูรวมกันที่ไหน?
- 1) Static HTML `prototype/index.html` เป็น gallery (มี `.mac-sidebar` / `.mac-table` แล้ว) **(Recommended)**
- 2) เอกสาร Markdown อย่างเดียว ไม่มีหน้า live
- 3) เพิ่ม Storybook / static docs site
- 4) Other (please specify): _______

**Answer**: 1) Static HTML `prototype/index.html` เป็น gallery (มี `.mac-sidebar` / `.mac-table` แล้ว)

---

### D3-4: Reference snippet ใน spec
**Question**: ตัวอย่างโค้ดในแต่ละ spec ควรเป็นแบบไหน?
- 1) HTML สั้น (และชื่อคลาส React/Tailwind ได้) — ไม่ใช่ template ครบชุด **(Recommended)** — สอดคล้องนโยบาย snippet ของ foundation
- 2) HTML อย่างเดียว
- 3) ตัวอย่างแยกครบทุก stack ที่เอกสารรับรอง (Go/HTMX + React + …)
- 4) Other (please specify): _______

**Answer**: 1) HTML สั้น (และชื่อคลาส React/Tailwind ได้) — ไม่ใช่ template ครบชุด

---

### D3-5: ชื่อคลาสของ shell (sidebar / table)
**Question**: คลาสที่ spec และ prototype ต้องใช้ร่วมกันคืออะไร?
- 1) ล็อก `.mac-sidebar` / `.mac-table` / `.mac-table-wrap` / `.mac-section` **(Recommended)** — มีใน brand-theme + prototype แล้ว
- 2) เปลี่ยนเป็น `.i24-sidebar` / `.i24-table` ให้สอดคล้อง prefix `.i24-*`
- 3) spec อธิบาย anatomy อย่างเดียว ไม่ล็อกชื่อคลาส CSS
- 4) Other (please specify): _______

**Answer**: 1) ล็อก `.mac-sidebar` / `.mac-table` / `.mac-table-wrap` / `.mac-section`

---

### D3-6: Footer บังคับ
**Question**: footer "Powered by i24" ใน unit นี้มีสถานะอย่างไร?
- 1) บังคับทุกระบบที่มี UI — ระบุใน README + `footer.md` **(Recommended)** — เป็นมาตรฐานปัจจุบัน
- 2) แนะนำ แต่ไม่บังคับ
- 3) ย้ายไป unit `delivery-guides` ไม่กำหนดใน spec
- 4) Other (please specify): _______

**Answer**: 1) บังคับทุกระบบที่มี UI — ระบุใน README + `footer.md`

---

### D3-7: เกณฑ์ a11y ของ component
**Question**: นอกจาก contrast สีที่ foundation ล็อกแล้ว spec ต้องกำหนด a11y อะไร?
- 1) WCAG 2.1 AA: focus ที่มองเห็น (`color-focus-ring`), keyboard, แตะขั้นต่ำ 40×40, role/aria ในแต่ละ spec **(Recommended)**
- 2) เขียนโน้ต a11y หลวม ไม่มี checklist
- 3) ยกระดับ AAA + บังคับ `prefers-reduced-motion` ทุกตัว
- 4) Other (please specify): _______

**Answer**: 1) WCAG 2.1 AA: focus ที่มองเห็น (`color-focus-ring`), keyboard, แตะขั้นต่ำ 40×40, role/aria ในแต่ละ spec

---

### D3-8: Correctness & Property-Based Testing
**Question**: ตรวจว่า spec/prototype “ถูกเสมอ” อย่างไร?
- 1) คุณสมบัติตอน review: spec ครบ Tokens used + States; ไม่มี hex แบรนด์โดยไม่มีชื่อ token; คลาสใน prototype ตรง spec; gallery มี footer **(Recommended)**
- 2) สคริปต์ parse markdown / HTML แล้วตรวจใน CI
- 3) Property-based testing ด้วยไลบรารี (fast-check / Hypothesis)
- 4) ไม่ตรวจเชิงคุณสมบัติ — พึ่งสายตาอย่างเดียว
- 5) Other (please specify): _______

**Answer**: 1) คุณสมบัติตอน review: spec ครบ Tokens used + States; ไม่มี hex แบรนด์โดยไม่มีชื่อ token; คลาสใน prototype ตรง spec; gallery มี footer

---

### D3-9: โครงไฟล์ใน `docs/components/`
**Question**: จัดไฟล์ spec อย่างไร?
- 1) `README.md` เป็นดัชนี + กฎร่วม และหนึ่งไฟล์ต่อ component **(Recommended)** — โครงปัจจุบัน
- 2) รวมทุก component ในไฟล์เดียว
- 3) รวมตามประเภท (`basic.md`, `navigation.md`, `complex.md`)
- 4) Other (please specify): _______

**Answer**: 1) `README.md` เป็นดัชนี + กฎร่วม และหนึ่งไฟล์ต่อ component

---

### D3-10: Observability Strategy
**Question**: unit เอกสารนี้ต้องมี observability ระดับไหน? (ไม่ใช่ runtime service)
- 1) Minimal — CHANGELOG + บันทึกการเปลี่ยน spec/prototype ใน PR **(Recommended)**
- 2) Standard — logging + metrics + health + readiness
- 3) Full — logging + metrics + tracing + alerting + dashboards
- 4) None — ไม่ติดตามการเปลี่ยนมาตรฐาน
- 5) Other (please specify): _______

**Answer**: 1) Minimal — CHANGELOG + บันทึกการเปลี่ยน spec/prototype ใน PR

---

### D3-11: Error Tracking
**Question**: จับ error ของมาตรฐาน component อย่างไร?
- 1) Log-based only — บันทึกใน git history / CHANGELOG **(Recommended)**
- 2) Dedicated error tracking service — Sentry / Datadog / Rollbar
- 3) Cloud-native — CloudWatch Insights / GCP Error Reporting / Azure Monitor
- 4) None — ไม่ติดตาม
- 5) Other (please specify): _______

**Answer**: 1) Log-based only — บันทึกใน git history / CHANGELOG

---

### D3-12: Health & Lifecycle Management
**Question**: lifecycle ของ “การปล่อย spec / prototype” ต้องการอะไร?
- 1) Basic — merge เข้า main = ปล่อย (พอสำหรับเอกสารภายใน) **(Recommended)**
- 2) Health + readiness + graceful shutdown (สำหรับ container)
- 3) Health + readiness + graceful shutdown + startup probe + drain delay
- 4) Other (please specify): _______

**Answer**: 1) Basic — merge เข้า main = ปล่อย (พอสำหรับเอกสารภายใน)

---

## Decisions Summary
<!-- Machine-readable compact summary. Downstream phases: read ONLY this section. -->
- D3-1 Catalog Scope: Lock `docs/components/README.md` — 14 specs (sidebar, table, modal, select, toast, pagination, footer included)
- D3-2 Spec Template: 8 sections — Purpose → Anatomy → Variants → Sizes → States → Tokens used → Accessibility → Reference snippet
- D3-3 Preview: Static HTML `prototype/index.html` gallery
- D3-4 Snippets: Short HTML (+ optional React/Tailwind class names), not full templates
- D3-5 Shell Classes: Lock `.mac-sidebar` / `.mac-table` / `.mac-table-wrap` / `.mac-section`
- D3-6 Footer Mandate: Required on every UI — README + `footer.md`
- D3-7 Component A11y: WCAG 2.1 AA — visible focus (`color-focus-ring`), keyboard, 40×40 touch, role/aria per spec
- D3-8 Correctness: Review properties — Tokens+States complete; no brand hex without token name; prototype classes match spec; gallery has footer
- D3-9 File Layout: `README.md` index + one file per component
- D3-10 Observability: Minimal — CHANGELOG + PR notes on spec/prototype changes
- D3-11 Error Tracking: Log-based only — git history / CHANGELOG
- D3-12 Health/Lifecycle: Basic — merge `main` = release

---

**Instructions**: Fill in your answers above and respond with "done"
