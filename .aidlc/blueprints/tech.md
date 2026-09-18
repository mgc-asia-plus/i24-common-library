# Tech — i24-common-library

## Summary
- **Nature**: documentation-based common library — deliverable เป็นไฟล์ `.md` ทั้งหมด (ไม่ใช่ code generator / ไม่เก็บ template code หลายชุด)
- **Format**: Markdown + ตาราง + code snippet สั้น ๆ เพื่ออธิบาย (ไม่ใช่ code ที่ต้อง build)
- **Brand SSOT**: Navy Solid + Frosted Gray Glass + Deep Crimson ที่ `docs/brand/` (foundation unit `brand-theme`)
- **Documented stacks**: Go monolith (Chi+HTMX+Tailwind v4), Next.js, Nest.js, Express.js — อธิบายเป็นแนวทาง ไม่ใช่โค้ดสำเร็จ

## Stack (ของตัว repo)
- **Content**: Markdown (`.md`)
- **Build System**: ไม่มี — เป็นเอกสารล้วน (อาจเพิ่ม static docs site ภายหลัง = out-of-scope v1)
- **Tooling (optional)**: markdown linter, preview ใน editor
- **Versioning**: git + CHANGELOG.md
- **Repo**: Single repo เอกสาร — ไม่มี package manager / monorepo tool

## Brand / Theme (foundation — D3 brand-theme)
- **Canonical palette**: `docs/brand/palette.md` — Primary Navy Solid `#0F172A`, Secondary Frosted Gray Glass, Brand Accent Deep Crimson `#B0141B`
- **Token layers**: Primitive → Semantic (light/dark)
- **Theme mapping**: Tailwind CSS **4.3.3** `@theme` + CSS variables + `[data-theme="light"|"dark"]` (snippet อ้างอิงสั้น ไม่ใช่ template เต็ม)
- **Downstream rule**: อ้างชื่อ token เท่านั้น — ห้ามคัดลอก hex นอก `docs/brand/`
- **Effects**: `docs/brand/effects.md` เป็น SSOT ของสูตร glass/gradient
- **Contrast**: WCAG 2.1 AA สำหรับข้อความบนพื้นหลัก
- **Release**: merge `main` = ปล่อย; บันทึกใน CHANGELOG + PR

## UI Components (domain — D3 ui-components)
- **Catalog**: 14 specs ใน `docs/components/` (index = `README.md`) — หนึ่งไฟล์ต่อ component
- **Spec template**: Purpose → Anatomy → Variants → Sizes → States → Tokens used → Accessibility → Reference snippet
- **Preview**: static HTML `prototype/index.html` (ไม่ใช่ Storybook / docs site)
- **Shell classes**: `.mac-sidebar` / `.mac-table` / `.mac-table-wrap` / `.mac-section`
- **Footer**: "Powered by i24" บังคับทุกระบบที่มี UI
- **A11y**: WCAG 2.1 AA — focus ที่มองเห็น (`color-focus-ring`), keyboard, แตะ 40×40, role/aria
- **Snippets**: HTML สั้น (+ ชื่อคลาส React/Tailwind ได้) ไม่ใช่ template ครบชุด
- **Correctness**: review properties (ไม่ใช้ CI script)

## Delivery Guides (domain — D3 delivery-guides)
- **Stacks**: 4 — Go monolith, Next.js, Nest.js, Express.js (`docs/stacks/`)
- **Guide depth**: setup + วิธีต่อ theme/tokens + ลิงก์ spec — ไม่ใช่ template โค้ดครบชุด
- **Conventions**: `project-structure.md`, `naming.md`, `git.md`, `json-api.md` (envelope + `snake_case`)
- **Scaffolding**: checklist `docs/scaffolding.md` แยกขั้นต่อ stack — ไม่มี generator
- **Upstream**: ลิงก์ `docs/brand/` + `docs/components/` ห้ามสำเนาตารางสี/anatomy
- **Footer**: ขั้น "Powered by i24" บังคับในทุก stack ที่มี UI
- **Correctness**: review properties (ไม่ใช้ CI script)

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
