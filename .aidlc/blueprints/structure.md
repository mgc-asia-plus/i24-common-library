# Structure — i24-common-library

## Summary
- **Repo type**: documentation repo (Markdown เป็นหลัก)
- **Key dir**: `docs/` เก็บมาตรฐานทั้งหมด แยกตามหมวด
- **Entry point**: `docs/README.md` (สารบัญ + วิธีใช้)
- **Brand module**: `docs/brand/{palette,design-tokens,theme-tailwind,effects}.md` — foundation `brand-theme`
- **UI module**: `docs/components/` (14 specs) + `prototype/index.html` — unit `ui-components`
- **Delivery module**: `docs/stacks/` + `docs/conventions/` + `docs/scaffolding.md` — unit `delivery-guides`

## Repository
- **Type**: Single repo (เอกสาร)
- **Root**: `README.md` ภาพรวม + ชี้ไป `docs/`

## Proposed Documentation Tree (v1)
```
docs/
  README.md                 สารบัญ + วิธีใช้ common library
  brand/
    palette.md              SSOT สี — Navy Solid + Frosted Gray Glass + Deep Crimson + contrast AA
    design-tokens.md        tokens 2 ชั้น: Primitive → Semantic (light/dark)
    theme-tailwind.md       map tokens → Tailwind v4 `@theme` + CSS variables + `[data-theme]` (snippet สั้น)
    effects.md              SSOT สูตร glass/gradient — component อ้างสูตร ห้ามคิดค่าเอง
  components/
    README.md               รายการ component + หลักการ/สถานะ/accessibility ร่วม
    button.md
    badge.md
    card.md
    input.md
    table.md                `.mac-table` ใน `.mac-table-wrap` / `.mac-section`
    nav-header.md
    sidebar.md              `.mac-sidebar` — พื้นไม่สลับ theme
    alert.md
    theme-mode.md           สลับ light/dark (`[data-theme]`)
    footer.md               บังคับ "Powered by i24"
    modal.md
    select.md
    toast.md
    pagination.md
  stacks/
    go-monolith.md          โครง + convention + วิธีต่อ theme (Chi+HTMX+Tailwind)
    nextjs.md               โครง frontend + วิธีต่อ theme/tokens
    nestjs.md               โครง backend + convention + config
    expressjs.md            โครง backend + convention + config
  conventions/
    project-structure.md
    naming.md
    git.md
    json-api.md
  scaffolding.md            checklist เริ่มโปรเจกต์ใหม่ทีละ stack (แทน generator)
prototype/index.html        gallery รวม token + component
CHANGELOG.md
```

## Notes
- แต่ละ component spec ใช้เทมเพลต 8 หัวข้อ: Purpose → Anatomy → Variants → Sizes → States → Tokens used → Accessibility → Reference snippet (HTML สั้น)
- Stack guides + conventions + scaffolding เป็นของ unit `delivery-guides` — ลิงก์กลับ brand/components ห้ามสำเนาตารางสี/anatomy
- ชุด stack ที่ล็อก: Go monolith, Next.js, Nest.js, Express.js — ไม่มี generator
- ไม่มี build artifact — เป็นเอกสารล้วน
