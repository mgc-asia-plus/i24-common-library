# Brand Palette — Navy Solid & Frosted Gray Glass

> **SSOT ของสี** — ธีมผสมผสานระบบของ `i24-booking-service` เข้ากับ **Primary Navy Solid** และ **Secondary เทากระจกใสทะลุ**
>
> เสาหลักระบบสี: **Primary = Navy Solid (#0F172A)** · **Secondary = เทากระจกใสทะลุ (Frosted Gray Glass)** · **Canvas = #F5F5F7 / #0A0A0F** · **Brand Accent = Deep Crimson Red (#B0141B)**

---

## 1. Primary Palette: Navy Solid (#0F172A)

ใช้กับปุ่ม primary, pagination หน้าปัจจุบัน, **พื้น sidebar** (ไม่สลับตาม theme)

| Token | ค่า CSS / Hex | การใช้งาน |
| :--- | :--- | :--- |
| `primary-solid` / `--i24-primary` | `#0F172A` | ปุ่มหลัก, pagination active, พื้น `.mac-sidebar` |
| `primary-hover` | `#06182B` | Hover ปุ่ม (light) |
| `primary-hover-dark` | `#1D4B82` | Hover ปุ่ม / resizer (dark) |
| `on-primary` | `#FFFFFF` | ข้อความบน Navy |
| `primary-glass` (Option) | `rgba(15, 23, 42, 0.75)` | สีกรมท่าใสทะลุ (ตัวเลือกเสริม) |

---

## 2. Secondary Palette: เทากระจกใสทะลุ (Frosted Gray Translucent Glass)

| Token | Light Mode | Dark Mode | การใช้งาน |
| :--- | :--- | :--- | :--- |
| `secondary-glass-bg` | `rgba(0, 0, 0, 0.06)` | `rgba(255, 255, 255, 0.12)` | ปุ่มรองและปุ่มควบคุมกระจกใสสีเทา |
| `secondary-glass-hover` | `rgba(0, 0, 0, 0.10)` | `rgba(255, 255, 255, 0.18)` | Hover state |
| `secondary-glass-border` | `rgba(0, 0, 0, 0.06)` | `rgba(255, 255, 255, 0.12)` | ขอบบางของกระจกสีเทา |
| `secondary-glass-sheen` | `inset 0 1px 0 rgba(255, 255, 255, 0.75)` | `inset 0 1px 0 rgba(255, 255, 255, 0.20)` | แสงสะท้อนขอบบน |
| `secondary-text` | `#1A1A1A` | `#F5F5F5` | ข้อความบนปุ่มกระจกสีเทา |

---

## 3. Canvas & Neutrals

| Token | Light Mode | Dark Mode | การใช้งาน |
| :--- | :--- | :--- | :--- |
| `page-bg` | `#F5F5F7` | `#0A0A0F` | พื้นหลังแคนวาสหลัก |
| `surface` | `rgba(255, 255, 255, 0.70)` + blur 24px | `rgba(255, 255, 255, 0.07)` | พื้นผิวการ์ด / Container |
| `border` / hairline | `rgba(20, 28, 50, 0.09)` | `rgba(255, 255, 255, 0.06)` | เส้นบางกรอบการ์ด |
| `text` | `#1A1A1A` | `#F3F4F6` | ข้อความหลัก (เซลล์ตาราง) |
| `text-muted` | `#6B7280` | `#9CA3AF` | ข้อความรอง |
| `text-empty` | `#6E6E73` | `#6E6E73` | ว่างไม่มีข้อมูลในตาราง |
| `table-header-bg` | `#E2E8F0` (Cool Slate) | `rgba(255, 255, 255, 0.06)` | พื้นหัวตาราง — **ไม่ใช้กับแถวข้อมูล** |
| `table-header-text` | `#334155` | `#9CA3AF` (`text-muted`) | ตัวอักษรหัวตาราง |
| `table-cell-border` | `rgba(0, 0, 0, 0.05)` | `rgba(255, 255, 255, 0.06)` | เส้นใต้เซลล์ |

---

## 4. Brand Accent: Deep Crimson Red

| Token | ค่า CSS / Hex | การใช้งาน |
| :--- | :--- | :--- |
| `brand-red` | `#B0141B` | สีแดงเข้มประจำแบรนด์, ปุ่มออกจากระบบ |
| `brand-red-hover` | `#8E1015` | Hover ปุ่มแดงทึบ |
| `danger` | `#B0141B` | ปุ่มลบ / การกระทำที่เป็นอันตราย |
| `logout-hover` | Light `rgba(176, 20, 27, 0.12)` · Dark `rgba(176, 20, 27, 0.18)` | Hover ปุ่มออกจากระบบบน sidebar |
| `status-danger-bg` | `rgba(176, 20, 27, 0.12)` | พื้นหลัง Badge หรือ Alert แจ้งเตือน |

---

## 5. Sidebar (พื้น Navy ไม่สลับ theme)

พื้น `.mac-sidebar` ใช้ Navy Solid เดียวกันทั้ง light/dark — ตัวอักษรขาวโปร่ง

| Token | ค่า | การใช้งาน |
| :--- | :--- | :--- |
| `color-sidebar-bg` | `#0F172A` | พื้น sidebar |
| `color-sidebar-border` | `rgba(255, 255, 255, 0.08)` | เส้นขวา |
| `color-sidebar-text-active` | `#FFFFFF` | รายการที่เลือก / ชื่อแอป |
| `color-sidebar-text` | `rgba(255, 255, 255, 0.88)` | รายการเมนูปกติ |
| `color-sidebar-text-group` | `rgba(255, 255, 255, 0.55)` | หัวกลุ่มเมนู |
| `color-sidebar-hover` | `rgba(255, 255, 255, 0.06)` | hover รายการ |
| `color-sidebar-selected` | `rgba(255, 255, 255, 0.10)` | รายการที่เลือก (ไม่มีแถบสีข้าง) |
| `color-sidebar-nested` | `rgba(255, 255, 255, 0.12)` | เส้นซ้าย nested |
| `color-sidebar-scrollbar` | `rgba(255, 255, 255, 0.22)` → hover `0.35` | scrollbar |
| `color-sidebar-footer-border` | `rgba(255, 255, 255, 0.12)` | เส้นบน footer |
| `color-sidebar-footer-bg` | Light `rgba(0, 0, 0, 0.12)` · Dark `rgba(0, 0, 0, 0.18)` | พื้น footer |
| `color-sidebar-email` | `rgba(255, 255, 255, 0.60)` | อีเมลผู้ใช้ |
| `color-sidebar-badge` | `rgba(255, 255, 255, 0.14)` | badge บน sidebar |
| `color-sidebar-backdrop` | `rgba(0, 0, 0, 0.25)` | overlay mobile |

สเปกคอมโพเนนต์: [`../components/sidebar.md`](../components/sidebar.md)

---

## 6. Contrast & Accessibility (WCAG 2.1)

คู่ข้อความหลักต้องผ่าน **WCAG 2.1 AA** (≥ **4.5:1** สำหรับข้อความปกติ).

| fg | bg | อัตราส่วน Contrast | wcag_level |
| :--- | :--- | :--- | :--- |
| `on-primary` `#FFFFFF` | `primary` / `--i24-primary` / `color-sidebar-bg` `#0F172A` | **17.85:1** | ✅ **AAA** (ผ่าน AA ≥ 4.5:1) |
| `color-text` `#1A1A1A` | `canvas` `#F5F5F7` | **15.98:1** | ✅ **AAA** |
| `color-text` `#F3F4F6` | `canvas` `#0A0A0F` (dark) | **17.95:1** | ✅ **AAA** |
| `white` `#FFFFFF` | `brand-red` `#B0141B` | **7.09:1** | ✅ **AAA** |
| `text` `#1A1A1A` | Gray Glass (Light) บน canvas | **≈ 14.0:1** | ✅ **AAA** |
| `table-header-text` `#334155` | `table-header-bg` `#E2E8F0` | **8.40:1** | ✅ **AAA** |

---

## 7. Table status (จาก i24-etax-service `.mac-badge`)

คอลัมน์สถานะในตารางใช้ **ข้อความ + จุดสี** พื้นโปร่ง — **ไม่ทา Cool Slate และไม่ใช้ gold ทั้งคอลัมน์**

| Variant | Light | Dark | ใช้เมื่อ (ตัวอย่าง etax) |
| :--- | :--- | :--- | :--- |
| `success` | `#137A47` | `#3BB273` | `ready` / `submitted` / `success` / `imported` |
| `warning` | `#B7791F` | `#D6A24A` | `pending` / `prepare` / `new` / `failed_retry` / `[transient]` |
| `danger` | `#B0141B` | `#B0141B` | `failed` / `error` / `invalid` / `[permanent]` |
| `muted` | `#6B7280` | `#9CA3AF` | ว่าง / ไม่ทราบ / `history` |
| `status` (gold) | `#A8811C` | `#E7C873` | ป้าย luxury **ทางเลือก** — ไม่ใช้ทั้งคอลัมน์สถานะ |

**Row hover**
- Light: `linear-gradient(135deg, rgba(176,20,27,0.06), rgba(15,23,42,0.08))`
- Dark: `linear-gradient(135deg, rgba(236,33,41,0.12), rgba(46,78,166,0.16))`

Mapping อ้างอิง: `i24-etax-service/internal/helpers/admintable/cell.go` (`processStatusVariant`) + `errorTypeBadge`  
สเปกคอมโพเนนต์: [`../components/table.md`](../components/table.md) · [`../components/badge.md`](../components/badge.md)
