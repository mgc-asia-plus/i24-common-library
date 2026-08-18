# Structure — i24-common-library

## Summary
- **Repo type**: documentation repo (Markdown เป็นหลัก)
- **Key dir**: `docs/` เก็บมาตรฐานทั้งหมด แยกตามหมวด
- **Entry point**: `docs/README.md` (สารบัญ + วิธีใช้)

## Repository
- **Type**: Single repo (เอกสาร)
- **Root**: `README.md` ภาพรวม + ชี้ไป `docs/`

## Proposed Documentation Tree (v1)
```
docs/
  README.md                 สารบัญ + วิธีใช้ common library
  brand/
    palette.md              สีจากโลโก้ (hex codes, marked) + usage + do/don't
    design-tokens.md        tokens: color/typography/spacing/radius/shadow + semantic light/dark
    theme-tailwind.md       วิธี map tokens → Tailwind v4 @theme (snippet สั้น)
  components/
    README.md               รายการ component + หลักการ/สถานะ/accessibility ร่วม
    button.md
    badge.md
    card.md
    input.md
    table.md
    nav-header.md
    alert.md
    theme-mode.md           สลับ light/dark (theme mode)
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
CHANGELOG.md
```

## Notes
- แต่ละ component spec ใช้เทมเพลตเดียวกัน: Anatomy → Variants → States → Tokens used → Accessibility → Reference snippet (สั้น ต่อ stack)
- Phase v1: brand + tokens + theme + components + stacks(go, nextjs) + conventions + scaffolding
- Phase v1.1: stacks(nestjs, expressjs) ลงรายละเอียด backend เต็ม
- ไม่มี build artifact — เป็นเอกสารล้วน
