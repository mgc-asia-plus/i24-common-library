# Tasks Decisions (D4) — unit: brand-theme

## Context Summary
- Unit: `brand-theme` (foundation) — design compact อนุมัติแล้ว (รวม edit: Navy `#0F172A`, sidebar/table tokens)
- 4 components: PaletteSSOT, TokenRegistry, ThemeMappingGuide, EffectsSSOT
- 6 entities / 4 document contracts / ไม่มี HTTP, ไม่มี DB, ไม่มี test runner
- งานหลัก: จัด `docs/brand/{palette,design-tokens,theme-tailwind,effects}.md` ให้เป็น SSOT + sync blueprints ที่ยัง drift (ชุดโลโก้แดงเก่า)
- D3: review properties ตอน PR; CHANGELOG; merge main = ปล่อย; อ้างชื่อ token ห้ามคัดลอก hex
- ทีมใหญ่ แต่ unit นี้เป็นเอกสารชุดเล็กที่ต้องเรียงตาม dependency

---

## Decision Questions

### D4-1: Task breakdown strategy
**Question**: จะแตกงาน `brand-theme` อย่างไร?
- 1) ตามไฟล์ SSOT — 1 งานต่อ `palette` / `design-tokens` / `theme-tailwind` / `effects` แล้วค่อย sync blueprint + CHANGELOG **(Recommended)**
- 2) ตามคุณสมบัติ correctness — งาน unique-names, งาน light/dark pairs, งาน contrast AA ข้ามไฟล์
- 3) กองเดียว — แก้ `docs/brand/` ทั้งชุดใน 1 งาน
- 4) Other (please specify): _______

**Answer**: 1) ตามไฟล์ SSOT — 1 งานต่อ `palette` / `design-tokens` / `theme-tailwind` / `effects` แล้วค่อย sync blueprint + CHANGELOG

---

### D4-2: Implementation approach
**Question**: ลำดับเขียนกับตรวจของคุณสมบัติ (D3-9 ไม่มี test runner)?
- 1) เขียนเอกสารก่อน แล้วปิดท้ายด้วย review checklist (unique names / light-dark / contrast AA / no hex leak) **(Recommended)**
- 2) TDD — เขียนตาราง contrast + รายการ token ที่ต้องมีก่อน แล้วค่อยเติมเอกสารให้ผ่าน
- 3) ไม่มีขั้นตรวจ — ส่งเอกสารอย่างเดียว
- 4) Other (please specify): _______

**Answer**: 1) เขียนเอกสารก่อน แล้วปิดท้ายด้วย review checklist (unique names / light-dark / contrast AA / no hex leak)

---

### D4-3: Component priority
**Question**: ทำ component ไหนก่อน?
- 1) PaletteSSOT → TokenRegistry → ThemeMappingGuide กับ EffectsSSOT (หลัง token พร้อม) **(Recommended)**
- 2) TokenRegistry ก่อน palette (นิยามชื่อก่อนค่อยใส่ค่า)
- 3) EffectsSSOT ก่อน เพราะ UI ติดแก้ว
- 4) Other (please specify): _______

**Answer**: 1) PaletteSSOT → TokenRegistry → ThemeMappingGuide กับ EffectsSSOT (หลัง token พร้อม)

---

### D4-4: Integration strategy
**Question**: จัดการ drift ของ `blueprints/product.md` และ `resources.md` (ชุดโลโก้แดงเก่า) ตอนไหน?
- 1) งานท้าย — หลัง 4 ไฟล์ brand นิ่งแล้ว sync blueprint ให้ชี้ `docs/brand/palette.md` **(Recommended)**
- 2) ทำเป็นงานแรก เพื่อตัดของเก่าก่อนแตะ docs
- 3) ไม่แตะ blueprint ใน unit นี้ — ปล่อยให้ unit อื่น
- 4) Other (please specify): _______

**Answer**: 1) งานท้าย — หลัง 4 ไฟล์ brand นิ่งแล้ว sync blueprint ให้ชี้ `docs/brand/palette.md`

---

### D4-5: Testing strategy
**Question**: งานตรวจอะไรบ้างใน unit นี้?
- 1) Review checklist ตาม 4 properties ใน design (ไม่เพิ่มสคริปต์/CI) **(Recommended)**
- 2) เพิ่มสคริปต์ parse markdown ตรวจ hex/contrast ใน CI
- 3) ไม่มีงานตรวจ
- 4) Other (please specify): _______

**Answer**: 1) Review checklist ตาม 4 properties ใน design (ไม่เพิ่มสคริปต์/CI)

---

### D4-6: Task granularity
**Question**: ขนาดงานต่อข้อ?
- 1) 1 concern ต่องาน (เช่น palette คนละงานกับ tokens) — ประมาณครึ่งวันถึง 1 วัน **(Recommended)**
- 2) Atomic มาก — แยกเป็นรายตาราง/ราย token
- 3) Multi-concern — รวม brand ทั้งโฟลเดอร์ใน 2 งาน
- 4) Other (please specify): _______

**Answer**: 1) 1 concern ต่องาน (เช่น palette คนละงานกับ tokens) — ประมาณครึ่งวันถึง 1 วัน

---

### D4-7: Parallel work
**Question**: รันงานขนานได้ไหม?
- 1) ลำดับตาม dependency; ขนานได้เฉพาะ `theme-tailwind.md` กับ `effects.md` หลัง tokens นิ่ง **(Recommended)**
- 2) ขนานทั้ง 4 ไฟล์เลย (เสี่ยงชื่อ token ไม่ตรง)
- 3) ทำทีละไฟล์ทั้งชุด ไม่ขนาน
- 4) Other (please specify): _______

**Answer**: 1) ลำดับตาม dependency; ขนานได้เฉพาะ `theme-tailwind.md` กับ `effects.md` หลัง tokens นิ่ง

---

## Decisions Summary
- D4-1 Breakdown Strategy: ตามไฟล์ SSOT — palette / design-tokens / theme-tailwind / effects แล้ว sync blueprint + CHANGELOG
- D4-2 Implementation Approach: เขียนเอกสารก่อน แล้วปิดท้ายด้วย review checklist
- D4-3 Component Priority: PaletteSSOT → TokenRegistry → ThemeMappingGuide ∥ EffectsSSOT
- D4-4 Integration Strategy: งานท้าย sync blueprints ให้ชี้ docs/brand/palette.md
- D4-5 Testing Strategy: Review checklist ตาม 4 properties (ไม่เพิ่มสคริปต์/CI)
- D4-6 Task Granularity: 1 concern ต่องาน
- D4-7 Parallel Work: ขนานได้เฉพาะ theme-tailwind กับ effects หลัง tokens นิ่ง

---

**Instructions**: Fill in your answers above and respond with "done"
