# i24 Common Library — สารบัญ

เอกสารมาตรฐานกลางของ i24 ยึดเป็น single source of truth (SSOT)

## วิธีใช้เอกสารชุดนี้
1. **เริ่มโปรเจกต์ใหม่** → อ่าน [`scaffolding.md`](scaffolding.md) เลือก stack แล้วทำตาม checklist
2. **ตั้งธีม/สี** → [`brand/palette.md`](brand/palette.md) + [`brand/design-tokens.md`](brand/design-tokens.md) + [`brand/theme-tailwind.md`](brand/theme-tailwind.md)
3. **สร้าง UI** → เปิด spec ที่ [`components/`](components/README.md) แล้ว implement ตาม stack
4. **เขียนโค้ดให้ตรงมาตรฐาน** → [`conventions/`](conventions/project-structure.md)

## แผนผังเอกสาร

### Brand & Theme
| ไฟล์ | เนื้อหา |
|------|---------|
| [`brand/palette.md`](brand/palette.md) | สีจากโลโก้ พร้อม hex code + usage + do/don't |
| [`brand/design-tokens.md`](brand/design-tokens.md) | tokens ทั้งหมด (color/type/spacing/radius/shadow) + semantic light/dark |
| [`brand/theme-tailwind.md`](brand/theme-tailwind.md) | map tokens → Tailwind v4 `@theme` |

### Components
[`components/README.md`](components/README.md) — หลักการร่วม + รายการ
- [button](components/button.md) · [badge](components/badge.md) · [card](components/card.md) · [input](components/input.md) · [table](components/table.md) · [nav-header](components/nav-header.md) · [alert](components/alert.md) · [theme-mode](components/theme-mode.md) · [footer 🔒](components/footer.md)

### Stacks
- [go-monolith](stacks/go-monolith.md) — Chi + HTMX + Tailwind v4 *(v1)*
- [nextjs](stacks/nextjs.md) — frontend *(v1)*
- [nestjs](stacks/nestjs.md) — backend
- [expressjs](stacks/expressjs.md) — backend

### Conventions
- [project-structure](conventions/project-structure.md) · [naming](conventions/naming.md) · [git](conventions/git.md) · [json-api](conventions/json-api.md)

### Preview
- [`../prototype/index.html`](../prototype/index.html) — เปิดในเบราว์เซอร์เพื่อดู swatch สีจริง + ทุก component + toggle light/dark (ไฟล์เดียว ไม่ต้อง build)

### อื่น ๆ
- [scaffolding.md](scaffolding.md) — checklist เริ่มโปรเจกต์
- [../CHANGELOG.md](../CHANGELOG.md)

## หลักการ (principles)
- **SSOT**: ค่าจริง (สี/token) ระบุที่ `brand/` ที่เดียว — เอกสารอื่นอ้างอิงกลับมา ไม่ทำซ้ำค่า
- **อธิบายให้ชัด > เก็บโค้ด**: code snippet มีเท่าที่จำเป็นเพื่ออธิบาย ไม่ใช่ template ครบชุด
- **stack-agnostic ก่อน**: spec อธิบายพฤติกรรม/โครงสร้าง แล้วค่อยมีตัวอย่างต่อ stack
- **accessibility เป็น default**: ทุก component ระบุ a11y ขั้นต่ำ
