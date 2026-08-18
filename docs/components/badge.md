# Badge

## Purpose
ป้ายเล็กแสดงสถานะ หมวด หรือจำนวน (เช่น "ใหม่", "รอดำเนินการ", จำนวนแจ้งเตือน)

## Anatomy
`[ (dot?) label ]` — ข้อความสั้น พื้นอ่อน radius สูง (pill)

## Variants
| Variant | พื้น | ข้อความ | ใช้เมื่อ |
|---------|------|---------|----------|
| `neutral` | `color-surface` | `color-text-muted` | ทั่วไป |
| `brand` | `brand-red-50` | `brand-red-600` | เน้นแบรนด์ |
| `accent` | coral อ่อน | `color-text` | tag/หมวด |
| `success` | เขียวอ่อน | `color-success` | สำเร็จ |
| `warning` | เหลืองอ่อน | เหลืองเข้ม | เตือน |
| `danger` | แดงอ่อน | `color-danger` | ผิดพลาด |

## Sizes
| Size | สูง | text |
|------|-----|------|
| `sm` | 18px | `text-xs` |
| `md` (default) | 22px | `text-sm` |

## States
- static เป็นหลัก (ไม่โต้ตอบ). ถ้าคลิกได้/ลบได้ → เพิ่มปุ่ม × ที่มี `aria-label` และ focus ring
- dot variant: จุดสีนำหน้าเพื่อสื่อสถานะโดยไม่พึ่งสีอย่างเดียว

## Tokens used
`color-surface`, `color-text`, `color-text-muted`, `brand-red-50`, `brand-red-600`, `color-success`, `color-danger`, `radius-pill`, `text-xs/sm`, `space-2/3`

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
