# Nav / Header

## Purpose
แถบนำทางบนสุด — โลโก้ i24 (asset จริง), เมนูหลัก, ปุ่ม theme mode, เมนูผู้ใช้  
ผิว Luxury Clear Glass = แถบกระจกใสทรง pill ลอย ใช้สูตร `surface-white-glass` จาก [`../brand/effects.md`](../brand/effects.md) (ห้ามคิด blur/opacity เอง)

## Anatomy
```
╭───────────────────────────────────────────────╮  ← glass pill (sticky)
│ [i24 logo]  เมนู1 เมนู2 เมนู3 ...   [🌓] [user] │
╰───────────────────────────────────────────────╯
```
- ซ้าย: โลโก้จริง `i24_LOGO.svg` เป็นลิงก์กลับหน้าแรก — ไม่ใช้กล่องตัวอักษร
- กลาง/ซ้าย: เมนูหลัก
- ขวา: [theme-mode](theme-mode.md) toggle + เมนูผู้ใช้
- viewport แคบ: เมนูยุบเป็น hamburger → drawer/disclosure

## Variants
| Variant | เมื่อไหร่ | visual |
|---------|----------|--------|
| `app` (default) | แอปที่มีหลายหน้า | แถบ `surface-white-glass` ทรง pill, sticky, กว้างเท่า container |
| `contained` | เนื้อหากลางจำกัดความกว้าง | เหมือน `app` แต่จำกัดความกว้างเนื้อหากลาง |

## Sizes
| ส่วน | ค่า |
|------|-----|
| ความสูงแถบ | 56px |
| sticky offset | `top: 14px` |
| โลโก้ | สูง 30px, กว้างอัตโนมัติ |
| มุมแถบ | `radius-pill` (9999px) |
| ช่องว่างรายการ | 24px |
| ลิงก์เมนู / hamburger / theme / user | เป้าแตะขั้นต่ำ 40×40px |

## States
| State | พฤติกรรม |
|-------|----------|
| `default` (ลิงก์) | `color-text` ความทึบ ~0.66 |
| `hover` | เพิ่มความทึบ; พื้น `color-secondary-glass` ได้ |
| `active` (หน้าปัจจุบัน) | `color-text` + `font-weight: 700` + `aria-current="page"` — ไม่ใช้สีแดง |
| `focus` | วง focus ที่มองเห็น (`color-focus-ring` = `color-primary` / `#0F172A`) บนทุกลิงก์/ปุ่ม |
| `disabled` | ลิงก์/ปุ่มที่กดไม่ได้: `color-text-muted`, ไม่มี hover, `aria-disabled="true"` |
| `open` (mobile drawer) | hamburger `aria-expanded="true"`; ปิดด้วย Esc |

## Tokens used
| Token | บทบาท |
|-------|--------|
| `color-surface` | พื้นแถบกระจก (recipe `surface-white-glass`) |
| `glass-hairline` (`color-border`) | เส้นบางของแถบ |
| `color-text` | ลิงก์เมนู / หน้าปัจจุบัน |
| `color-text-muted` | ลิงก์รอง / disabled |
| `color-secondary-glass` | พื้น hover ลิงก์ |
| `color-primary` / `--i24-primary` | วง `color-focus-ring` (navy `#0F172A`) |
| `radius-pill` | มุมแคปซูลของแถบ |

สูตรพื้น: `surface-white-glass` — อ้าง [`../brand/effects.md`](../brand/effects.md); มุมใช้ `radius-pill` แทน `radius-card` เพราะเป็นแถบแคปซูล  
`prefers-reduced-transparency` และ fallback ทึบใช้ค่าใน effects — ห้ามคิด blur ใหม่

## Accessibility
- ครอบด้วย `<header>` + `<nav aria-label="หลัก">`
- โลโก้เป็นลิงก์กลับหน้าแรก + `aria-label="i24 หน้าแรก"`; `<img alt="i24">` (ไม่ปล่อยว่าง)
- หน้าปัจจุบัน `aria-current="page"`
- hamburger: `<button type="button">` + `aria-expanded` + `aria-controls`; เป้าแตะ ≥ 40×40px
- theme toggle / เมนูผู้ใช้: มี `aria-label`; เป้าแตะ ≥ 40×40px
- คีย์บอร์ด: Tab วนทุกลิงก์/ปุ่ม; Enter เปิดลิงก์หรือเมนู; Esc ปิด drawer แล้วคืนโฟกัสไป hamburger
- วง focus ที่มองเห็นบนทุก control (`color-focus-ring` = `color-primary` / `#0F172A`)
- แถบแก้วต้องคง contrast ของข้อความ (ดู [`../brand/effects.md`](../brand/effects.md))

## Reference snippet
```html
<header class="app">
  <nav aria-label="หลัก">
    <a href="/" aria-label="i24 หน้าแรก">
      <img src="/static/i24_LOGO.svg" alt="i24" />
    </a>
    <a href="/dashboard" aria-current="page">แดชบอร์ด</a>
    <a href="/invoices">ใบแจ้งหนี้</a>
    <button type="button" aria-label="สลับธีม">🌓</button>
  </nav>
</header>
```
โลโก้: แต่ละ stack วาง `i24_LOGO.svg` เป็น static asset — ดู [footer.md](footer.md)
