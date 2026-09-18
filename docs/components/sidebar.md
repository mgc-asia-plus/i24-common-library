# Sidebar

## Purpose
แถบนำทางซ้ายแนว macOS Settings / Finder — พื้น Navy ทึบ ตัวอักษรขาว sticky สูงเต็มจอ  
ล็อกคลาส `.mac-sidebar` ทั้งระบบ — **ห้ามประกาศ hex ซ้ำ** อ้าง token จาก [`../brand/design-tokens.md`](../brand/design-tokens.md)  
พื้น = `color-sidebar-bg` (`#0F172A`) **ไม่สลับตาม light/dark** (`[data-theme]` ไม่เปลี่ยนค่านี้)

## Anatomy
```
┌ header: ชื่อแอป + badge     ┐
│ nav เลื่อนได้               │  ← กลุ่มเมนู + รายการ (+ nested)
│   (sticky สูงเต็มจอ)        │
├ footer: โปรไฟล์ + ออกจากระบบ ┤
└ resizer (desktop)           ┘
```
- `.mac-sidebar` อยู่ใน `.mac-shell` คู่กับ `.mac-sidebar-backdrop` (overlay) และ `<main class="mac-section">`
- รายการ: `.mac-sidebar-item` / หัวกลุ่ม `.mac-sidebar-group` / nested `.is-nested`
- footer แถบ: `.mac-sidebar-footer` (ค่า `color-sidebar-footer-bg` สลับโหมดได้ — คนละส่วนกับพื้น sidebar)

## Variants
| Variant | เมื่อไหร่ | พฤติกรรม |
|---------|----------|----------|
| `expanded` (default) | desktop | กว้าง `sidebar-width` (260px) |
| `collapsed` | desktop ≥1024px กดย่อ | icon rail `sidebar-rail` (52px), ไอคอน 18px |
| `overlay` | viewport ต่ำกว่า 1024px | ลอยทับจอ + backdrop `color-sidebar-backdrop` |

ลากความกว้างได้เฉพาะ `expanded` บน desktop: `sidebar-width-min`–`sidebar-width-max` (220–480px)

## Sizes
| ส่วน | Token / ค่า |
|------|-------------|
| ความกว้างปกติ | `sidebar-width` (260px) |
| ช่วงลาก | `sidebar-width-min`–`sidebar-width-max` (220–480px) |
| โหมดย่อ | `sidebar-rail` (52px) |
| มุมรายการ | `radius-sidebar-item` (6px) |
| ฟอนต์รายการ | `sidebar-item-font` (13px / weight 500) |
| หัวกลุ่ม | `sidebar-group-font` (11px / uppercase / weight 600) |
| ไอคอน | `sidebar-icon` (16px; ย่อ 18px) |
| รายการ / logout / ปุ่มย่อ | เป้าแตะขั้นต่ำ 40×40px |

## States
| State | พฤติกรรม |
|-------|----------|
| `default` | ข้อความ `color-sidebar-text`; พื้นแถบ `color-sidebar-bg` (`#0F172A`) ทั้งสองโหมด |
| `hover` | พื้นรายการ `color-sidebar-hover` |
| `selected` / `active` | พื้น `color-sidebar-selected` + ข้อความ `color-sidebar-text-active` — **ไม่มีแถบสีข้าง** |
| `focus` | วง focus ที่มองเห็น (`color-focus-ring` = `color-primary` / `#0F172A`, `:focus-visible`) |
| `disabled` | รายการที่กดไม่ได้: จางลง, ไม่มี hover, `aria-disabled="true"` |
| `group header` | `color-sidebar-text-group` ไม่ใช่ control |
| `nested` | เส้นซ้าย `color-sidebar-nested` |
| `logout` | ข้อความ/ไอคอน `color-danger` (`#B0141B`); hover พื้น `color-logout-hover` (สูตร `crimson-glass-tint`) |

พื้น sidebar = `color-sidebar-bg` (`#0F172A`) **ไม่สลับตาม light/dark**

## Tokens used
| Token | บทบาท |
|-------|--------|
| `color-sidebar-bg` | พื้น `.mac-sidebar` — `#0F172A` ทั้งสองโหมด |
| `color-sidebar-border` | เส้นขวา |
| `color-sidebar-text` | รายการปกติ |
| `color-sidebar-text-active` | รายการที่เลือก / ชื่อแอป |
| `color-sidebar-text-group` | หัวกลุ่ม |
| `color-sidebar-hover` | hover รายการ |
| `color-sidebar-selected` | พื้นรายการที่เลือก |
| `color-sidebar-nested` | เส้นซ้าย nested |
| `color-sidebar-scrollbar` / `color-sidebar-scrollbar-hover` | scrollbar |
| `color-sidebar-footer-bg` / `color-sidebar-footer-border` | พื้น/เส้น footer ในแถบ (footer-bg สลับโหมดได้) |
| `color-sidebar-email` / `color-sidebar-badge` | อีเมลผู้ใช้ / badge สภาพแวดล้อม |
| `color-sidebar-backdrop` | พื้นหลัง overlay |
| `color-danger` / `color-logout-hover` | ปุ่มออกจากระบบ |
| `color-primary` / `--i24-primary` | วง `color-focus-ring` (`#0F172A`) |
| `sidebar-width` / `sidebar-width-min` / `sidebar-width-max` / `sidebar-rail` / `sidebar-icon` | ขนาดแถบ |
| `radius-sidebar-item` | มุมรายการ |

สูตร hover ออกจากระบบ: `crimson-glass-tint` ใน [`../brand/effects.md`](../brand/effects.md)

## Accessibility
- `<aside class="mac-sidebar">` + `<nav aria-label="หลัก">`
- รายการที่เลือก: `aria-current="page"`
- โหมดย่อ: ทุกปุ่ม/ลิงก์มี `aria-label` (ไอคอนอย่างเดียวไม่พอ); เป้าแตะ ≥ 40×40px
- overlay: เมื่อเปิดใช้ `aria-modal="true"` บน aside; ปิดด้วย Esc หรือคลิก `.mac-sidebar-backdrop`; คืนโฟกัสไปปุ่มเปิด
- logout: `<button type="button">` + ชื่อที่อ่านได้; เป้าแตะ ≥ 40×40px
- resizer: `role="separator"` + `aria-orientation="vertical"` + `aria-label`; ลูกศรซ้าย/ขวาปรับความกว้าง
- คีย์บอร์ด: Tab วนรายการ; Enter เปิดลิงก์; Esc ปิด overlay
- วง `:focus-visible` ที่มองเห็นบนทุกรายการที่โต้ตอบได้ (`color-focus-ring` = `color-primary` / `#0F172A`)

## Reference snippet
```html
<div class="mac-shell">
  <div class="mac-sidebar-backdrop" hidden></div>
  <aside class="mac-sidebar" style="width:260px">
    <div class="mac-sidebar-header">
      <span class="mac-sidebar-title">i24</span>
      <span class="mac-sidebar-badge">Prod</span>
    </div>
    <nav class="mac-sidebar-nav" aria-label="หลัก">
      <p class="mac-sidebar-group">ภาพรวม</p>
      <a class="mac-sidebar-item is-active" href="/dashboard" aria-current="page">แดชบอร์ด</a>
      <a class="mac-sidebar-item" href="/invoices">ใบกำกับ</a>
    </nav>
    <div class="mac-sidebar-footer">
      <button type="button" class="mac-sidebar-logout" aria-label="ออกจากระบบ">ออกจากระบบ</button>
    </div>
    <div class="mac-sidebar-resizer" role="separator" aria-orientation="vertical" aria-label="ปรับความกว้างเมนู"></div>
  </aside>
  <main class="mac-section"><!-- เนื้อหา --></main>
</div>
```
