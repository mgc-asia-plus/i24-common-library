# Alert

## Purpose
ข้อความแจ้งสถานะแบบ inline (สำเร็จ/เตือน/ผิดพลาด/ข้อมูล) — ไม่ใช่ toast ที่หายเอง

## Anatomy
`[ icon | title + message | (dismiss ×?) ]`

## Variants
| Variant | สี (semantic) | icon |
|---------|---------------|------|
| `info` | `color-info` (info-500) | ℹ️ |
| `success` | `color-success` | ✓ |
| `warning` | warning | ⚠ |
| `danger` | `color-danger` | ✕ |

ทุก variant พื้นใช้เฉดอ่อนของสีนั้น + ข้อความเฉดเข้ม เพื่อ contrast

## States
- static; ถ้า dismiss ได้ → ปุ่ม × มี `aria-label="ปิด"` + focus ring
- (optional) `with-action` — ปุ่ม action ท้ายข้อความ

## Tokens used
`color-success`, `color-danger`, `color-info`, `color-text`, `color-surface`, `radius-md`, `space-3/4`, `text-sm`

## Accessibility
- error/สำคัญ: container `role="alert"` (อ่านทันที)
- info ที่ไม่เร่งด่วน: `role="status"` / `aria-live="polite"`
- อย่าสื่อด้วยสีอย่างเดียว — มี icon + ข้อความชัด
- ข้อความ error ควรบอก "เกิดอะไร + ทำอย่างไรต่อ"

## Reference snippet
```html
<div role="alert" class="flex gap-3 rounded-md p-4 bg-[--color-surface] text-[--color-text] border-l-4 border-[--color-danger]">
  <span aria-hidden="true">✕</span>
  <div class="text-sm">
    <p class="font-semibold">บันทึกไม่สำเร็จ</p>
    <p class="text-[--color-text-muted]">กรุณาตรวจสอบข้อมูลแล้วลองใหม่</p>
  </div>
</div>
```
