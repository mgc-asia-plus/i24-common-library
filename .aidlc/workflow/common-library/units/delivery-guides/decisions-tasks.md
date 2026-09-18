# Tasks Decisions (D4) — unit: delivery-guides

## Context Summary
- Unit: `delivery-guides` (domain) — design compact อนุมัติแล้ว
- 3 components: StackGuideSet, ConventionSet, ScaffoldingChecklist
- 6 entities / 3 document contracts / ไม่มี HTTP, ไม่มี DB, ไม่มี test runner, ไม่มี generator
- ล็อก 4 stack (Go / Next / Nest / Express) + 4 convention + `docs/scaffolding.md` (ไฟล์มีอยู่แล้ว — งานคือให้ชี้ SSOT, ไม่มี hex ล้วน, footer ใน UI path)
- D3: review 5 properties ตอน PR; CHANGELOG; merge main = ปล่อย; ลิงก์กลับ brand/components
- Upstream `brand-theme` และ `ui-components` เสร็จแล้ว

---

## Decision Questions

### D4-1: Task breakdown strategy
**Question**: จะแตกงาน `delivery-guides` อย่างไร?
- 1) ตาม design component: กลุ่ม stack guides → conventions → scaffolding แล้วค่อย review + CHANGELOG **(Recommended)**
- 2) หนึ่งงานต่อไฟล์ (4 stack + 4 convention + scaffolding = 9+ งาน)
- 3) กองเดียว — แก้ docs/stacks + conventions + scaffolding ใน 1 งาน
- 4) Other (please specify): _______

**Answer**: 1) ตาม design component: กลุ่ม stack guides → conventions → scaffolding แล้วค่อย review + CHANGELOG

---

### D4-2: Implementation approach
**Question**: ลำดับเขียนกับตรวจของคุณสมบัติ (D3-8 ไม่มี test runner)?
- 1) จัดเอกสารก่อน แล้วปิดท้ายด้วย review checklist (theme pointer / convention ครบ / scaffolding ต่อ stack / no orphan hex / footer) **(Recommended)**
- 2) TDD — เขียนตารางคุณสมบัติให้ fail ก่อน แล้วค่อยปะเอกสารให้ผ่าน
- 3) ไม่มีขั้นตรวจ — ส่งเอกสารอย่างเดียว
- 4) Other (please specify): _______

**Answer**: 1) จัดเอกสารก่อน แล้วปิดท้ายด้วย review checklist (theme pointer / convention ครบ / scaffolding ต่อ stack / no orphan hex / footer)

---

### D4-3: Component priority
**Question**: ทำ component ไหนก่อน?
- 1) StackGuideSet → ConventionSet → ScaffoldingChecklist **(Recommended)** — checklist อ้างทั้งสองชุด
- 2) ConventionSet ก่อน แล้วค่อย stack
- 3) ScaffoldingChecklist ก่อน แล้วไล่ guide ให้ตรง checklist
- 4) Other (please specify): _______

**Answer**: 1) StackGuideSet → ConventionSet → ScaffoldingChecklist

---

### D4-4: Integration strategy
**Question**: จัดการลิงก์ไป `brand-theme` / `ui-components` ตอนไหน?
- 1) ใส่ลิงก์ SSOT ตอนเขียนแต่ละชุด; ไม่แก้ไฟล์ brand/components ใน unit นี้; งานท้ายคือ CHANGELOG **(Recommended)**
- 2) แก้ `docs/brand/` และ spec component ใน unit นี้ถ้าเจอ hex
- 3) ไม่แตะ CHANGELOG / ไม่ตรวจ hex ใน guide
- 4) Other (please specify): _______

**Answer**: 1) ใส่ลิงก์ SSOT ตอนเขียนแต่ละชุด; ไม่แก้ไฟล์ brand/components ใน unit นี้; งานท้ายคือ CHANGELOG

---

### D4-5: Testing strategy
**Question**: งานตรวจอะไรบ้างใน unit นี้?
- 1) Review checklist ตาม 5 properties ใน design (ไม่เพิ่มสคริปต์/CI) **(Recommended)**
- 2) เพิ่มสคริปต์ parse markdown ตรวจใน CI
- 3) ไม่มีงานตรวจ
- 4) Other (please specify): _______

**Answer**: 1) Review checklist ตาม 5 properties ใน design (ไม่เพิ่มสคริปต์/CI)

---

### D4-6: Task granularity
**Question**: ขนาดงานต่อข้อ?
- 1) 1 concern ต่องาน — กลุ่ม stack คนละงานกับ conventions, scaffolding คนละงาน, review คนละงาน **(Recommended)**
- 2) Atomic — แยกเป็นรายไฟล์ทั้ง 9
- 3) Multi-concern — รวม guides + conventions + scaffolding ใน 2 งาน
- 4) Other (please specify): _______

**Answer**: 1) 1 concern ต่องาน — กลุ่ม stack คนละงานกับ conventions, scaffolding คนละงาน, review คนละงาน

---

### D4-7: Parallel work
**Question**: รันงานขนานได้ไหม?
- 1) ลำดับตาม dependency; ขนานได้เฉพาะกลุ่ม stack กับ conventions (ไฟล์ไม่ซ้อน) แล้วค่อย scaffolding **(Recommended)**
- 2) ขนานทั้ง stack + conventions + scaffolding พร้อมกัน (เสี่ยง checklist ไม่ตรง)
- 3) ทำทีละงานทั้งชุด ไม่ขนาน
- 4) Other (please specify): _______

**Answer**: 1) ลำดับตาม dependency; ขนานได้เฉพาะกลุ่ม stack กับ conventions (ไฟล์ไม่ซ้อน) แล้วค่อย scaffolding

---

## Decisions Summary
<!-- Machine-readable compact summary. Downstream phases: read ONLY this section. -->
- D4-1 Breakdown Strategy: ตาม design component — stack guides → conventions → scaffolding แล้ว review + CHANGELOG
- D4-2 Implementation Approach: จัดเอกสารก่อน แล้วปิดท้ายด้วย review checklist
- D4-3 Component Priority: StackGuideSet → ConventionSet → ScaffoldingChecklist
- D4-4 Integration Strategy: ใส่ลิงก์ SSOT ตอนเขียนแต่ละชุด; ไม่แก้ brand/components; CHANGELOG ท้าย
- D4-5 Testing Strategy: Review checklist ตาม 5 properties (ไม่เพิ่มสคริปต์/CI)
- D4-6 Task Granularity: 1 concern ต่องาน
- D4-7 Parallel Work: ขนาน stack guides กับ conventions แล้วค่อย scaffolding

---

**Instructions**: Fill in your answers above and respond with "done"
