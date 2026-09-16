# Nav / Header

## Purpose
แถบนำทางบนสุด — โลโก้ i24 (จริง), เมนูหลัก, ปุ่ม theme mode, เมนูผู้ใช้ (ธีม Luxury Clear Glass = แถบกระจกใสทรง pill ลอย)

## Anatomy
```
╭───────────────────────────────────────────────╮  ← glass pill (sticky)
│ [i24 logo]  เมนู1 เมนู2 เมนู3 ...   [🌓] [user] │
╰───────────────────────────────────────────────╯
```
- ซ้าย: **โลโก้จริง** `i24_LOGO.svg` (เป็นลิงก์กลับหน้าแรก) — ไม่ใช้กล่องตัวอักษร
- กลาง/ซ้าย: เมนูหลัก
- ขวา: [theme-mode](theme-mode.md) toggle + เมนูผู้ใช้

## Variants
- `app` (default) — glass pill, sticky (`top:14px`), เต็มความกว้าง container
- `contained` — จำกัดความกว้างเนื้อหากลาง

## States
- **link active**: `color-text` + `font-weight:700` (ไม่ใช้สีแดง เพื่อความสุขุมของธีม luxury) + `aria-current="page"`
- **link default**: `color-text` opacity ~0.66
- **link hover**: เพิ่ม opacity / พื้น `grad-brand-soft`
- **mobile**: ยุบเมนูเป็น hamburger → drawer/disclosure
- **focus**: ทุกลิงก์/ปุ่มมี focus ring (`color-focus-ring` = navy)

## Tokens used
`glass-*` (nav = clear glass, blur ~7px), `glass-border`, `glass-shadow`, `color-text`, `color-text-muted`, `color-focus-ring`, `radius-pill`, `space-5/6`

## Accessibility
- ครอบด้วย `<header>` + `<nav aria-label="หลัก">`
- **โลโก้เป็นลิงก์กลับหน้าแรก** + `aria-label="i24 หน้าแรก"`; `<img alt="i24">` (ไม่ปล่อยว่าง)
- เมนูปัจจุบัน `aria-current="page"`
- hamburger: `<button aria-expanded aria-controls>`
- เมนูใช้คีย์บอร์ดได้ (Tab/Enter/Esc ปิด drawer)
- แถบ glass ต้องคง contrast ของข้อความ (ดู [`../brand/effects.md`](../brand/effects.md))

## Reference snippet
```html
<header class="app" style="position:sticky;top:14px;z-index:20">
  <nav aria-label="หลัก"
       style="display:flex;align-items:center;gap:24px;height:56px;padding:0 24px;border-radius:9999px;background:rgba(255,255,255,0.35);backdrop-filter:blur(20px) saturate(180%);-webkit-backdrop-filter:blur(20px) saturate(180%);border:1px solid rgba(255,255,255,0.4);box-shadow:0 4px 20px rgba(0,0,0,0.04)">
    <a href="/" aria-label="i24 หน้าแรก" style="display:inline-flex;align-items:center">
      <img src="/static/i24_LOGO.svg" alt="i24" style="height:30px;width:auto" />
    </a>
    <a href="/dashboard" aria-current="page" class="text-[--color-text]" style="font-weight:700">แดชบอร์ด</a>
    <a href="/invoices" class="text-[--color-text]" style="opacity:.66">ใบแจ้งหนี้</a>
    <div style="margin-left:auto;display:flex;gap:12px;align-items:center">
      <!-- theme-mode toggle (Pill button) -->
      <!-- user menu -->
    </div>
  </nav>
</header>
```
> โลโก้: แต่ละ stack วาง `i24_LOGO.svg` เป็น static asset (Go `go:embed` static / Next `public/`) — ดู [`footer.md`](footer.md)
