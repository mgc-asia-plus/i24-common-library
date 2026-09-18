# Design Tokens — Navy Solid & Frosted Gray Glass

โครงสร้าง token 2 ชั้น: **Primitive** (ค่าดิบ) → **Semantic** (สื่อความหมาย, map ตาม theme mode)

> Hex SSOT อยู่ที่ [`palette.md`](palette.md) — ไฟล์นี้ตั้งชื่อ token

---

## 1. Primitive Tokens

### Color: Navy Solid (Primary)
- `primary-navy: #0F172A` — ปุ่ม, pagination active, พื้น sidebar (ไม่สลับ theme)
- `primary-navy-hover: #06182B` (light)
- `primary-navy-hover-dark: #1D4B82` (dark)
- `on-primary: #FFFFFF`

### Color: Navy Translucent Glass (Option)
- `primary-glass-bg: rgba(15, 23, 42, 0.75)`
- `primary-glass-hover: rgba(15, 23, 42, 0.88)`
- `primary-glass-border: none`

### Color: Brand Red (Deep Crimson)
- `brand-red: #B0141B`
- `brand-red-hover: #8E1015`
- `brand-red-dark: #6B0C10`

### Color: Frosted Gray Glass
- `frosted-gray-light: rgba(0, 0, 0, 0.06)`
- `frosted-gray-dark: rgba(255, 255, 255, 0.12)`
- `frosted-gray-border: none`

### Color: White Translucent Glass (Card)
- `surface-light: rgba(255, 255, 255, 0.70)` + blur 24px
- `surface-dark: rgba(255, 255, 255, 0.07)` + blur 24px

### Color: Canvas & Neutrals
- `canvas-light: #F5F5F7`, `canvas-dark: #0A0A0F`
- `text-light: #1A1A1A`, `text-dark: #F3F4F6`
- `empty-text: #6E6E73`
- `text-muted-light: #6B7280`
- `text-muted-dark: #9CA3AF`

### Color: Cool Slate (หัวตารางเท่านั้น)
- `slate-200: #E2E8F0` — พื้นหัวตาราง light
- `slate-700: #334155` — ตัวอักษรหัวตาราง light
- `slate-header-bg-dark: rgba(255, 255, 255, 0.06)` — พื้นหัวตาราง dark (ตัวอักษร dark = `text-muted-dark`)

### Color: Gold (badge ทางเลือก)
- `gold-light: #A8811C`
- `gold-dark: #E7C873`

### Radius
| Token | ค่า | การใช้งาน |
| :--- | :--- | :--- |
| `radius-btn` / `radius-badge` / `radius-pill` | **9999px** | ปุ่ม, badge, pagination |
| `radius-card` | **20px** | การ์ดที่หุ้มตาราง / glass card |
| `radius-table` | **14px** | มุมกรอบ `.mac-table-wrap` เดี่ยว |
| `radius-sidebar-item` | **6px** | รายการเมนู sidebar |
| `radius-box` | 10px | input / กล่องทั่วไป |

### Typography
| Token | ค่า |
| :--- | :--- |
| `font-sans` | -apple-system, BlinkMacSystemFont, "Inter", "Noto Sans Thai", system-ui, sans-serif |

### Sidebar dimensions
| Token | ค่า |
| :--- | :--- |
| `sidebar-width` | 260px |
| `sidebar-width-min` | 220px |
| `sidebar-width-max` | 480px |
| `sidebar-rail` | 52px (ย่อ desktop ≥1024px) |
| `sidebar-icon` | 16px (ย่อ 18px) |
| `sidebar-item-font` | 13px / weight 500 |
| `sidebar-group-font` | 11px / uppercase / weight 600 |

---

## 2. Semantic Tokens (Theme-Aware)

| Semantic Token | Light Mode | Dark Mode | การนำไปใช้ |
| :--- | :--- | :--- | :--- |
| `color-bg` | `#F5F5F7` | `#0A0A0F` | พื้นหลังแคนวาส |
| `color-surface` | `rgba(255, 255, 255, 0.70)` | `rgba(255, 255, 255, 0.07)` | การ์ดขาวใส |
| `color-border` / `glass-hairline` | `rgba(20, 28, 50, 0.09)` | `rgba(255, 255, 255, 0.06)` | เส้นบาง |
| `color-primary` / `--i24-primary` | `#0F172A` | `#0F172A` | ปุ่มหลัก, pagination, พื้น sidebar |
| `color-primary-hover` | `#06182B` | `#1D4B82` | hover ปุ่ม |
| `color-secondary-glass` | `rgba(0, 0, 0, 0.06)` | `rgba(255, 255, 255, 0.12)` | ปุ่มรอง |
| `color-on-primary` | `#FFFFFF` | `#FFFFFF` | ตัวหนังสือบน Navy |
| `color-text` | `#1A1A1A` | `#F3F4F6` | ตัวหนังสือหลัก / เซลล์ |
| `color-text-muted` | `#6B7280` | `#9CA3AF` | ตัวหนังสือรอง |
| `color-text-empty` | `#6E6E73` | `#6E6E73` | ว่างไม่มีข้อมูล |
| `color-table-header-bg` | `#E2E8F0` | `rgba(255, 255, 255, 0.06)` | พื้นหัวตาราง |
| `color-table-header-text` | `#334155` | `#9CA3AF` | ตัวอักษรหัวตาราง |
| `color-table-cell-border` | `rgba(0, 0, 0, 0.05)` | `rgba(255, 255, 255, 0.06)` | เส้นใต้เซลล์ |
| `grad-table-row-hover` | `linear-gradient(135deg, rgba(176,20,27,0.06), rgba(15,23,42,0.08))` | `linear-gradient(135deg, rgba(236,33,41,0.12), rgba(46,78,166,0.16))` | hover แถว |
| `color-success` | `#137A47` | `#3BB273` | badge สำเร็จ |
| `color-warning` | `#B7791F` | `#D6A24A` | badge เตือน |
| `color-danger` | `#B0141B` | `#B0141B` | badge ล้มเหลว / ออกจากระบบ |
| `color-gold` | `#A8811C` | `#E7C873` | badge status ทางเลือก |
| `color-logout-hover` | `rgba(176, 20, 27, 0.12)` | `rgba(176, 20, 27, 0.18)` | hover ปุ่มออกจากระบบ |

### Sidebar (พื้นไม่สลับ theme — ค่าเดียวทั้งสองโหมด ยกเว้น footer)

| Semantic Token | Light | Dark |
| :--- | :--- | :--- |
| `color-sidebar-bg` | `#0F172A` | `#0F172A` |
| `color-sidebar-border` | `rgba(255,255,255,0.08)` | `rgba(255,255,255,0.08)` |
| `color-sidebar-text` | `rgba(255,255,255,0.88)` | `rgba(255,255,255,0.88)` |
| `color-sidebar-text-active` | `#FFFFFF` | `#FFFFFF` |
| `color-sidebar-text-group` | `rgba(255,255,255,0.55)` | `rgba(255,255,255,0.55)` |
| `color-sidebar-hover` | `rgba(255,255,255,0.06)` | `rgba(255,255,255,0.06)` |
| `color-sidebar-selected` | `rgba(255,255,255,0.10)` | `rgba(255,255,255,0.10)` |
| `color-sidebar-nested` | `rgba(255,255,255,0.12)` | `rgba(255,255,255,0.12)` |
| `color-sidebar-scrollbar` | `rgba(255,255,255,0.22)` | `rgba(255,255,255,0.22)` |
| `color-sidebar-scrollbar-hover` | `rgba(255,255,255,0.35)` | `rgba(255,255,255,0.35)` |
| `color-sidebar-footer-border` | `rgba(255,255,255,0.12)` | `rgba(255,255,255,0.12)` |
| `color-sidebar-footer-bg` | `rgba(0,0,0,0.12)` | `rgba(0,0,0,0.18)` |
| `color-sidebar-email` | `rgba(255,255,255,0.60)` | `rgba(255,255,255,0.60)` |
| `color-sidebar-badge` | `rgba(255,255,255,0.14)` | `rgba(255,255,255,0.14)` |
| `color-sidebar-backdrop` | `rgba(0,0,0,0.25)` | `rgba(0,0,0,0.25)` |

หน้าอื่นที่ยึดชุดนี้: ใช้คลาส `.mac-sidebar` / `.mac-table` — **ห้ามประกาศสีซ้ำ**
