# Design Tokens — Navy Solid & Frosted Gray Glass

โครงสร้าง token 2 ชั้น: **Primitive** (ค่าดิบ) → **Semantic** (สื่อความหมาย, map ตาม theme mode)

---

## 1. Primitive Tokens

### Color: Navy Solid (Primary สีกรมท่าทึบ — ไร้ขอบ 100%)
- `primary-navy: #0A2540` (Light Mode)
- `primary-navy-hover: #06182B`
- `primary-navy-dark: #153965` (Dark Mode, hover: `#1D4B82`)
- `on-primary: #FFFFFF`

### Color: Navy Translucent Glass (Option ปุ่มใส)
- `primary-glass-bg: rgba(10, 37, 64, 0.75)`
- `primary-glass-hover: rgba(10, 37, 64, 0.88)`
- `primary-glass-border: none` (❌ ไม่ใส่ขอบ)

### Color: Brand Red (แดงเข้ม Deep Crimson / Ruby)
- `brand-red: #B0141B` (สีแดงเข้มประจำแบรนด์ สุขุม หรูหรา)
- `brand-red-hover: #8E1015`
- `brand-red-dark: #6B0C10`

### Color: Frosted Gray Glass (Secondary ใสทะลุ — ไร้ขอบ 100%)
- Light Mode: `rgba(0, 0, 0, 0.06)` (พื้นผิว), `border: none`
- Dark Mode: `rgba(255, 255, 255, 0.12)` (พื้นผิว), `border: none`

### Color: White Translucent Glass (Card ขาวใส — ไร้ขอบ 100%)
- Light Mode: `rgba(255, 255, 255, 0.70)` + blur 24px, `border: none`, `box-shadow: 0 10px 30px -5px rgba(0,0,0,0.04)`
- Dark Mode: `rgba(255, 255, 255, 0.07)` + blur 24px, `border: none`, `box-shadow: none`

### Color: Canvas & Neutrals
- `canvas-light: #FFFFFF` (พื้นหลังสีขาวบริสุทธิ์), `canvas-dark: #0A0A0F`
- `surface-light: rgba(255, 255, 255, 0.70)`, `surface-dark: rgba(255, 255, 255, 0.07)`
- `text-light: #1A1A1A`, `text-dark: #F3F4F6`

### Color: Cool Slate (หัวตารางเท่านั้น)
- `slate-200: #E2E8F0` — พื้นหัวตาราง light
- `slate-700: #334155` — ตัวอักษรหัวตาราง light
- Dark: พื้น `rgba(255, 255, 255, 0.06)` · ตัวอักษร = `color-text-muted` — **ห้ามใช้ Cool Slate ทึบใน dark**

### Radius
| Token | ค่า | การใช้งาน |
| :--- | :--- | :--- |
| `radius-btn` | **9999px** | **ความมนของปุ่มทุกแบบ (ทรงแคปซูลมนเท่า Badges 100%)** |
| `radius-badge` | 9999px | ป้าย Badge (ทรงแคปซูลมน) |
| `radius-box` | 10px | กล่อง, การ์ด, ช่อง Input ตามมาตรฐาน Booking Service |

---

## 2. Semantic Tokens (Theme-Aware)

| Semantic Token | Light Mode | Dark Mode | การนำไปใช้ |
| :--- | :--- | :--- | :--- |
| `color-bg` | `#FFFFFF` | `#0A0A0F` | พื้นหลังแคนวาสหลัก (สีขาวบริสุทธิ์) |
| `color-surface` | `rgba(255, 255, 255, 0.70)` | `rgba(255, 255, 255, 0.07)` | พื้นผิวการ์ดขาวใส |
| `color-border` | `transparent` | `transparent` | ไร้เส้นขอบ |
| `color-primary` | `#0A2540` | `#153965` | **ปุ่มหลัก Primary Navy Solid (ทึบ คมชัด)** |
| `color-secondary-glass` | `rgba(0, 0, 0, 0.06)` | `rgba(255, 255, 255, 0.12)` | **ปุ่มรอง Secondary เทากระจกใสทะลุ** |
| `color-on-primary` | `#FFFFFF` | `#FFFFFF` | ตัวหนังสือบนปุ่ม Navy |
| `color-text` | `#1A1A1A` | `#F3F4F6` | ตัวหนังสือหลัก |
| `color-text-muted` | `#6B7280` | `#9CA3AF` | ตัวหนังสือรอง |
| `color-table-header-bg` | `#E2E8F0` | `rgba(255, 255, 255, 0.06)` | พื้นหัวตาราง (Cool Slate light) |
| `color-table-header-text` | `#334155` | `#9CA3AF` | ตัวอักษรหัวตาราง |
| `color-success` | `#137A47` | `#3BB273` | สถานะสำเร็จในตาราง |
| `color-warning` | `#B7791F` | `#D6A24A` | สถานะรอ/เตือนในตาราง |
| `color-danger` | `#B0141B` | `#B0141B` | สถานะล้มเหลวในตาราง (Deep Crimson) |
