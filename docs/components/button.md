# Button

## Purpose
ปุ่มสำหรับ action หลักของหน้า/ฟอร์ม. ใช้ `primary` สำหรับ action สำคัญที่สุด 1 อย่างต่อบริบท

## Anatomy
`[ (icon?) label (icon?) ]` — ข้อความอยู่กลาง, icon ซ้าย/ขวาได้, พื้น + radius + padding

## Variants
| Variant | พื้น | ข้อความ | ใช้เมื่อ |
|---------|------|---------|----------|
| `primary` | `grad-brand` (แดง) | `color-on-primary` | action หลัก |
| `accent` | `grad-accent` (navy) | `white` | action รองที่เด่น (คู่กับ primary) |
| `secondary` | โปร่ง + border `color-border` | `color-text` | action รอง |
| `ghost` | โปร่ง | `color-primary` | action เบา / ใน toolbar |
| `glass` | `glass-bg-strong` + border + blur | `color-text` | action รองบนพื้น modern/glass |
| `danger` | `color-danger` | `white` | ลบ/ทำลาย (ยืนยันแล้ว) |

> โหมด Luxury Clear Glass: `primary` = `grad-brand` (แดง), `accent` = `grad-accent` (navy), ปุ่มสีมี gloss streak (`::after` overlay ขาวจาง); ปุ่มรอง = `glass`. คง contrast + focus ring (ดู [`../brand/effects.md`](../brand/effects.md))

## Sizes
| Size | สูง | padding-x | text |
|------|-----|-----------|------|
| `sm` | 32px | `space-3` | `text-sm` |
| `md` (default) | 40px | `space-5` | `text-base` |
| `lg` | 48px | `space-6` | `text-lg` |

## States
- **hover**: primary → `color-primary-hover`; secondary/ghost → พื้น `color-surface`
- **focus-visible**: ring 2px `color-focus-ring` (offset 2px)
- **active**: กดจมเล็กน้อย (translate 1px) — optional
- **disabled**: opacity ~50%, `cursor: not-allowed`, ไม่มี hover
- **loading**: แสดง spinner, ปิดการคลิก, คง label เพื่อกันหน้ากระตุก

## Tokens used
`color-primary`, `color-primary-hover`, `color-on-primary`, `color-border`, `color-text`, `color-danger`, `color-focus-ring`, `radius-pill` (หรือ `radius-md`), `space-3/5/6`, `text-sm/base/lg`

## Accessibility
- ใช้ `<button>` จริง (ไม่ใช่ `<div>`); ถ้าเป็นลิงก์ใช้ `<a>` ที่ดูเหมือนปุ่ม
- `type="button"` เว้นแต่เป็น submit
- โหมด loading ตั้ง `aria-busy="true"` และ `disabled`
- ปุ่มที่มีแต่ icon ต้องมี `aria-label`
- แตะได้ ≥ 40x40px

## Reference snippet
HTML / HTMX (Go monolith):
```html
<button type="submit"
        class="bg-primary text-on-primary rounded-pill px-5 h-10 hover:bg-primary-hover
               focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[--color-focus-ring]
               disabled:opacity-50 disabled:cursor-not-allowed"
        hx-post="/save" hx-indicator="#save-spin">
  บันทึก
</button>
```
React (Next.js) — props ที่ควรมี:
```tsx
type ButtonProps = {
  variant?: "primary" | "secondary" | "ghost" | "danger";
  size?: "sm" | "md" | "lg";
  loading?: boolean;
  iconStart?: React.ReactNode;
} & React.ButtonHTMLAttributes<HTMLButtonElement>;
// map variant/size → class ตามตารางด้านบน
```
