# Decomposition Decisions (D2)

## Context Summary
- Greenfield / scope=new — **documentation-based common library** (deliverable = `.md` ไม่ใช่ code generator)
- ไม่มี `requirements.md` ใช้ Key Features จาก `product.md` + D1 (pivot) เป็นขอบเขตงาน
- โดเมนที่มีอยู่แล้วใน `docs/`: brand/tokens, components, stacks, conventions, scaffolding, prototype
- ทีมใหญ่ (9+), Personas ไม่ทำ
- เอกสารชุดแรกส่งแล้ว — D2 ใช้จัดขอบเขต units สำหรับดูแล/ขยายต่อ ไม่ใช่เริ่มจากศูนย์
- ห้ามตัดสิน tech stack ในเฟสนี้ (เป็นงานของ design)

**งานที่ต้องจัด units (จาก Key Features):**
| ID | Feature | โดเมน |
|----|---------|--------|
| F-brand | Brand & color (palette จากโลโก้) | brand |
| F-tokens | Design tokens (color/type/spacing + semantic light/dark) | brand |
| F-theme | Theme guide (map → Tailwind v4 `@theme`) | brand |
| F-effects | Effects (gradient + glass) | brand |
| F-components | Component specs (anatomy/variants/states/a11y) | components |
| F-stacks | Stack setup guides (Go monolith / Next.js / Nest.js / Express.js) | stacks |
| F-conventions | Conventions (structure, naming, git, JSON API) | conventions |
| F-scaffolding | Scaffolding checklist เริ่มโปรเจกต์ | delivery |
| F-prototype | Preview gallery (`prototype/index.html`) | prototype |

---

## Decision Questions

### D2-1: ความจำเป็นในการแยก units
**Question**: เอกสารมีหลายหมวดและทีมใหญ่ — ควรแยกเป็น units หรือถือเป็นชุดเดียว?
- 1) แยกเป็น units ตามโดเมนเอกสาร (brand / components / guides) เพื่อ ownership ชัด **(Recommended)**
- 2) ไม่แยก — ชุดเอกสารทั้ง repo เป็น unit เดียว (ข้าม decomposition)
- 3) แยกเฉพาะงานที่ยังไม่นิ่ง (เช่น components v1.2 + stacks) ที่เหลือถือว่าเสร็จแล้ว
- 4) Other (please specify): _______

**Answer**: 1) แยกเป็น units ตามโดเมนเอกสาร (brand / components / guides) เพื่อ ownership ชัด

---

### D2-2: รูปแบบโครงสร้างระบบ (architecture pattern)
**Question**: จัดขอบเขตของ common library แบบไหน? (ยังไม่เลือก stack)
- 1) Modular Monolith — repo เอกสารเดียว แยกโมดูลตามหมวด (`docs/brand`, `docs/components`, …) **(Recommended)**
- 2) Single Unit — ไม่แบ่งโมดูล เอกสารรวมกองเดียว
- 3) Distributed — แยก repo ตามหมวด (brand คนละ repo กับ components)
- 4) Other (please specify): _______

**Answer**: 1) Modular Monolith — repo เอกสารเดียว แยกโมดูลตามหมวด (`docs/brand`, `docs/components`, …)

---

### D2-3: กลยุทธ์การแยก (decomposition strategy)
**Question**: ใช้หลักอะไรตัดขอบเขต units?
- 1) Domain-Driven — ตามโดเมนเอกสาร: brand-theme, ui-components, delivery-guides **(Recommended)**
- 2) Layer-Based — ตามชั้นทางเทคนิค: tokens / specs / stack adapters
- 3) User Journey-Based — ตามวิธีใช้: เริ่มโปรเจกต์ใหม่ / สร้าง UI / review มาตรฐาน
- 4) Other (please specify): _______

**Answer**: 1) Domain-Driven — ตามโดเมนเอกสาร: brand-theme, ui-components, delivery-guides

---

### D2-4: Foundation unit (ของกลางที่ทุก unit ยึด)
**Question**: ต้องมี foundation unit ไหม? tokens เป็น SSOT ที่ component/stack/prototype อ้างอิง
- 1) ใช่ — unit `brand-theme` เป็น foundation (palette + tokens + theme + effects) ทำก่อนเสมอ **(Recommended)**
- 2) ใช่ แต่ foundation = โครง repo (`README`, `docs/README`, CHANGELOG, หลักการเขียนเอกสาร) ไม่ใช่ brand
- 3) ไม่ต้อง — แต่ละ unit พึ่งกันแบบ customer/supplier โดยไม่มี foundation แยก
- 4) Other (please specify): _______

**Answer**: 1) ใช่ — unit `brand-theme` เป็น foundation (palette + tokens + theme + effects) ทำก่อนเสมอ

---

### D2-5: ชุด units และงานที่ผูก
**Question**: ยืนยันชุด units นี้ไหม?
- 1) 3 units **(Recommended)**
  - `brand-theme`: F-brand, F-tokens, F-theme, F-effects
  - `ui-components`: F-components, F-prototype
  - `delivery-guides`: F-stacks, F-conventions, F-scaffolding
- 2) 4 units — แยก `prototype-gallery` ออกจาก `ui-components`
- 3) 5 units — ตามโฟลเดอร์ปัจจุบัน: `brand` / `components` / `stacks` / `conventions` / `prototype`
- 4) Other (please specify): _______

**Answer**: 1) 3 units — `brand-theme` (F-brand, F-tokens, F-theme, F-effects) / `ui-components` (F-components, F-prototype) / `delivery-guides` (F-stacks, F-conventions, F-scaffolding)

---

### D2-6: ความสัมพันธ์ระหว่าง units (dependencies)
**Question**: units ต่อกันอย่างไร?
- 1) Customer/Supplier ทางเดียว: `brand-theme` → `ui-components` → `delivery-guides` (ห้ามวนกลับ; ค่าสี/token อยู่ที่ brand ที่เดียว) **(Recommended)**
- 2) Shared Kernel — มีชุด token กลางแยก pack ให้ทุก unit copy
- 3) ต่างคนต่างเดิน — แต่ละ unit มีสำเนา palette/token ของตัวเอง
- 4) Other (please specify): _______

**Answer**: 1) Customer/Supplier ทางเดียว: `brand-theme` → `ui-components` → `delivery-guides` (ห้ามวนกลับ; ค่าสี/token อยู่ที่ brand ที่เดียว)

---

### D2-7: ลำดับพัฒนา (development sequence)
**Question**: ลำดับส่งมอบ units ควรเป็นอย่างไร?
- 1) `brand-theme` → `ui-components` (รวม prototype) → `delivery-guides` **(Recommended)**
- 2) `brand-theme` กับ `ui-components` ขนานได้เลย แล้วค่อย `delivery-guides`
- 3) ทำ `delivery-guides` ก่อน (ทีมเริ่มโปรเจกต์ใหม่ได้เร็ว) แล้วค่อย lock brand/components
- 4) Other (please specify): _______

**Answer**: 1) `brand-theme` → `ui-components` (รวม prototype) → `delivery-guides`

---

## Decisions Summary
<!-- Machine-readable compact summary. Downstream phases: read ONLY this section. -->
- D2-1 Decomposition Need: แยกเป็น units ตามโดเมนเอกสาร (brand / components / guides)
- D2-2 Architecture Pattern: Modular Monolith — repo เอกสารเดียว แยกโมดูลตามหมวด
- D2-3 Decomposition Strategy: Domain-Driven — brand-theme, ui-components, delivery-guides
- D2-4 Foundation Unit: brand-theme (palette + tokens + theme + effects) เป็น foundation ทำก่อนเสมอ
- D2-5 Unit Set: 3 units — brand-theme (F-brand, F-tokens, F-theme, F-effects); ui-components (F-components, F-prototype); delivery-guides (F-stacks, F-conventions, F-scaffolding)
- D2-6 Dependencies: Customer/Supplier ทางเดียว brand-theme → ui-components → delivery-guides; token SSOT ที่ brand ที่เดียว
- D2-7 Development Sequence: brand-theme → ui-components (รวม prototype) → delivery-guides

---

**Instructions**: Fill in your answers above and respond with "done"
