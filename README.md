# i24 Common Library

มาตรฐานกลางของ i24 ในรูป **เอกสาร** (documentation-based common library) — ไม่ใช่ code generator และไม่เก็บ template code หลายชุด

จุดประสงค์: ให้ทุกโปรเจกต์ i24 ยึด **แหล่งความจริงเดียว (SSOT)** เรื่องแบรนด์ สี design tokens component spec และ convention แล้วแต่ละทีมนำไป implement ตาม tech stack ของตัวเอง แก้มาตรฐานที่เอกสารกลางที่เดียว

## เริ่มที่ไหน
- อ่าน [`docs/README.md`](docs/README.md) เป็นสารบัญหลัก
- เริ่มโปรเจกต์ใหม่: ดู [`docs/scaffolding.md`](docs/scaffolding.md)
- สีแบรนด์: ดู [`docs/brand/palette.md`](docs/brand/palette.md)

## หมวดเอกสาร
| หมวด | เนื้อหา |
|------|---------|
| `docs/brand/` | สีจากโลโก้, design tokens, การทำ Tailwind theme |
| `docs/components/` | spec ของแต่ละ UI component |
| `docs/stacks/` | แนวทาง setup + convention ต่อ tech stack |
| `docs/conventions/` | naming, project structure, git, JSON/API |
| `docs/scaffolding.md` | checklist เริ่มโปรเจกต์ใหม่ |

## Documented stacks
Go monolith (Chi + HTMX + Tailwind v4) · Next.js · Nest.js · Express.js

## สถานะ
- **v1**: brand, tokens, theme, components, conventions, scaffolding, stacks (go-monolith, nextjs)
- **v1.1**: backend เต็ม (nestjs, expressjs) — เสร็จแล้ว

> ค่าสีแบรนด์ยืนยันจากไฟล์ vector ทางการ `i24_LOGO.svg` (`brand-red-500 #EC2129`, `coral-400 #F48569`, `white #FFFFFF`). SSOT ของสีอยู่ที่ [`docs/brand/palette.md`](docs/brand/palette.md)

ดูประวัติการเปลี่ยนแปลงที่ [`CHANGELOG.md`](CHANGELOG.md)
