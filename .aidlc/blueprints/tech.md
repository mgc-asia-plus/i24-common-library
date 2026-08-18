# Tech — i24-common-library

## Summary
- **Nature**: documentation-based common library — deliverable เป็นไฟล์ `.md` ทั้งหมด (ไม่ใช่ code generator / ไม่เก็บ template code หลายชุด)
- **Format**: Markdown + ตาราง + code snippet สั้น ๆ เพื่ออธิบาย (ไม่ใช่ code ที่ต้อง build)
- **Documented stacks**: Go monolith (Chi+HTMX+Tailwind v4), Next.js, Nest.js, Express.js — อธิบายเป็นแนวทาง ไม่ใช่โค้ดสำเร็จ

## Stack (ของตัว repo)
- **Content**: Markdown (`.md`)
- **Build System**: ไม่มี — เป็นเอกสารล้วน (อาจเพิ่ม static docs site ภายหลัง = out-of-scope v1)
- **Tooling (optional)**: markdown linter, preview ใน editor
- **Versioning**: git + CHANGELOG.md

## Content Architecture
- **SSOT**: brand/tokens ระบุค่าเป็นเอกสารเดียว → stack guides อ้างอิงกลับมา
- **โครงเอกสาร**: brand → tokens → theme → components → stacks → conventions → scaffolding
- **Code snippet policy**: ใส่เท่าที่จำเป็นเพื่ออธิบาย (เช่น ตัวอย่าง `@theme` block, class ที่ควรใช้) — ห้ามกลายเป็น template code ครบชุดที่ต้อง maintain

## Documented Stacks (อธิบายเป็นแนวทาง)
| Stack | เลเยอร์ | เอกสารครอบคลุม |
|-------|--------|----------------|
| Go (monolith) | full-stack SSR | โครงโปรเจกต์, วิธีต่อ Tailwind theme + `go:embed`, HTMX partial convention |
| Next.js | frontend | โครง, วิธีต่อ theme/tokens, การจัด component |
| Nest.js | backend | โครง module, convention, config/env |
| Express.js | backend | โครง, convention, config/env |

## Conventions ที่จะทำเป็นเอกสาร
- naming, project structure, git workflow, JSON (snake_case), error handling — เขียนเป็น `.md` ใน `conventions/`
