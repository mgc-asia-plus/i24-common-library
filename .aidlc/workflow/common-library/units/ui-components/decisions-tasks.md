# Tasks Decisions (D4) — unit: ui-components

## Context Summary
- Unit: `ui-components` (domain) — design compact อนุมัติแล้ว
- 3 components: SpecIndex, SpecLibrary, PreviewGallery
- 7 entities / 3 document contracts / ไม่มี HTTP, ไม่มี DB, ไม่มี test runner
- แคตตาล็อก 14 spec ใน `docs/components/` + gallery `prototype/index.html` (ไฟล์มีอยู่แล้ว — งานคือตรวจให้ครบเทมเพลต 8 หัวข้อ / token / คลาส / footer / a11y)
- D3: review properties ตอน PR; footer บังคับ; ล็อก `.mac-sidebar` / `.mac-table`; snippet HTML สั้น; CHANGELOG; merge main = ปล่อย
- Upstream `brand-theme` เสร็จแล้ว — อ้างชื่อ token ห้าม hex ล้วน
- ทีมใหญ่ แต่ unit นี้เป็นเอกสาร + หน้า preview ที่ต้องเรียงตาม dependency

---

## Decision Questions

### D4-1: Task breakdown strategy
**Question**: จะแตกงาน `ui-components` อย่างไร?
- 1) ตาม design component: SpecIndex (README) → กลุ่ม spec → PreviewGallery แล้วค่อย review + CHANGELOG **(Recommended)** — ไม่แยก 14 งานต่อไฟล์
- 2) หนึ่งงานต่อ spec (14 งาน + README + prototype) — ละเอียดแต่ยาว
- 3) กองเดียว — แก้ `docs/components/` ทั้งโฟลเดอร์ + prototype ใน 1 งาน
- 4) Other (please specify): _______

**Answer**: 1) ตาม design component: SpecIndex (README) → กลุ่ม spec → PreviewGallery แล้วค่อย review + CHANGELOG

---

### D4-2: Implementation approach
**Question**: ลำดับเขียนกับตรวจของคุณสมบัติ (D3-8 ไม่มี test runner)?
- 1) จัดเอกสาร/prototype ก่อน แล้วปิดท้ายด้วย review checklist (Tokens+States / no orphan hex / คลาสตรง spec / footer) **(Recommended)**
- 2) TDD — เขียนตารางคุณสมบัติให้ fail ก่อน แล้วค่อยปะ spec ให้ผ่าน
- 3) ไม่มีขั้นตรวจ — ส่งเอกสารอย่างเดียว
- 4) Other (please specify): _______

**Answer**: 1) จัดเอกสาร/prototype ก่อน แล้วปิดท้ายด้วย review checklist (Tokens+States / no orphan hex / คลาสตรง spec / footer)

---

### D4-3: Component priority
**Question**: ทำ component ไหนก่อน?
- 1) SpecIndex (กฎร่วม) → SpecLibrary → PreviewGallery **(Recommended)** — prototype ตาม spec
- 2) PreviewGallery ก่อน แล้วค่อยไล่ spec ให้ตรงหน้า
- 3) SpecLibrary ทั้งชุดก่อน ไม่แตะ README จนจบ
- 4) Other (please specify): _______

**Answer**: 1) SpecIndex (กฎร่วม) → SpecLibrary → PreviewGallery

---

### D4-4: Integration strategy
**Question**: จัดการ dependency ของ `brand-theme` และ downstream ตอนไหน?
- 1) ยึด token/effects จาก `docs/brand/` ทั้งชุด; ไม่เขียน stack guide (ของ `delivery-guides`); งานท้ายคือ CHANGELOG **(Recommended)**
- 2) เริ่มจากแก้ `delivery-guides` ให้ชี้ spec ตั้งแต่ใน unit นี้
- 3) ไม่แตะ CHANGELOG / ไม่ตรวจ hex ข้ามไฟล์ — ปล่อยให้ unit อื่น
- 4) Other (please specify): _______

**Answer**: 1) ยึด token/effects จาก `docs/brand/` ทั้งชุด; ไม่เขียน stack guide (ของ `delivery-guides`); งานท้ายคือ CHANGELOG

---

### D4-5: Testing strategy
**Question**: งานตรวจอะไรบ้างใน unit นี้?
- 1) Review checklist ตาม 4 properties ใน design (ไม่เพิ่มสคริปต์/CI) **(Recommended)**
- 2) เพิ่มสคริปต์ parse markdown/HTML ตรวจใน CI
- 3) ไม่มีงานตรวจ
- 4) Other (please specify): _______

**Answer**: 1) Review checklist ตาม 4 properties ใน design (ไม่เพิ่มสคริปต์/CI)

---

### D4-6: Task granularity
**Question**: ขนาดงานต่อข้อ?
- 1) 1 concern ต่องาน — README คนละงานกับกลุ่ม spec, prototype คนละงาน, review คนละงาน **(Recommended)**
- 2) Atomic มาก — แยกเป็นรายไฟล์ spec ทั้ง 14
- 3) Multi-concern — รวม spec + prototype + review ใน 2 งาน
- 4) Other (please specify): _______

**Answer**: 1) 1 concern ต่องาน — README คนละงานกับกลุ่ม spec, prototype คนละงาน, review คนละงาน

---

### D4-7: Parallel work
**Question**: รันงานขนานได้ไหม?
- 1) ลำดับตาม dependency; หลัง README นิ่ง ขนานกลุ่ม spec ที่ไฟล์ไม่ซ้อน แล้วค่อย prototype **(Recommended)**
- 2) ขนาน README + ทุก spec + prototype พร้อมกัน (เสี่ยงกฎร่วมไม่ตรง)
- 3) ทำทีละงานทั้งชุด ไม่ขนาน
- 4) Other (please specify): _______

**Answer**: 1) ลำดับตาม dependency; หลัง README นิ่ง ขนานกลุ่ม spec ที่ไฟล์ไม่ซ้อน แล้วค่อย prototype

---

## Decisions Summary
<!-- Machine-readable compact summary. Downstream phases: read ONLY this section. -->
- D4-1 Breakdown Strategy: ตาม design component — SpecIndex → กลุ่ม spec → PreviewGallery แล้ว review + CHANGELOG
- D4-2 Implementation Approach: จัดเอกสาร/prototype ก่อน แล้วปิดท้ายด้วย review checklist
- D4-3 Component Priority: SpecIndex → SpecLibrary → PreviewGallery
- D4-4 Integration Strategy: ยึด token จาก docs/brand; ไม่เขียน delivery-guides; CHANGELOG ท้าย
- D4-5 Testing Strategy: Review checklist ตาม 4 properties (ไม่เพิ่มสคริปต์/CI)
- D4-6 Task Granularity: 1 concern ต่องาน
- D4-7 Parallel Work: หลัง README ขนานกลุ่ม spec ที่ไฟล์ไม่ซ้อน แล้วค่อย prototype

---

**Instructions**: Fill in your answers above and respond with "done"
