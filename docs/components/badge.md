# Badge

## Purpose
ป้ายเล็กแสดงสถานะ หมวด หรือจำนวน (เช่น "ใหม่", "รอดำเนินการ", จำนวนแจ้งเตือน)

## Anatomy
`[ (dot?) label ]` — ข้อความสั้น พื้นโปร่ง radius สูง (pill)

## Variants
| Variant | พื้น | ข้อความ | ใช้เมื่อ |
|---------|------|---------|----------|
| `brand` | `grad-brand` (แดง) | `white` | เน้นแบรนด์ |
| `accent` | `grad-accent` (navy) | `white` | tag/หมวดเด่น |
| `success` | โปร่ง | `color-success` (`#137A47` / dark `#3BB273`) | สำเร็จในตาราง |
| `warning` | โปร่ง | `color-warning` (`#B7791F` / dark `#D6A24A`) | รอ / เตือนในตาราง |
| `danger` | โปร่ง | `color-danger` (`#B0141B`) | ล้มเหลวในตาราง |
| `muted` | โปร่ง | `color-text-muted` | ว่าง / ไม่ทราบ / history |
| `status` | โปร่ง หรือ glass | `color-gold` | **ทางเลือก** ป้าย luxury — **ไม่ใช้เป็นคอลัมน์สถานะตาราง** |

> **ตาราง (SSOT จาก i24-etax-service `.mac-badge`)**: คอลัมน์สถานะใช้ `success` / `warning` / `danger` / `muted` + จุดสี (`mac-badge-dot`) พื้นโปร่ง — ดู [`table.md`](table.md) และ [`../brand/palette.md`](../brand/palette.md) §6.  
> สื่อสถานะด้วยข้อความ + จุด ไม่พึ่งสีอย่างเดียว

## Sizes
| Size | สูง | text |
|------|-----|------|
| `sm` | 18px | `text-xs` |
| `md` (default) | 22px | `text-sm` |

## States
- static เป็นหลัก (ไม่โต้ตอบ). ถ้าคลิกได้/ลบได้ → เพิ่มปุ่ม × ที่มี `aria-label` และ focus ring
- dot variant: จุดสีนำหน้าเพื่อสื่อสถานะโดยไม่พึ่งสีอย่างเดียว — **บังคับในคอลัมน์สถานะตาราง**

## Tokens used
`grad-brand`, `grad-accent`, `color-success`, `color-warning`, `color-danger`, `color-text-muted`, `color-gold`, `radius-pill`, `text-xs/sm`, `space-2/3`

## Accessibility
- อย่าสื่อความหมายด้วย "สี" อย่างเดียว — ใส่ข้อความ/ไอคอน/dot ประกอบ
- ถ้า badge เป็นจำนวนแจ้งเตือนของปุ่ม ให้ผูก `aria-label` ที่ปุ่ม เช่น "การแจ้งเตือน 3 รายการ"
- badge ที่ลบได้: ปุ่ม × ต้องเข้าถึงด้วยคีย์บอร์ด

## Reference snippet
```html
<!-- คอลัมน์สถานะในตาราง (etax) -->
<span class="mac-badge mac-badge--success"><span class="mac-badge-dot" aria-hidden="true"></span>ส่งแล้ว</span>
<span class="mac-badge mac-badge--warning"><span class="mac-badge-dot" aria-hidden="true"></span>รอดำเนินการ</span>
<span class="mac-badge mac-badge--danger"><span class="mac-badge-dot" aria-hidden="true"></span>ล้มเหลว</span>
```
