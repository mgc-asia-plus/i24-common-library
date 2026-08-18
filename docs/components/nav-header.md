# Nav / Header

## Purpose
แถบนำทางบนสุดของแอป — โลโก้ i24, เมนูหลัก, ปุ่ม theme mode, เมนูผู้ใช้

## Anatomy
```
┌───────────────────────────────────────────────┐
│ [logo i24]  เมนู1 เมนู2 เมนู3 ...   [🌓] [user] │
└───────────────────────────────────────────────┘
```
- ซ้าย: โลโก้ (พื้นแบรนด์ `brand-red-500`) + ชื่อระบบ
- กลาง/ซ้าย: เมนูหลัก (active = `color-primary`)
- ขวา: [theme-mode](theme-mode.md) toggle + เมนูผู้ใช้

## Variants
- `app` (default) — เต็มความกว้าง, sticky บนสุด
- `contained` — จำกัดความกว้างเนื้อหากลาง

## States
- **link active**: ข้อความ `color-primary` + เส้นใต้/แถบ 2px
- **link hover**: พื้น `color-surface`
- **mobile**: ยุบเมนูเป็นปุ่ม hamburger → เปิด drawer/disclosure
- **focus**: ทุกลิงก์/ปุ่มมี focus ring

## Tokens used
`brand-red-500`, `color-bg`, `color-surface`, `color-border`, `color-text`, `color-primary`, `space-4/6`, `shadow-sm`

## Accessibility
- ครอบด้วย `<header>` + `<nav aria-label="หลัก">`
- เมนูปัจจุบันตั้ง `aria-current="page"`
- hamburger: `<button aria-expanded aria-controls>`
- โลโก้เป็นลิงก์กลับหน้าแรกและมีข้อความ (alt/`aria-label` "i24 หน้าแรก")
- เมนูใช้คีย์บอร์ดได้ (Tab/Enter/Esc ปิด drawer)

## Reference snippet
```html
<header class="sticky top-0 bg-[--color-bg] border-b border-[--color-border] shadow-sm">
  <nav aria-label="หลัก" class="flex items-center gap-6 px-6 h-14">
    <a href="/" aria-label="i24 หน้าแรก" class="font-bold text-[--color-primary]">i24</a>
    <a href="/dashboard" aria-current="page" class="text-[--color-primary] font-medium">แดชบอร์ด</a>
    <a href="/invoices" class="text-[--color-text] hover:text-[--color-primary]">ใบแจ้งหนี้</a>
    <div class="ml-auto flex items-center gap-3">
      <!-- theme-mode toggle -->
      <!-- user menu -->
    </div>
  </nav>
</header>
```
