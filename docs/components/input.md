# Input

## Purpose
ช่องกรอกข้อความบรรทัดเดียว (`text` / `email` / `number` / `password` / `search`) พร้อม label และสถานะ validation — ใช้ในฟอร์มเมื่อผู้ใช้ต้องพิมพ์ค่า

## Anatomy
```
Label (+ * ถ้าจำเป็น)
┌───────────────────────────┐
│ (icon?) ค่า...    (icon?)  │
└───────────────────────────┘
Helper / Error text
```
- บังคับ: `<label>` ผูก `for`/`id` (หรือ `aria-label`) + `<input>`
- ทางเลือก: ไอคอนนำ/ตาม, addon (เช่นหน่วย "บาท"), helper / error

## Variants
- ตามชนิด: `text`, `email`, `number`, `password`, `search`
- `with-icon` — ไอคอนนำหน้าหรือต่อท้าย
- `with-addon` — ส่วนประกอบติดข้างช่อง (หน่วย, ปุ่มเล็ก)

ผิวช่อง: พื้น `color-bg` หรือ `color-surface`; เส้น `color-border`; มน `radius-box` (10px)

## Sizes

| Size | Height | ตัวอักษร |
|------|--------|----------|
| `sm` | 40px | `text-sm` |
| `md` (default) | 40px | `text-base` |

ความสูงขั้นต่ำ **40×40px** ทุกขนาด (พื้นที่แตะบนมือถือ)

## States

| State | พฤติกรรม |
|-------|----------|
| **default** | เส้น `color-border`; พื้น `color-bg` หรือ `color-surface` |
| **focus** | วงแหวน `color-focus-ring` (ค่า = `color-primary` / `--i24-primary` `#0F172A`) — ไม่ใช้ขอบแดงตอนโฟกัสปกติ |
| **disabled** | `disabled`; พื้น `color-surface`; `cursor: not-allowed`; ไม่รับโฟกัสแก้ไข |
| **readonly** | แก้ไม่ได้แต่คัดลอกได้; ไม่เน้นเส้นเท่า default |
| **error** | เส้น `color-danger` (`#B0141B`) + ข้อความ error ใต้ช่อง + `aria-invalid="true"` |
| **success** (optional) | เส้น `color-success` |

## Tokens used
- `color-bg` — พื้นช่อง (หรือแคนวาส)
- `color-surface` — พื้น disabled / ทางเลือก
- `color-border` — เส้น default
- `color-text` (`#1A1A1A` / `#F3F4F6`) — ค่าที่พิมพ์
- `color-text-muted` — placeholder / helper
- `color-danger` (`#B0141B`) — error
- `color-success` — success (optional)
- `radius-box` (10px)
- `font-sans`
- `color-focus-ring` — focus ที่มองเห็น (กฎร่วม SpecIndex); ค่าวงแหวน = `color-primary` / `--i24-primary` (`#0F172A`)

ชื่อ token จาก [`../brand/design-tokens.md`](../brand/design-tokens.md)

## Accessibility
- ทุกช่องมี `<label>` ผูก `for`/`id` หรือ `aria-label` — placeholder ไม่ใช่ label
- Error ผูก `aria-describedby` ไปข้อความ error; ตั้ง `aria-invalid="true"`
- ฟิลด์จำเป็น: `required` + เครื่องหมาย `*` ที่ label (มี `aria-hidden` บนเครื่องหมายถ้าประกาศ required แล้ว)
- คีย์บอร์ด: `Tab` เข้าช่อง; พิมพ์ได้ตามชนิด
- Focus ที่มองเห็น: `color-focus-ring`
- พื้นที่แตะ ≥ **40×40px**

## Reference snippet
```html
<div>
  <label for="email">อีเมล <span aria-hidden="true">*</span></label>
  <input id="email" type="email" required
         aria-invalid="true" aria-describedby="email-err"
         class="h-10 rounded-[--radius-box] border border-[--color-border]
                bg-[--color-bg] px-3 text-[--color-text]
                focus-visible:outline-2 focus-visible:outline-[--color-focus-ring]" />
  <p id="email-err">รูปแบบอีเมลไม่ถูกต้อง</p>
</div>
```
