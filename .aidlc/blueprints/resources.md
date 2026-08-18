# External Resources

## Design Resources
- **Design tool**: none (ยังไม่ระบุ Figma/Sketch)
- **Design system docs**: none — จะสร้างในโปรเจกต์นี้
- **Wireframes/mockups**: none
- **Brand asset**: `i24_LOGO.png` (workspace root) — ใช้ดึง brand palette

## Brand Palette (จากไฟล์ vector ทางการ i24_LOGO.svg)
> ✅ red-500/coral-400/white ยืนยันจากโลโก้แล้ว; เฉดอื่น derived. หากมี brand guide ทางการ ให้ยึดแทน

```jsonc
{
  "brand": {
    "red":   { "50": "#FDECED", "100": "#FBD0D2", "400": "#F04E52", "500": "#EC2129", "600": "#C81B22", "700": "#AA171D" },
    "coral": { "300": "#F7A48A", "400": "#F48569", "500": "#F1684D" }
  },
  "neutral": { "white": "#FFFFFF", "paper-muted": "#F7F7F8", "ink-500": "#6B7280", "ink-900": "#1A1A1A" }
}
```

| Token | Hex | บทบาท |
|-------|-----|-------|
| `brand-red-500` | `#EC2129` ✅ | สีหลัก (พื้นโลโก้), primary |
| `brand-red-600` | `#C81B22` | hover/active |
| `brand-red-400` | `#F04E52` | เน้นรอง |
| `brand-red-50` | `#FDECED` | tint พื้นหลัง |
| `brand-coral-400` | `#F48569` ✅ | accent (blob โลโก้) |
| `brand-coral-300` | `#F7A48A` | accent อ่อน |
| `white` | `#FFFFFF` | text บนพื้นแดง / card |
| `ink-900` | `#1A1A1A` | ข้อความหลัก |
| `ink-500` | `#6B7280` | ข้อความรอง |
| `paper-muted` | `#F7F7F8` | surface |

## API Resources
- **OpenAPI/Swagger**: none (library ไม่มี API)
- **GraphQL schema**: none
- **Existing API docs**: none

## Knowledge Resources
- **Documentation**: none yet
- **Reference implementations**: i24-etax-service (Go+Chi+HTMX+Tailwind v4) — เป็น consumer อ้างอิงฝั่ง Go

## Available Tools
- [ ] Design tool MCP server
- [x] Web search
- [ ] Other MCP servers: ___

## Notes
- ไฟล์ `.kiro/steering/{product,tech,structure,session-boot}.md` ปัจจุบันเป็นของ i24-etax-service (ก็อปติดมา) — ไม่ใช่ resource ของโปรเจกต์นี้ แนะนำลบ/แทนที่
