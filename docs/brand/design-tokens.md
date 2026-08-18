# Design Tokens

โครง token 2 ชั้น: **Primitive** (ค่าดิบ) → **Semantic** (สื่อความหมาย, map ตาม theme mode)
Component อ้าง **semantic** เสมอ ไม่อ้าง primitive ตรง ๆ เพื่อให้สลับ light/dark ได้

> ค่าสี primitive ดึงจาก [`palette.md`](palette.md) (marked — รอยืนยัน)

## 1) Primitive tokens

### Color (ดู palette.md เป็น SSOT — ค่ายืนยันจากโลโก้แล้ว)
`brand-red-{50,100,400,500,600,700}` · `brand-coral-{300,400,500}` · `ink-{300,500,700,900}` · `white` · `paper` · `paper-muted` · `success/warning/danger/info-500`
ค่าหลัก (จาก `i24_LOGO.svg`): `brand-red-500 = #EC2129`, `brand-coral-400 = #F48569`, `white = #FFFFFF`

### Typography
| Token | ค่า | หมายเหตุ |
|-------|-----|----------|
| `font-sans` | `"Inter", "Noto Sans Thai", system-ui, sans-serif` | รองรับไทย |
| `font-mono` | `"JetBrains Mono", ui-monospace, monospace` | code |
| `text-xs` | 12px / 1.4 | |
| `text-sm` | 14px / 1.5 | |
| `text-base` | 16px / 1.6 | body default |
| `text-lg` | 18px / 1.6 | |
| `text-xl` | 20px / 1.4 | |
| `text-2xl` | 24px / 1.3 | heading |
| `text-3xl` | 30px / 1.25 | |
| `font-normal / medium / semibold / bold` | 400 / 500 / 600 / 700 | |

### Spacing (scale 4px)
`space-1=4` · `2=8` · `3=12` · `4=16` · `5=20` · `6=24` · `8=32` · `10=40` · `12=48` · `16=64` (px)

### Radius
| Token | ค่า |
|-------|-----|
| `radius-sm` | 4px |
| `radius-md` | 8px |
| `radius-lg` | 12px |
| `radius-xl` | 16px |
| `radius-pill` | 9999px (ปุ่ม/แท็บมุมมน, โทนโลโก้) |

### Shadow
| Token | ค่า |
|-------|-----|
| `shadow-sm` | `0 1px 2px rgba(0,0,0,.06)` |
| `shadow-md` | `0 2px 8px rgba(0,0,0,.10)` |
| `shadow-lg` | `0 8px 24px rgba(0,0,0,.14)` |

## 2) Semantic tokens (theme-aware)

Component ใช้ชื่อพวกนี้ ค่าจะเปลี่ยนตาม theme mode

| Semantic token | Light → primitive | Dark → primitive |
|----------------|-------------------|------------------|
| `color-bg` | `paper` `#FFFFFF` | `#0F1115` |
| `color-surface` | `paper-muted` `#F7F7F8` | `#171A21` |
| `color-border` | `ink-300` `#D1D5DB` | `#2A2F3A` |
| `color-text` | `ink-900` `#1A1A1A` | `#F3F4F6` |
| `color-text-muted` | `ink-500` `#6B7280` | `#9CA3AF` |
| `color-primary` | `brand-red-500` `#EC2129` | `brand-red-500` `#EC2129` |
| `color-primary-hover` | `brand-red-600` `#C81B22` | `brand-red-400` `#F04E52` |
| `color-on-primary` | `white` `#FFFFFF` | `white` `#FFFFFF` |
| `color-accent` | `brand-coral-400` `#F48569` | `brand-coral-300` `#F7A48A` |
| `color-danger` | `danger-500` `#DC2626` | `#F87171` |
| `color-success` | `success-500` `#16A34A` | `#4ADE80` |
| `color-focus-ring` | `brand-red-400` `#F04E52` | `brand-red-400` `#F04E52` |

> ค่าฝั่ง dark เป็นชุดเริ่มต้น (derived) — ปรับได้ตอนยืนยันแบรนด์ แต่ต้องคง contrast ให้ผ่าน AA

## กติกาใช้ token
- Component/หน้า → ใช้ **semantic** เท่านั้น (`color-primary`, `color-text`, …)
- Primitive แก้ที่ palette.md → semantic ที่นี่ → propagate ทุก component
- ห้าม hardcode hex ในโค้ด/CSS ของโปรเจกต์ปลายทาง
- theme mode (light/dark) ดู [`../components/theme-mode.md`](../components/theme-mode.md)
- การแปลงเป็น Tailwind ดู [`theme-tailwind.md`](theme-tailwind.md)
