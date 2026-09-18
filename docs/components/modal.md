# Modal / Dialog

## Purpose
หน้าต่างป๊อปอัปสำหรับยืนยันการกระทำสำคัญ (ส่งข้อมูล, ลบรายการ) หรือแบบฟอร์มสั้น โดยไม่พาผู้ใช้ออกจากหน้าเดิม  
พื้นผิวกล่องใช้สูตร `surface-white-glass` จาก [`../brand/effects.md`](../brand/effects.md) — ห้ามคิด blur / opacity / radius เอง

## Anatomy
```
┌──────── overlay (dim) ─────────┐
│  ┌──────── modal card ───────┐ │
│  │ Header: title + close     │ │
│  │ Body: ข้อความ / ฟอร์มย่อย  │ │
│  │ Footer: Cancel | Primary  │ │
│  └───────────────────────────┘ │
└────────────────────────────────┘
```
1. **Overlay** — ม่านทึบ `color-sidebar-backdrop` (`rgba(0,0,0,0.25)`) ตัดการโต้ตอบหน้าหลัก (ไม่มี blur ของ overlay — ไม่มี EffectRecipe สำหรับ overlay)
2. **Modal card** — สูตร `surface-white-glass` (`color-surface`, blur **24px**, `radius-card` **20px**)
3. **Header** — หัวข้อ + ปุ่มปิด
4. **Body** — คำอธิบายหรืออินพุต 1–3 ช่อง
5. **Footer actions** — ปุ่มรองซ้าย/ยกเลิก, ปุ่มหลักขวา

## Variants
| Variant | เมื่อไหร่ที่ใช้ | ปุ่มหลัก |
|---------|----------------|----------|
| `confirm` | ยืนยันทั่วไป (บันทึก, ส่ง) | `.btn-primary` สูตร `btn-navy-solid` — `color-primary` / `--i24-primary` (`#0F172A`) + `color-on-primary` (`#FFFFFF`) |
| `danger` | ลบหรือการกระทำที่กู้คืนไม่ได้ | `.btn-danger` — `color-danger` (`#B0141B`) + `color-on-primary` (`#FFFFFF`) |
| `form` | ฟอร์มย่อย 1–3 ช่อง | เหมือน `confirm` |

ปุ่มยกเลิกใช้ `.btn-gray-glass` สูตร `btn-gray-glass` (`color-secondary-glass`).

## Sizes
| Size | ความกว้างกล่อง | ปุ่มใน footer | ใช้เมื่อ |
|------|----------------|---------------|---------|
| `sm` (confirm) | `max-width: 480px` | สูง ≥ **40px** (`md` ใน [button.md](button.md)) | ยืนยันสั้น |
| `md` (form, default) | `max-width: 640px` | สูง ≥ **40px** | มีอินพุต |

ปุ่มปิดและปุ่มแอ็กชันทุกตัวแตะได้ขั้นต่ำ **40×40px**.

## States
| State | พฤติกรรม |
|-------|----------|
| `default` (เปิด) | overlay + card มองเห็น; โฟกัสย้ายเข้า dialog |
| `hover` | ปุ่มตามสูตร `btn-navy-solid` / `btn-gray-glass` (`color-primary-hover` บน primary) |
| `focus` / `focus-visible` | วงแหวนที่มองเห็นบนปุ่มปิดและปุ่มแอ็กชัน (`color-focus-ring` = `color-primary` / `--i24-primary` `#0F172A`) |
| `active` | กดปุ่มหลัก — `transform: scale(0.98)` ตามสูตรปุ่ม |
| `disabled` | ปุ่มหลัก/ยกเลิกกดไม่ได้ขณะส่งคำขอ; `aria-disabled` / `disabled` |
| `loading` | ปุ่มหลักแสดงกำลังทำงาน; ห้ามปิดด้วย overlay click จนกว่าจะเสร็จหรือ error |

## Tokens used
- `color-surface` — พื้นกล่อง (light `rgba(255,255,255,0.70)` / dark `rgba(255,255,255,0.07)`) สูตร `surface-white-glass`
- `color-sidebar-backdrop` (`rgba(0,0,0,0.25)`) — overlay ทึบ
- `color-primary` / `--i24-primary` (`#0F172A`) — ปุ่มยืนยัน, หัวข้อ, focus ring
- `color-primary-hover` (`#06182B` light / `#1D4B82` dark)
- `color-on-primary` (`#FFFFFF`)
- `color-secondary-glass` — ปุ่มยกเลิก (`btn-gray-glass`)
- `color-danger` (`#B0141B`) — ปุ่มทำลาย
- `color-text` (`#1A1A1A` / `#F3F4F6`) · `color-text-muted` (`#6B7280` / `#9CA3AF`)
- `radius-card` **20px** · `radius-pill` / `radius-btn` **9999px** (ปุ่ม)
- `color-focus-ring` — ใช้ค่า `color-primary` / `--i24-primary` (`#0F172A`)
- `font-sans`

อ้างสูตรเท่านั้น: `surface-white-glass` (blur **24px**), `btn-navy-solid`, `btn-gray-glass` (blur **16px**) ใน [`../brand/effects.md`](../brand/effects.md).  
`prefers-reduced-transparency` / fallback ทึบ — ตาม effects ห้ามคิดค่าใหม่.

## Accessibility
- **Role**: กล่องมี `role="dialog"` และ `aria-modal="true"`; `aria-labelledby` ชี้หัวข้อ; `aria-describedby` ชี้คำอธิบาย
- **Focus trap**: เมื่อเปิด ย้ายโฟกัสเข้า dialog (ปุ่มปิดหรือปุ่มหลัก). `Tab` / `Shift+Tab` วนเฉพาะปุ่มและอินพุตใน dialog ไม่หลุดไปหน้าหลัก. เมื่อปิด คืนโฟกัสให้ตัวเปิด
- **Keyboard**: `Escape` ปิด (ยกเว้น `loading` ที่ล็อกการปิด); `Enter` ยืนยันเมื่อโฟกัสปุ่มหลัก
- **Touch**: ปุ่มปิดและแอ็กชัน ≥ **40×40px**
- **Focus ที่มองเห็น**: `focus-visible` วงแหวน `color-focus-ring` (`color-primary` / `--i24-primary` `#0F172A`)
- Overlay คลิกปิดได้เมื่อไม่ใช่ `loading`; `body` ใส่ scroll lock (`overflow: hidden`) ขณะเปิด
- อย่าใช้ `aria-hidden` บน dialog ที่โฟกัสอยู่

## Reference snippet
```html
<div class="i24-modal-overlay" data-open="true">
  <div class="surface-white-glass i24-modal" role="dialog" aria-modal="true"
       aria-labelledby="modal-title" aria-describedby="modal-desc">
    <h2 id="modal-title">ยืนยันการบันทึก</h2>
    <button type="button" class="i24-modal-close" aria-label="ปิด">✕</button>
    <p id="modal-desc">บันทึกรายการนี้เข้าสู่ระบบใช่หรือไม่?</p>
    <button type="button" class="btn-gray-glass">ยกเลิก</button>
    <button type="button" class="btn-primary">ยืนยัน</button>
  </div>
</div>
```
HTML สั้นสำหรับ anatomy — implementer ใส่ focus trap / ESC ใน runtime ของ stack เอง ไม่คัดลอก template เต็ม.
