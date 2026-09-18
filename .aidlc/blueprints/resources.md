# External Resources

## Design Resources
- **Design tool**: none (ยังไม่ระบุ Figma/Sketch)
- **Design system docs**: none — จะสร้างในโปรเจกต์นี้
- **Wireframes/mockups**: none
- **Brand asset**: `i24_LOGO.svg` (workspace root) — โลโก้ทางการ; **อย่าดึง palette จากโลโก้** — SSOT สีอยู่ที่ `docs/brand/palette.md`

## Brand Palette (SSOT: `docs/brand/palette.md`)

ชุดโลโก้แดงเก่าไม่ใช่ primary อีกต่อไป — ยึด [`docs/brand/palette.md`](../../docs/brand/palette.md) (Navy Solid `#0F172A`)

| Token | Hex | บทบาท |
|-------|-----|-------|
| `primary-solid` / `--i24-primary` | `#0F172A` | **Navy Solid — สีหลัก** (ปุ่ม, pagination, พื้น `.mac-sidebar`) |
| `color-sidebar-bg` | `#0F172A` | พื้น sidebar — **ไม่สลับตาม theme** |
| `on-primary` | `#FFFFFF` | ข้อความบน Navy |
| canvas (`page-bg`) | `#F5F5F7` / `#0A0A0F` | พื้นหลัง light / dark |
| `brand-red` / `danger` | `#B0141B` | Deep Crimson — brand-red / danger **ไม่ใช่ primary** |

## API Resources
- **OpenAPI/Swagger**: none (library ไม่มี API)
- **GraphQL schema**: none
- **Existing API docs**: none

## Knowledge Resources
- **Documentation**: `docs/` — SSOT ที่ `docs/brand/palette.md` (หัวตาราง Cool Slate + สถานะตารางจาก i24-etax-service)
- **Reference implementations**: i24-etax-service (Go+Chi+HTMX+Tailwind v4) — เป็น consumer อ้างอิงฝั่ง Go

## Available Tools
- [ ] Design tool MCP server
- [x] Web search
- [ ] Other MCP servers: ___

## Notes
- ไฟล์ `.kiro/steering/{product,tech,structure,session-boot}.md` ปัจจุบันเป็นของ i24-etax-service (ก็อปติดมา) — ไม่ใช่ resource ของโปรเจกต์นี้ แนะนำลบ/แทนที่
