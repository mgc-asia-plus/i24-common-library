# Button

## Purpose
ปุ่มมาตรฐานของ i24 สำหรับสั่ง action — **Primary Navy Solid** สำหรับงานหลัก และ **Secondary Frosted Gray Glass** สำหรับงานรอง ใช้เมื่อผู้ใช้ต้องบันทึก ยืนยัน ยกเลิก หรือลบข้อมูล

## Anatomy
```
[ leading-icon? ]  label  [ trailing-icon? / spinner? ]
```
- บังคับ: `<button type="button|submit|reset">` + ข้อความที่มองเห็น หรือ `aria-label` เมื่อมีแต่ไอคอน
- ทางเลือก: ไอคอนนำ/ตาม; spinner เมื่อ `loading`

## Variants

| Variant | เมื่อไหร่ที่ใช้ | Visual |
|---------|----------------|--------|
| `primary` | Action หลัก (บันทึก, จอง, ยืนยัน) | Recipe `btn-navy-solid` — พื้น `color-primary` / `--i24-primary` (`#0F172A`) ทึบ ไร้ขอบ; ข้อความ `color-on-primary` (`#FFFFFF`); มน `radius-btn` / `radius-pill` |
| `secondary` | Action รอง (ยกเลิก, ย้อนกลับ) | Recipe `btn-gray-glass` — พื้น `color-secondary-glass`; ข้อความ `color-text`; มนแคปซูลเท่า primary |
| `primary-glass` (option) | Action หลักแบบโปร่งแสง | Recipe `btn-navy-glass` — พื้น `primary-glass-bg`; ข้อความ `color-on-primary` |
| `danger` | ลบหรือทำลายข้อมูล | พื้น `color-danger` (`#B0141B`); ข้อความ `color-on-primary`; มนแคปซูลเท่ากัน |
| `ghost` | Toolbar / action เบา | พื้นโปร่งใส; ข้อความ `color-primary` หรือ `color-text` |

คลาสที่ล็อก: `.btn-primary` / `.btn-navy-solid`, `.btn-gray-glass` / `.btn-secondary`, `.btn-navy-glass`, `.btn-danger`, `.btn-ghost`

Blur / opacity ของแก้วอ้างสูตรใน [`../brand/effects.md`](../brand/effects.md) เท่านั้น — ห้ามคิดค่าใหม่

## Sizes

| Size | Height | Padding แนวนอน | ตัวอักษร | ใช้เมื่อ |
|------|--------|----------------|----------|----------|
| `sm` | 40px | 14px | 13px | Table row, filter — ไม่ต่ำกว่าพื้นที่แตะ 40×40 |
| `md` (default) | 42px | 22px | 14px | ฟอร์ม, modal actions |
| `lg` | 48px | 26px | 15px | Hero CTA |

ทุกขนาดมีพื้นที่แตะอย่างน้อย **40×40px** (`min-height` / hit area)

## States

| State | พฤติกรรม |
|-------|----------|
| **default** | ตาม variant |
| **hover** | `primary` → `color-primary-hover` (`#06182B` light / `#1D4B82` dark); `secondary` ตาม hover ของ `btn-gray-glass`; `danger` → `brand-red-hover` (`#8E1015`); เลื่อนตาม recipe |
| **focus** / `focus-visible` | วงแหวนมองเห็น `color-focus-ring` (ค่า = `color-primary` / `--i24-primary` `#0F172A`) — ห้ามตัด outline |
| **active** | กดค้างตาม recipe (`scale(0.98)`) |
| **disabled** | `disabled` หรือ `aria-disabled="true"`; ไม่รับคลิก; ไม่มี hover; `cursor: not-allowed` |
| **loading** | `aria-busy="true"`; แสดง spinner; กันคลิกซ้ำ |

## Tokens used
- `color-primary` / `--i24-primary` (`#0F172A`) — พื้น primary
- `color-primary-hover` (`#06182B` / `#1D4B82`) — hover primary
- `color-on-primary` (`#FFFFFF`) — ข้อความบน Navy / danger
- `color-secondary-glass` — พื้น secondary
- `color-text` (`#1A1A1A` / `#F3F4F6`) — ข้อความ secondary
- `color-danger` (`#B0141B`) — danger
- `brand-red-hover` (`#8E1015`) — hover danger
- `primary-glass-bg` / `primary-glass-hover` — option navy glass
- `radius-btn` / `radius-pill` (9999px)
- `font-sans`
- `color-focus-ring` — focus ที่มองเห็น (กฎร่วม SpecIndex); ค่าวงแหวน = `color-primary`
- Effects: `btn-navy-solid`, `btn-gray-glass`, `btn-navy-glass` — [`../brand/effects.md`](../brand/effects.md)

ชื่อ token จาก [`../brand/design-tokens.md`](../brand/design-tokens.md)

## Accessibility
- ใช้ `<button>` จริง — role โดยกำเนิด; อย่าใช้ `<div>` คลิกได้
- คีย์บอร์ด: `Tab` โฟกัสได้; `Enter` / `Space` เท่ากับคลิก
- Focus ที่มองเห็น: `focus-visible` ด้วย `color-focus-ring`
- พื้นที่แตะ ≥ **40×40px**
- ปุ่มมีแต่ไอคอน: ต้องมี `aria-label`
- `disabled` ใช้ attribute ของปุ่ม (หรือ `aria-disabled` ถ้ายังต้องโฟกัสเพื่อคำอธิบาย)
- อย่าสื่อความหมายด้วยสีอย่างเดียว (เช่น danger มีข้อความ "ลบรายการ")

## Reference snippet
```html
<button type="button" class="btn-primary">บันทึก</button>
<button type="button" class="btn-gray-glass">ยกเลิก</button>
<button type="button" class="btn-danger">ลบรายการ</button>
<button type="button" class="btn-ghost" disabled>ดูตัวอย่าง</button>
```

React / Tailwind (ชื่อคลาส):
```html
<button type="submit"
        class="btn-primary h-10 px-[22px] rounded-full font-semibold
               bg-[--i24-primary] text-[--i24-on-primary]
               focus-visible:outline-2 focus-visible:outline-[--color-focus-ring]">
  บันทึก
</button>
```
