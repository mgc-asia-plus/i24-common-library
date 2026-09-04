# Design Tokens — Luxury Clear Glass

โครง token 2 ชั้น: **Primitive** (ค่าดิบ) → **Semantic** (สื่อความหมาย, map ตาม theme mode)
Component อ้าง **semantic** เสมอ เพื่อสลับ light/dark ได้
> sync จาก `prototype/index.html`; สี SSOT อยู่ที่ [`palette.md`](palette.md); effect (glass/gradient) ที่ [`effects.md`](effects.md)

## 1) Primitive tokens

### Color
- **red** (brand): `red-500 #EC2129` ✅, `red-600 #B0141B`, `red-700 #7E0E14`
- **navy** (accent): `navy-400 #2E4EA6`, `navy-500 #1E3A8A`, `navy-600 #152C63`
- **slate/ink**: `ink-900 #1A1D24`, `ink-700 #333A46`, `ink-500 #6B7482`, `ink-300 #D2D7DF`, `black #0A0C11`, `white #FFFFFF`
- **gold**: `#A8811C` (light) / `#E7C873` (dark)
- **status**: danger `#C1121F`, success `#137A47`, warning `#B7791F`, info `#1E3A8A`

### Typography
| Token | ค่า | หมายเหตุ |
|-------|-----|----------|
| `font-sans` | `-apple-system, BlinkMacSystemFont, "Inter", "Noto Sans Thai", system-ui, sans-serif` | Mac/iOS = SF Pro; อื่น ๆ = Inter (ละติน) + Noto Sans Thai (ไทย) |
| `font-mono` | `"JetBrains Mono", ui-monospace, monospace` | code |
| `text-xs…3xl` | 12 / 14 / 16 / 18 / 20 / 24 / 30 px | heading letter-spacing `-.02em` |
| `font-normal…extrabold` | 400 / 500 / 600 / 700 / 800 | 800 สำหรับ display/KPI |

> **Web fonts**: โหลด Inter + Noto Sans Thai (Google Fonts `display=swap` + `preconnect`) หรือ self-host `@font-face`. ตัวอย่างใน `prototype/index.html`

### Spacing (scale 4px)
`space-1=4` · `2=8` · `3=12` · `4=16` · `5=20` · `6=24` · `8=32` · `10=40` · `12=48` · `16=64` (px)

### Radius
`radius-sm 12px` · `radius-md 8px` · `radius (default) 20px` · `radius-pill 9999px`

## 2) Semantic tokens (theme-aware)

| Semantic token | Light | Dark |
|----------------|-------|------|
| `color-text` | `#1A1D24` | `#EDEFF4` |
| `color-text-muted` | `#5C6675` | `#98A1B2` |
| `color-bg` | `#FFFFFF` | `#0F1115` |
| `color-surface` | `#F4F6F9` | `#171A21` |
| `color-border` | `ink-300 #D2D7DF` | `#2A2F3A` |
| `color-primary` | `red-500 #EC2129` | `#EC2129` |
| `color-on-primary` | `#FFFFFF` | `#FFFFFF` |
| `color-accent` | `navy-500 #1E3A8A` | `#7C93E0` |
| `color-focus-ring` | `navy-400 #2E4EA6` | `#7C93E0` |
| `color-gold` | `#A8811C` | `#E7C873` |
| `color-danger` | `#C1121F` | `#F1616B` |
| `color-success` | `#137A47` | `#3BB273` |
| `color-warning` | `#B7791F` | `#D6A24A` |
| `color-info` | `#1E3A8A` | `#7C93E0` |
| `page-bg` | `#EEF0F4` | `#0A0C11` |

> ค่าฝั่ง dark เป็นชุดสำหรับ luxury dark — คง contrast ให้ผ่าน AA

## 3) Effect tokens (clear glass + gradient)
ค่าเต็ม + recipe + a11y อยู่ที่ [`effects.md`](effects.md)
- `grad-brand` (`#E11D27 → #A81319`), `grad-accent` (`#2A4AA0 → #152C63`), `grad-brand-soft`
- `glass-tint / sheen / top / gloss` (เคลือบเงา 4 ชั้น), `glass-bg`, `glass-bg-strong`, `glass-border`, `glass-hairline`, `glass-shadow`, `glass-blur 3px`
- `blob-red / blob-blue / blob-gray` (ambient background)

## กติกาใช้ token
- Component/หน้า → ใช้ **semantic** เท่านั้น (ห้าม hardcode hex)
- gradient เฉพาะ element (ปุ่ม/badge/โลโก้) — ห้ามที่ bg หน้า/ตัวหนังสือ
- surface หลัก (card/nav/footer/ปุ่มรอง) = clear glass
- theme mode ดู [`../components/theme-mode.md`](../components/theme-mode.md); Tailwind ดู [`theme-tailwind.md`](theme-tailwind.md)
