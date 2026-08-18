# Requirements Decisions (D1)

## Context Summary
- Greenfield, scope=new — สร้าง i24 common **scaffolding monorepo + generator**
- clone repo → รันคำสั่งเลือก tech stack → scaffold โปรเจกต์ใหม่ที่ต่อ "ของกลาง" ไว้แล้ว
- Target stacks: Go monolith (Chi+HTMX+Tailwind v4), Next.js (frontend), Nest.js (backend), Express.js (backend)
- ของกลาง: design tokens/brand theme (สีจากโลโก้ — `brand-red-500 #E4181E`, `brand-coral-400 #F47C6E` ฯลฯ), component/template, convention
- หมายเหตุ: ผู้ใช้พิมพ์ "next.js" สองครั้ง — ตีความตัวที่สองเป็น **nest.js** (โปรดยืนยัน/แก้ที่ D1-2)

---

## Decision Questions

### D1-1: ขอบเขต release แรก (v1)
**Question**: v1 ควรครอบคลุมแค่ไหน?
- 1) ของกลาง (tokens+theme) + generator ที่ scaffold ได้ 1 stack (Go monolith) ก่อน
- 2) ของกลาง + generator + template ครบทุก stack ที่ระบุ + component/template ชุดพื้นฐาน **(Recommended)**
- 3) เหมือน (2) + docs/prototype site เต็มรูปแบบ + publish package
- 4) Other (please specify): _______

**Answer**: 2) ของกลาง + generator + template ครบทุก stack + component พื้นฐาน

---

### D1-2: รายการ stack ที่ generator ต้องรองรับใน v1
**Question**: ยืนยัน stack ที่ต้อง scaffold ได้ (คุณพิมพ์ next.js ซ้ำ — ตีความเป็น nest.js)
- 1) Go monolith, Next.js, Nest.js, Express.js (ครบ 4) **(Recommended)**
- 2) Go monolith, Next.js, Express.js (ตัด Nest.js)
- 3) เริ่มแค่ Go monolith + Next.js ก่อน แล้วค่อยเพิ่ม backend
- 4) Other (please specify): _______

**Answer**: 1) Go monolith, Next.js, Nest.js, Express.js (ครบ 4 — ยืนยัน nest.js)

---

### D1-3: กลไก generator (คำสั่ง scaffold)
**Question**: อยากให้ "คำสั่งเลือก stack" ทำงานแบบไหน?
- 1) Node CLI เช่น `npx create-i24` / `pnpm create i24` (interactive prompt) **(Recommended)**
- 2) Makefile / shell script เช่น `make new stack=go`
- 3) Go CLI (binary เดียว รันได้ทุก OS)
- 4) Other (please specify): _______

**Answer**: 1) Node CLI (`npx create-i24`, interactive prompt)

---

### D1-4: ผลลัพธ์ของ generator (scaffold ไปที่ไหน)
**Question**: รันคำสั่งแล้วควรได้อะไร?
- 1) สร้างโฟลเดอร์โปรเจกต์ใหม่แยกออกมา (repo ใหม่, ตัด git history ของ template) **(Recommended)**
- 2) scaffold ในตำแหน่งปัจจุบัน (in-place)
- 3) เลือกได้ทั้งสองแบบผ่าน flag
- 4) Other (please specify): _______

**Answer**: 1) สร้างโฟลเดอร์โปรเจกต์ใหม่แยกออกมา (ตัด git history)

---

### D1-5: ขอบเขต "ของกลาง" (shared common layer) ใน v1
**Question**: ของกลางที่ทุก stack ดึงไปใช้ ควรมีอะไรบ้าง?
- 1) แค่ design tokens + brand theme (สี/typography/spacing)
- 2) tokens+theme + component/template UI (frontend: React + HTMX partial) **(Recommended)**
- 3) เหมือน (2) + shared backend util/config/convention (สำหรับ nest/express)
- 4) Other (please specify): _______

**Answer**: 3) tokens+theme + UI component + shared backend util/config/convention (สำหรับ nest/express) — ครบ FE&BE

---

### D1-6: ชุด component/template พื้นฐานใน v1
**Question**: อยากได้ component/template อะไรในของกลาง v1?
- 1) Core เล็ก: Button, Badge, Card, Input + layout เปล่า
- 2) Core + layout/nav: Button, Badge, Card, Input, Table, Nav/Header, Alert + หน้า sample **(Recommended)**
- 3) เต็มชุด: + Modal, Tabs, Dropdown, Form ครบ + หลายหน้า sample
- 4) Other (please specify): _______

**Answer**: 2) + light/dark mode button toggle

---

### D1-7: การยืนยันค่าสีแบรนด์ (source of truth)
**Question**: จะ lock ค่าสีอย่างไร?
- 1) ใช้ค่าประมาณจากโลโก้ที่ mark ไว้ไปก่อน ปรับทีหลัง
- 2) ยืนยันด้วย brand guide/ไฟล์ vector ต้นฉบับก่อน lock **(Recommended)**
- 3) ให้ผม pixel-sample จากไฟล์โลโก้ให้ละเอียดเพื่อได้ค่าใกล้จริงสุด
- 4) Other (please specify): _______

**Answer**: 2) ยืนยันด้วย brand guide/ไฟล์ vector ต้นฉบับก่อน lock

---

### D1-8: Personas (บังคับถาม)
**Question**: ต้องการสร้าง persona ไหม?
- 1) ไม่ต้อง — ผู้ใช้เป็น developer ภายในกลุ่มเดียว **(Recommended)**
- 2) ต้องการ — แยก persona (starter user / common maintainer / team lead)
- 3) Other (please specify): _______

**Answer**: 1) ไม่ต้อง — developer ภายในกลุ่มเดียว

---

### D1-9: ขนาดทีม (บังคับถาม)
**Question**: มี developer กี่คนทำโปรเจกต์นี้?
- 1) Solo (1 คน)
- 2) ทีมเล็ก (2–3)
- 3) ทีมกลาง (4–8)
- 4) ทีมใหญ่ (9+)

**Answer**: 4)

---

## Decisions Summary
<!-- Auto-populated หลังผู้ใช้ตอบ -->
- D1-1 v1 Scope: ของกลาง + generator + template ครบทุก stack + component พื้นฐาน
- D1-2 Target Stacks: Go monolith, Next.js, Nest.js, Express.js (ครบ 4 — nest.js ยืนยัน)
- D1-3 Generator Mechanism: Node CLI (`npx create-i24`, interactive prompt)
- D1-4 Scaffold Output: สร้างโฟลเดอร์โปรเจกต์ใหม่แยก (ตัด git history)
- D1-5 Common Layer Scope: tokens+theme + UI component + shared backend util/config/convention (FE&BE)
- D1-6 Component Set: Core+layout/nav (Button, Badge, Card, Input, Table, Nav/Header, Alert) + sample page + light/dark mode toggle
- D1-7 Color SoT: ยืนยันด้วย brand guide/vector ต้นฉบับก่อน lock
- D1-8 Personas: ไม่ต้อง (developer ภายในกลุ่มเดียว)
- D1-9 Team Size: ทีมใหญ่ (9+)

<!-- Validation notes -->
- D1-5 หมายเหตุ: recommended คือ option 2 (frontend UI) แต่เลือก option 3 ให้ตรง requirement เดิม "template/component ทั้ง frontend/backend กลาง"
- D1-6 เพิ่ม dark mode → ของกลาง theme ต้องรองรับ light/dark (เพิ่ม token ชั้น semantic)

## Validation Resolution (Broad Scope → phased + boundaries)
**Phase v1 (MVP)**
- Common layer: design tokens (light/dark semantic) + brand theme (Tailwind v4)
- Component พื้นฐาน: Button, Badge, Card, Input, Table, Nav/Header, Alert + dark mode toggle + sample page
- Generator (Node CLI `npx create-i24`) รองรับ 2 stack: Go monolith + Next.js
- Prototype/preview page (swatch สี + components)

**Phase v1.1**
- Backend templates: Nest.js, Express.js + shared backend util/config/convention

**Out-of-scope (v1)**
- ยังไม่ publish เป็น package จริง (ใช้โหมด clone/monorepo ก่อน)
- ยังไม่มี docs site เต็มรูปแบบ
- Backend template = โครง+convention+shared util (ยังไม่รวม auth/DB/ORM สำเร็จรูป)
- ยังไม่รองรับ i18n, ยังไม่มี CI auto-publish

---

**Instructions**: เติมคำตอบด้านบนแล้วพิมพ์ "done" (หรือ "use recommendations" ให้เติมตัวเลือกแนะนำอัตโนมัติ)
