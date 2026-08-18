# Brand Palette

> **SSOT ของสี** — ทุกเอกสาร/โปรเจกต์อ้างอิงค่าจากที่นี่
>
> ✅ **ค่า brand color ยืนยันจากไฟล์ vector ทางการ `i24_LOGO.svg`** (fill จริงในไฟล์)
> เฉดเสริม (50/100/400/600/700, coral-300/500) เป็น **derived** จากสีหลัก
> (ก่อนหน้านี้ sample จาก PNG ได้ `#EC2028` ต่างจาก vector ทางการเพียง 1 หน่วย — ยึดค่า vector `#EC2129`)

## ที่มา
โลโก้ i24 = พื้นสี่เหลี่ยมมุมมนสีแดงสด + ตัวอักษร "i24" สีขาว + วง accent สีส้มปะการัง (coral) ด้านหลัง
ค่าจาก `i24_LOGO.svg`: **แดง `#EC2129`**, **ขาว `#FFFFFF`**, **coral `#F48569`**

## Brand gradient
`grad-brand = linear-gradient(135deg, #EC2129 0%, #F4574B 45%, #F48569 100%)` (แดง → coral)
ใช้กับ **องค์ประกอบ** (ปุ่ม primary, โลโก้, badge เน้น) — **ห้ามใช้กับพื้นหลังหน้า/ตัวหนังสือ**. รายละเอียด + glass ดู [`effects.md`](effects.md)

## Core brand colors

| Token | Hex | ที่มา | ตัวอย่างการใช้ |
|-------|-----|-------|----------------|
| `brand-red-50`  | `#FDECED` | derived | tint พื้นหลังอ่อน, badge แดงอ่อน |
| `brand-red-100` | `#FBD0D2` | derived | tint เข้มขึ้น, hover ของ badge |
| `brand-red-400` | `#F04E52` | derived | เน้นรอง, border เข้ม, focus ring แดง |
| `brand-red-500` | `#EC2129` | **✅ จากโลโก้** | สีหลักแบรนด์ — พื้นโลโก้, ปุ่ม primary, header, active |
| `brand-red-600` | `#C81B22` | derived | hover/pressed ของ primary + text ขาวขนาดเล็กบนพื้นแดง |
| `brand-red-700` | `#AA171D` | derived | เข้มสุด, พื้น active เข้ม |
| `brand-coral-300` | `#F7A48A` | derived | accent อ่อน, พื้น highlight |
| `brand-coral-400` | `#F48569` | **✅ จากโลโก้** | accent (blob ในโลโก้), tag, illustration |
| `brand-coral-500` | `#F1684D` | derived | accent เข้ม |

## Neutrals

| Token | Hex | ใช้กับ |
|-------|-----|--------|
| `white` | `#FFFFFF` | ตัวอักษรบนพื้นแดง, พื้น card |
| `ink-900` | `#1A1A1A` | ข้อความหลักบนพื้นสว่าง |
| `ink-700` | `#374151` | หัวข้อรอง |
| `ink-500` | `#6B7280` | ข้อความรอง / muted |
| `ink-300` | `#D1D5DB` | border, divider |
| `paper` | `#FFFFFF` | พื้นหน้า (light) |
| `paper-muted` | `#F7F7F8` | พื้น section / surface รอง (light) |

## Status colors (นอกโลโก้ — เสริมให้ครบระบบ UI)
| Token | Hex | ความหมาย |
|-------|-----|----------|
| `success-500` | `#16A34A` | สำเร็จ |
| `warning-500` | `#F59E0B` | เตือน |
| `danger-500` | `#DC2626` | ผิดพลาด (แยกจาก brand-red เพื่อไม่สับสน) |
| `info-500` | `#2563EB` | ข้อมูล |

## Usage — do / don't
**Do**
- ใช้ `brand-red-500` เป็นสี action หลัก (ปุ่ม primary, link เด่น)
- ใช้ `white` เป็นตัวอักษรบนปุ่มแดง — ถ้าเป็น **text เล็ก** บนพื้นแดง ใช้พื้น `brand-red-600` เพื่อ contrast ที่ผ่าน
- ใช้ `brand-coral-*` เป็น accent/ตกแต่งเท่านั้น ไม่ใช่สี action หลัก

**Don't**
- อย่าใช้ `brand-red-500` เป็นสี error/validation — ใช้ `danger-500` แทน (กันสับสนกับ action)
- อย่าวางข้อความ `ink-500` บนพื้น `brand-red-500` (contrast ไม่พอ)
- อย่าตั้งค่า hex เองในโปรเจกต์ — อ้าง token จากที่นี่เสมอ

## Contrast (คำนวณจากค่าจริง)
| คู่สี | อัตราส่วน | ผ่าน |
|-------|-----------|------|
| `white #FFFFFF` บน `brand-red-500 #EC2129` | **≈ 4.37:1** | ✅ text ใหญ่/ปุ่ม (≥18.66px bold หรือ 24px) & UI · ⚠️ **ต่ำกว่า** AA 4.5 สำหรับ text ปกติเล็ก |
| `white #FFFFFF` บน `brand-red-600 #C81B22` | **≈ 5.78:1** | ✅ ผ่าน AA ทุกขนาด — ใช้ตัวนี้เมื่อมี white text เล็กบนพื้นแดง |
| `ink-900 #1A1A1A` บน `paper #FFFFFF` | ≈ 17:1 | ✅ ผ่านสบาย |

> ตัวเลขคำนวณตามสูตร WCAG relative luminance — **การยืนยัน a11y เต็มต้องทดสอบด้วยเครื่องมือ/ผู้เชี่ยวชาญ + assistive tech**

## หมายเหตุการยืนยัน
- ค่า brand หลัก (red-500 `#EC2129`, coral-400 `#F48569`, white) = ดึงจาก fill ของ `i24_LOGO.svg` (vector ทางการ) แล้ว
- ถ้ามี brand guide ทางการที่ระบุค่าต่าง: เทียบค่า → อัปเดตไฟล์นี้ + [`design-tokens.md`](design-tokens.md) + [`theme-tailwind.md`](theme-tailwind.md) → บันทึก `CHANGELOG.md` → ตรวจ contrast ซ้ำ
