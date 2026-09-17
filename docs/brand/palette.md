# Brand Palette — Navy Solid & Frosted Gray Glass

> **SSOT ของสี** — ธีมผสมผสานระบบของ `i24-booking-service` เข้ากับ **Primary Navy Solid** และ **Secondary เทากระจกใสทะลุ**
>
> เสาหลักระบบสี: **Primary = Navy Solid (#0A2540)** · **Secondary = เทากระจกใสทะลุ (Frosted Gray Glass)** · **Canvas = สีขาว (#FFFFFF)** · **Brand Accent = Deep Crimson Red (#B0141B)**

---

## 1. Primary Palette: Navy Solid (#0A2540)

| Token | ค่า CSS / Hex | การใช้งาน |
| :--- | :--- | :--- |
| `primary-solid` | `#0A2540` | ปุ่มหลักสีกรมท่าทึบ คมชัด Contrast สูง AAA |
| `primary-hover` | `#06182B` | Hover state |
| `primary-dark` | `#153965` | Dark Mode state |
| `on-primary` | `#FFFFFF` | ข้อความสีขาวบน Navy |
| `primary-glass` (Option) | `rgba(10, 37, 64, 0.75)` | สีกรมท่าใสทะลุ (ตัวเลือกเสริม) |

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

## 3. Canvas & Neutrals (อิง i24-booking-service)

| Token | Light Mode | Dark Mode | การใช้งาน |
| :--- | :--- | :--- | :--- |
| `page-bg` | `#F5F5F7` | `#0A0A0F` | พื้นหลังแคนวาสหลัก |
| `surface` | `#FFFFFF` | `#171A21` | พื้นผิวการ์ด / Container |
| `border` | `#D1D5DB` | `#2A2F3A` | เส้นคั่นและขอบการ์ด |
| `text` | `#1A1A1A` | `#F3F4F6` | ข้อความหลัก |
| `text-muted` | `#6B7280` | `#9CA3AF` | ข้อความรอง |
| `table-header-bg` | `#E2E8F0` (Cool Slate) | `rgba(255, 255, 255, 0.06)` | พื้นหัวตาราง — **ไม่ใช้กับแถวข้อมูล** |
| `table-header-text` | `#334155` | `#9CA3AF` (`text-muted`) | ตัวอักษรหัวตาราง |

---

## 4. Brand Accent: Deep Crimson Red (แดงเข้มซิกเนเจอร์)

| Token | ค่า CSS / Hex | การใช้งาน |
| :--- | :--- | :--- |
| `brand-red` | `#B0141B` | สีแดงเข้มลึก (Deep Crimson) ประจำแบรนด์ หรูหรา สุขุม |
| `brand-red-hover` | `#8E1015` | Hover state |
| `danger` | `#B0141B` | ปุ่มลบ / การกระทำที่เป็นอันตราย |
| `status-danger-bg` | `rgba(176, 20, 27, 0.12)` | พื้นหลัง Badge หรือ Alert แจ้งเตือน |

---

## 5. Contrast & Accessibility (WCAG 2.1)

| คู่สี | อัตราส่วน Contrast | ผลประเมิน WCAG |
| :--- | :--- | :--- |
| `white #FFFFFF` บน `Navy Solid #0A2540` | **≈ 14.8:1** | ✅ ผ่าน **AAA** ทุกขนาดตัวอักษร |
| `white #FFFFFF` บน `Brand Red #B0141B` | **≈ 5.9:1** | ✅ ผ่าน **AA / AAA Large** |
| `text #1A1A1A` บน `Gray Glass (Light)` | **≈ 14.2:1** | ✅ ผ่าน **AAA** ทุกขนาดตัวอักษร |
| `table-header-text #334155` บน `table-header-bg #E2E8F0` | **≈ 8.4:1** | ✅ ผ่าน **AAA** ทุกขนาดตัวอักษร |

---

## 6. Table status (จาก i24-etax-service `.mac-badge`)

คอลัมน์สถานะในตารางใช้ **ข้อความ + จุดสี** พื้นโปร่ง — **ไม่ทา Cool Slate และไม่ใช้ gold ทั้งคอลัมน์**

| Variant | Light | Dark | ใช้เมื่อ (ตัวอย่าง etax) |
| :--- | :--- | :--- | :--- |
| `success` | `#137A47` | `#3BB273` | `ready` / `submitted` / `success` / `imported` |
| `warning` | `#B7791F` | `#D6A24A` | `pending` / `prepare` / `new` / `failed_retry` / `[transient]` |
| `danger` | `#B0141B` | `#B0141B` | `failed` / `error` / `invalid` / `[permanent]` |
| `muted` | `#6B7280` | `#9CA3AF` | ว่าง / ไม่ทราบ / `history` |

Mapping อ้างอิง: `i24-etax-service/internal/helpers/admintable/cell.go` (`processStatusVariant`) + `errorTypeBadge`  
สเปกคอมโพเนนต์: [`../components/table.md`](../components/table.md) · [`../components/badge.md`](../components/badge.md)
