# Pagination

## Purpose
แถบเปลี่ยนหน้าข้อมูลตารางหรือกริดที่ผูกกับ JSON API (`meta.page`, `meta.page_size`, `meta.total`)  
หน้าปัจจุบันใช้ **Navy Solid** `color-primary` / `--i24-primary` (`#0F172A`) สูตร `btn-navy-solid`; หน้าอื่นใช้ `btn-gray-glass` จาก [`../brand/effects.md`](../brand/effects.md)

## Anatomy
```
แสดง 1–20 จาก 137    [‹] [1] [2] [3] … [7] [›]
└── summary ──┘      └── page controls ────────┘
```
1. **Result summary** — เช่น "แสดง 1–20 จาก 137 รายการ"
2. **Previous** — หน้าก่อน
3. **Page numbers** — เลขหน้า + ellipsis เมื่อหน้าเยอะ
4. **Next** — หน้าถัดไป

วางร่วมกับ [table.md](table.md) ภายใต้ `.mac-section` เมื่อเป็นตาราง `.mac-table`.

## Variants
| Variant | เมื่อไหร่ที่ใช้ | ลักษณะ |
|---------|----------------|--------|
| `numbered` (default) | ตารางมาตรฐาน | สรุป + prev + เลขหน้า + next |
| `compact` | จอแคบ / การ์ด | prev / next + ข้อความ "หน้า n จาก m" ไม่โชว์ทุกเลข |

หน้า active **ต้อง** เป็น `color-primary` / `--i24-primary` (`#0F172A`) + `color-on-primary` (`#FFFFFF`) — ห้ามใช้ accent อื่น.

## Sizes
| Size | ปุ่มหน้า / prev / next | ใช้เมื่อ |
|------|------------------------|---------|
| `md` (default) | **40×40px** ขั้นต่ำ (แตะมือถือ) | ทั่วไป |
| `lg` | **42×42px** | แถบกว้าง คู่ตาราง |

`radius-pill` **9999px**. ห้ามสูง/กว้าง 36px — ต่ำกว่า 40×40.

## States
| State | พฤติกรรม |
|-------|----------|
| `default` | ปุ่มหน้าอื่น: สูตร `btn-gray-glass` (`color-secondary-glass`) |
| `hover` | หน้าอื่นตาม hover `btn-gray-glass`; หน้า active ไม่มี hover เปลี่ยนสีพื้น |
| `focus` / `focus-visible` | วงแหวน `color-focus-ring` (`color-primary` / `--i24-primary` `#0F172A`) ทุกปุ่มที่โฟกัสได้ |
| `active` (หน้าปัจจุบัน) | พื้น `color-primary` / `--i24-primary` (`#0F172A`); ตัวหนังสือ `color-on-primary` (`#FFFFFF`); `aria-current="page"`; ไม่ใช่ลิงก์นำทางซ้ำ |
| `disabled` | Prev ที่หน้า 1 / Next ที่หน้าสุดท้าย: `disabled` + `aria-disabled="true"` |
| `loading` (optional) | กำลังโหลดหน้าใหม่ — ปุ่มกดไม่ได้ชั่วคราว |

## Tokens used
- `color-primary` / `--i24-primary` (`#0F172A`) — หน้า active (สูตร `btn-navy-solid`)
- `color-on-primary` (`#FFFFFF`) — ตัวหนังสือหน้า active
- `color-primary-hover` (`#06182B` / `#1D4B82`) — ไม่ใช้กับหน้า active; ใช้ถ้ามีปุ่ม Navy อื่นในแถบ
- `color-secondary-glass` — ปุ่มหน้าอื่น / prev / next (สูตร `btn-gray-glass`, blur **16px**)
- `color-text` (`#1A1A1A` / `#F3F4F6`) · `color-text-muted` (`#6B7280` / `#9CA3AF`) — สรุปผลและ ellipsis
- `color-focus-ring` — ใช้ค่า `color-primary` / `--i24-primary` (`#0F172A`)
- `radius-pill` / `radius-btn` **9999px**
- `font-sans`

อ้างสูตร: `btn-navy-solid`, `btn-gray-glass` ใน [`../brand/effects.md`](../brand/effects.md).  
`prefers-reduced-transparency` / fallback ทึบ — ตาม effects.

## Accessibility
- **Role**: ครอบด้วย `<nav aria-label="Pagination">` (หรือชื่อที่แปลแล้ว); กลุ่มปุ่มเป็นรายการลิงก์/ปุ่มไม่ใช่ตาราง
- **Current page**: `aria-current="page"` บนปุ่มหน้า active; ใช้ token primary ตาม Variants
- **Keyboard**: `Tab` เลื่อนระหว่างปุ่มที่กดได้; `Enter` / `Space` เปลี่ยนหน้า; หน้า active ไม่ต้องโฟกัสซ้ำเป็นลิงก์
- **Touch**: ทุกปุ่มควบคุม ≥ **40×40px**
- **Focus ที่มองเห็น**: `focus-visible` บน prev / เลขหน้า / next
- **Disabled**: Prev/Next ที่หมดขอบเขตใส่ `disabled` และ `aria-disabled="true"` — อย่าซ่อนโดยไม่มีทางรู้
- Ellipsis เป็นข้อความ `aria-hidden="true"` ไม่ใช่ปุ่ม

## Reference snippet
```html
<nav class="i24-pagination" aria-label="Pagination">
  <p class="i24-pagination-summary">แสดง 1–20 จาก 137 รายการ</p>
  <div class="i24-pagination-controls">
    <button type="button" class="btn-gray-glass" disabled aria-disabled="true">‹</button>
    <button type="button" class="btn-primary" aria-current="page">1</button>
    <button type="button" class="btn-gray-glass">2</button>
    <span aria-hidden="true">…</span>
    <button type="button" class="btn-gray-glass">›</button>
  </div>
</nav>
```
HTML สั้น — ผูก `meta.page` / `page_size` / `total` ที่ runtime ของ stack ไม่ใส่ template เต็ม.
