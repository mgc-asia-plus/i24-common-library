# Select / Dropdown

## Purpose
กล่องเลือกค่าแบบคัสตอม แทน native `<select>` เพื่อให้ผิวและสถานะตรงธีม i24 (กระจกเทา + เมนูขาวใส) และขยายเป็น searchable combobox ได้  
Trigger ใช้สูตร `btn-gray-glass`; เมนูใช้ `surface-white-glass` จาก [`../brand/effects.md`](../brand/effects.md) — ห้ามคิด blur / opacity เอง

## Anatomy
```
┌──── trigger (combobox) ─────┐
│ Selected value        ⌄     │
└─────────────────────────────┘
        ▼ open
┌──── listbox ────────────────┐
│ Option                      │
│ Option (selected)           │
│ Option                      │
└─────────────────────────────┘
```
1. **Trigger** — ปุ่มแสดงค่าปัจจุบัน + ไอคอน chevron
2. **Selected value** — ข้อความที่เลือก หรือ placeholder
3. **Dropdown menu** — popover `role="listbox"`
4. **Option** — แถวตัวเลือก `role="option"`

## Variants
| Variant | เมื่อไหร่ที่ใช้ | ลักษณะ |
|---------|----------------|--------|
| `single` (default) | เลือกค่าเดียว | Trigger ปิดเมนูหลังเลือก |
| `searchable` | รายการยาว ต้องพิมพ์กรอง | เพิ่มช่องค้นหาในเมนู; ยังเป็น combobox + listbox |
| `native` (หลีกเลี่ยง) | ฟอร์มสำรองเมื่อไม่มี JS | `<select>` ธรรมดา — ไม่ใช้ใน UI หลัก |

ตัวเลือกที่เลือกแล้วใช้พื้น `color-primary` / `--i24-primary` (`#0F172A`) และตัวหนังสือ `color-on-primary` (`#FFFFFF`).  
Hover ตัวเลือกที่ยังไม่เลือกใช้ `color-secondary-glass` ไม่ใช่ tint ที่คิดเอง.

## Sizes
| Size | ความสูง trigger | แถว option | ใช้เมื่อ |
|------|-----------------|------------|---------|
| `sm` | **40px** (ขั้นต่ำแตะ) | สูง ≥ **40px** | แถวตาราง / filter แคบ |
| `md` (default) | **42px** | สูง ≥ **40px** | ฟอร์มทั่วไป |

ความกว้างตามคอลัมน์ฟอร์ม; เมนูกว้างเท่า trigger. `radius-pill` **9999px** บน trigger; เมนู `radius-card` **20px**.

## States
| State | พฤติกรรม |
|-------|----------|
| `default` | ปิดเมนู; `aria-expanded="false"`; พื้น trigger `color-secondary-glass` |
| `hover` | trigger ตาม hover ของ `btn-gray-glass` |
| `focus` / `focus-visible` | วงแหวน `color-focus-ring` (`color-primary` / `--i24-primary` `#0F172A`) บน trigger และ option ที่ไฮไลต์ด้วยคีย์บอร์ด |
| `open` | `aria-expanded="true"`; เมนู `surface-white-glass`; โฟกัสอยู่ใน listbox |
| `active` (option selected) | พื้น `color-primary` / `--i24-primary` (`#0F172A`); `aria-selected="true"` |
| `disabled` | trigger กดไม่ได้; ไม่เปิดเมนู; `disabled` + `aria-disabled="true"` |
| `loading` (optional) | รายการยังไม่มา — แสดงสถานะในเมนู ไม่ให้เลือก |

## Tokens used
- `color-secondary-glass` — พื้น trigger สูตร `btn-gray-glass` (blur **16px**, `radius-pill`)
- `color-surface` — พื้นเมนู สูตร `surface-white-glass` (blur **24px**, `radius-card` **20px**)
- `color-primary` / `--i24-primary` (`#0F172A`) — option ที่เลือก + focus ring
- `color-on-primary` (`#FFFFFF`)
- `color-text` (`#1A1A1A` / `#F3F4F6`) · `color-text-muted` (`#6B7280` / `#9CA3AF`) — ค่า / placeholder / chevron
- `color-focus-ring` — ใช้ค่า `color-primary` / `--i24-primary` (`#0F172A`)
- `radius-pill` / `radius-btn` **9999px** · `radius-card` **20px**
- `font-sans`

อ้างสูตร: `btn-gray-glass`, `surface-white-glass` ใน [`../brand/effects.md`](../brand/effects.md).  
`prefers-reduced-transparency` / fallback ทึบ — ตาม effects.

## Accessibility
- **Role**: trigger `role="combobox"` + `aria-haspopup="listbox"` + `aria-expanded` + `aria-controls` ชี้ listbox; เมนู `role="listbox"`; แถว `role="option"` + `aria-selected`
- **Keyboard**:
  - `Enter` / `Space` บน trigger — เปิด/ปิด
  - `ArrowDown` / `ArrowUp` — เลื่อนไฮไลต์ (เปิดเมนูถ้ายังปิด)
  - `Enter` — เลือกค่าที่ไฮไลต์แล้วปิด
  - `Escape` — ปิดโดยไม่เปลี่ยนค่า; คืนโฟกัสที่ trigger
  - `Tab` — ปิดเมนูและย้ายโฟกัสออก
- **Touch**: trigger และแต่ละ option ≥ **40×40px**
- **Focus ที่มองเห็น**: `focus-visible` บน trigger และ option ที่ไฮไลต์ด้วยคีย์บอร์ด
- คลิกนอกเมนูปิดได้; อย่าใช้เฉพาะ hover เพื่อเลือกค่า

## Reference snippet
```html
<div class="i24-select">
  <button type="button" class="btn-gray-glass i24-select-trigger" role="combobox"
          aria-haspopup="listbox" aria-expanded="false" aria-controls="car-list">
    <span>เลือกประเภทรถ…</span>
  </button>
  <ul id="car-list" class="surface-white-glass" role="listbox" hidden>
    <li role="option" aria-selected="true">Sedan</li>
    <li role="option" aria-selected="false">SUV</li>
  </ul>
</div>
```
HTML สั้นสำหรับ anatomy / ARIA — อย่าคัดลอกเป็น template ครบชุดต่อ stack.
