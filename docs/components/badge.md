# Badge

## Purpose
ป้ายเล็กแสดงสถานะ หมวด หรือจำนวน (เช่น "ใหม่", "รอดำเนินการ", จำนวนแจ้งเตือน)

## Anatomy
`[ (dot?) label ]` — ข้อความสั้น พื้นอ่อน radius สูง (pill)

## Variants
| Variant | พื้น | ข้อความ | ใช้เมื่อ |
|---------|------|---------|----------|
| `brand` | `grad-brand` (แดง) | `white` | เน้นแบรนด์ |
| `accent` | `grad-accent` (navy) | `white` | tag/หมวดเด่น |
| `status` | clear glass (`glass-bg` + hairline) | `color-gold` | สถานะในตาราง (ลุค luxury) |
| `success` | glass/โปร่ง | `color-success` | สำเร็จ |
| `warning` | glass/โปร่ง | `color-warning` | เตือน |
| `danger` | glass/โปร่ง | `color-danger` | ผิดพลาด |

> `status` = กระจกใส + ตัวอักษรสีทอง (`color-gold`) ใช้ในคอลัมน์สถานะของตาราง. ⚠️ gold บน light ≈ 3.6:1 → ใช้ตัวหนา หรือดู a11y ใน [`../brand/effects.md`](../brand/effects.md). สื่อสถานะด้วย dot/ข้อความด้วย ไม่พึ่งสีอย่างเดียว

## Sizes
| Size | สูง | text |
|------|-----|------|
| `sm` | 18px | `text-xs` |
| `md` (default) | 22px | `text-sm` |

## States
- static เป็นหลัก (ไม่โต้ตอบ). ถ้าคลิกได้/ลบได้ → เพิ่มปุ่ม × ที่มี `aria-label` และ focus ring
- dot variant: จุดสีนำหน้าเพื่อสื่อสถานะโดยไม่พึ่งสีอย่างเดียว

## Tokens used
`grad-brand`, `grad-accent`, `glass-bg`, `glass-hairline`, `color-gold`, `color-text-muted`, `color-success`, `color-danger`, `color-warning`, `radius-pill`, `text-xs/sm`, `space-2/3`

## Accessibility
- อย่าสื่อความหมายด้วย "สี" อย่างเดียว — ใส่ข้อความ/ไอคอน/dot ประกอบ
- ถ้า badge เป็นจำนวนแจ้งเตือนของปุ่ม ให้ผูก `aria-label` ที่ปุ่ม เช่น "การแจ้งเตือน 3 รายการ"
- badge ที่ลบได้: ปุ่ม × ต้องเข้าถึงด้วยคีย์บอร์ด

## Reference snippet
```html
<span class="inline-flex items-center gap-1 rounded-pill bg-[--color-surface] text-[--color-text-muted] text-xs px-2 h-[18px]">
  <span class="w-1.5 h-1.5 rounded-pill bg-[--color-accent]"></span>
  รอดำเนินการ
</span>
```
