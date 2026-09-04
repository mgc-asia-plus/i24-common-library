# Input

## Purpose
ช่องกรอกข้อความบรรทัดเดียว (text/email/number/password) พร้อม label และสถานะ validation

## Anatomy
```
Label (+ * ถ้าจำเป็น)
┌───────────────────────────┐
│ (icon?) ค่า...    (icon?)  │
└───────────────────────────┘
Helper / Error text
```

## Variants
- ตามชนิด: `text`, `email`, `number`, `password`, `search`
- `with-icon` (นำหน้า/ต่อท้าย), `with-addon` (เช่นหน่วย "บาท")

## Sizes
| Size | สูง | text |
|------|-----|------|
| `sm` | 32px | `text-sm` |
| `md` (default) | 40px | `text-base` |

## States
- **default**: border `color-border`, พื้น `color-bg` (หรือ glass `input-bg` ในธีม Luxury Clear Glass)
- **focus**: ring `color-focus-ring` (navy) — ไม่ใช้ขอบแดง
- **disabled**: พื้น `color-surface`, opacity ลด, `not-allowed`
- **readonly**: ไม่มี border เน้น, แก้ไม่ได้แต่ copy ได้
- **error**: border `color-danger` + error text ใต้ช่อง + `aria-invalid="true"`
- **success** (optional): border `color-success`

## Tokens used
`color-bg`, `input-bg` (glass), `color-surface`, `color-border`, `color-text`, `color-text-muted`, `color-danger`, `color-focus-ring` (navy), `radius-md`, `space-3`, `text-sm/base`

## Accessibility
- ทุก input ต้องมี `<label>` ผูกด้วย `for`/`id` (หรือ `aria-label`)
- error ผูกด้วย `aria-describedby` ชี้ไป error text; ตั้ง `aria-invalid`
- ฟิลด์จำเป็น: `required` + เครื่องหมาย * ที่ label (ไม่พึ่งสีอย่างเดียว)
- placeholder ไม่ใช่ label

## Reference snippet
```html
<div class="flex flex-col gap-1">
  <label for="email" class="text-sm text-[--color-text]">อีเมล <span aria-hidden="true">*</span></label>
  <input id="email" type="email" required aria-describedby="email-err"
         class="h-10 rounded-md border border-[--color-border] bg-[--color-bg] px-3 text-[--color-text]
                focus-visible:outline-2 focus-visible:outline-[--color-focus-ring]" />
  <p id="email-err" class="text-sm text-[--color-danger]">รูปแบบอีเมลไม่ถูกต้อง</p>
</div>
```
> validation ฝั่ง server/HTMX: คืน partial ที่มี state error; ฝั่ง React: คุม state + aria ตามตาราง
