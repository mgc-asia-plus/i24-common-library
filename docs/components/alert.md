# Alert

## Purpose
ข้อความแจ้งสถานะแบบ **inline** (สำเร็จ / เตือน / ผิดพลาด / ข้อมูล) ค้างบนหน้าจอจนกว่าจะแก้สาเหตุหรือผู้ใช้ปิด — ไม่ใช่ toast ที่หายเอง

## Anatomy
```
[ icon | title + message | (dismiss ×?) ]
```
- บังคับ: ไอคอน + ข้อความ (title และ/หรือ message)
- ทางเลือก: ปุ่มปิด; ปุ่ม action ท้ายข้อความ

## Variants

| Variant | เมื่อไหร่ที่ใช้ | Visual |
|---------|----------------|--------|
| `info` | ข้อมูลไม่เร่งด่วน | เน้นด้วย `color-primary` / `--i24-primary` (`#0F172A`); ข้อความ `color-text`; พื้น `color-surface` |
| `success` | สำเร็จ | `color-success` (`#137A47` / dark `#3BB273`) |
| `warning` | เตือน ให้ตรวจสอบ | `color-warning` (`#B7791F` / dark `#D6A24A`) |
| `danger` | ผิดพลาด ต้องแก้ | `color-danger` (`#B0141B`) |

พื้นใช้ `color-surface` (หรือ `crimson-glass-tint` เมื่อเป็น danger ตาม [`../brand/effects.md`](../brand/effects.md)) — ห้ามคิด opacity เอง; มน `radius-box`

## Sizes

| Size | Padding | ตัวอักษร |
|------|---------|----------|
| `sm` | 12px | เล็ก |
| `md` (default) | 16px | `text-sm` |

ปุ่มปิด / action มีพื้นที่แตะ ≥ **40×40px**

## States

| State | พฤติกรรม |
|-------|----------|
| **default** | แสดง inline ตาม variant; static ถ้าปิดไม่ได้ |
| **focus** | ปุ่ม × / action มีวงแหวน `color-focus-ring` (ค่า = `color-primary` / `--i24-primary` `#0F172A`) |
| **disabled** | ปุ่ม × / action ที่ปิดแล้ว — ไม่รับคลิก; `disabled` หรือ `aria-disabled` |

ทางเลือก `with-action` — ปุ่มท้ายข้อความใช้ spec [`button.md`](button.md)

## Tokens used
- `color-primary` / `--i24-primary` (`#0F172A`) — เน้น info
- `color-success` (`#137A47` / `#3BB273`)
- `color-warning` (`#B7791F` / `#D6A24A`)
- `color-danger` (`#B0141B`)
- `color-text` / `color-text-muted` — ข้อความ
- `color-surface` — พื้น
- `color-logout-hover` — พื้น danger อ่อนเมื่อใช้ recipe `crimson-glass-tint`
- `radius-box` (10px)
- `color-focus-ring` — focus ของปุ่มปิด / action (กฎร่วม SpecIndex); ค่าวงแหวน = `color-primary`
- Effect (danger อ่อน): `crimson-glass-tint` — [`../brand/effects.md`](../brand/effects.md)

ชื่อ token จาก [`../brand/design-tokens.md`](../brand/design-tokens.md)

## Accessibility
- ผิดพลาด / สำคัญ: container `role="alert"` (อ่านทันที)
- ข้อมูลไม่เร่งด่วน: `role="status"` / `aria-live="polite"`
- อย่าสื่อด้วยสีอย่างเดียว — มีไอคอน + ข้อความชัด; error บอก "เกิดอะไร + ทำอย่างไรต่อ"
- ปุ่มปิด: `aria-label="ปิด"`; คีย์บอร์ด `Tab` + `Enter` / `Space`; focus `color-focus-ring`; พื้นที่แตะ ≥ **40×40px**

## Reference snippet
```html
<div role="alert" class="flex gap-3 rounded-[--radius-box] p-4 bg-[--color-surface] text-[--color-text] border-l-4 border-[--color-danger]">
  <span aria-hidden="true">✕</span>
  <div>
    <p>บันทึกไม่สำเร็จ</p>
    <p>กรุณาตรวจสอบข้อมูลแล้วลองใหม่</p>
  </div>
  <button type="button" aria-label="ปิด"
          class="min-h-10 min-w-10 focus-visible:outline-2 focus-visible:outline-[--color-focus-ring]">×</button>
</div>
```
