# Theme Mode

## Purpose
ปุ่ม/ตัวควบคุมสลับธีมของแอประหว่าง **light / dark** (และทางเลือก **system**) โดยเขียน `[data-theme]` ที่ root — ใช้เมื่อผลิตภัณฑ์รองรับสองโหมดตาม semantic tokens

กลไก: ค่าปัจจุบันอยู่ที่ `data-theme` บน `<html>` (`light` | `dark`); แผนที่ตัวแปรอ่านจาก [`../brand/theme-tailwind.md`](../brand/theme-tailwind.md); จำค่าที่ผู้ใช้เลือกใน `localStorage` key `i24-theme`; โหมด `system` ตาม `prefers-color-scheme`

ลำดับค่าเริ่มต้น (กันจอกระพริบ — เขียน **ก่อน paint**):
1. มี `localStorage['i24-theme']` → ใช้ค่านั้น
2. ไม่มี → ตาม `prefers-color-scheme`
3. ตั้ง `data-theme` บน `<html>`

## Anatomy
```
[ icon-toggle: ☀ / 🌙 ]
หรือ
[ Light | Dark | System ]   ← segmented
```
- บังคับ: ปุ่มหรือกลุ่มตัวเลือกที่เปลี่ยน `data-theme`
- ทางเลือก: ป้ายข้อความประกอบไอคอน

## Variants

| Variant | เมื่อไหร่ที่ใช้ | Visual |
|---------|----------------|--------|
| `icon-toggle` (default) | สลับ 2 ค่า light/dark | ปุ่มไอคอน; มน `radius-pill`; พื้นโปร่งหรือ `color-surface` เมื่อ hover |
| `segmented` | ให้เลือก 3 ค่า Light / Dark / System | กลุ่มปุ่ม; ตัวที่ active ใช้ `color-primary` / `--i24-primary` (`#0F172A`) + `color-on-primary` |

ห้ามคิด blur/opacity ของพื้นผิวเอง — ถ้าใช้แก้ว ให้อ้าง recipe ใน [`../brand/effects.md`](../brand/effects.md)

## Sizes

| Size | เป้าหมายแตะ | หมายเหตุ |
|------|-------------|----------|
| `md` (default) | **40×40px** | ปุ่มไอคอนอย่างน้อย 40×40; segmented แต่ละช่องไม่ต่ำกว่านี้ |

## States

| State | พฤติกรรม |
|-------|----------|
| **default** | สะท้อนค่าปัจจุบัน (ไอคอน / ตัวเลือกที่ active); คลิกแล้วเปลี่ยนทันที ไม่ reload |
| **focus** | วงแหวน `color-focus-ring` (ค่า = `color-primary` / `--i24-primary` `#0F172A`) |
| **disabled** | ล็อกธีมชั่วคราว — `disabled` / `aria-disabled`; ไม่รับคลิก |

## Tokens used
- `color-text` (`#1A1A1A` / `#F3F4F6`) — ไอคอน / ป้าย
- `color-surface` — พื้น hover / segmented track
- `color-primary` / `--i24-primary` (`#0F172A`) — ช่องที่เลือกใน segmented
- `color-on-primary` (`#FFFFFF`)
- `radius-pill` (9999px)
- `color-focus-ring` — focus ที่มองเห็น (กฎร่วม SpecIndex); ค่าวงแหวน = `color-primary`

ชุดสีทั้งหน้าสลับผ่าน semantic tokens ใน [`../brand/design-tokens.md`](../brand/design-tokens.md) เมื่อ `[data-theme]` เปลี่ยน (พื้น `.mac-sidebar` ยังเป็น `color-sidebar-bg` ไม่สลับ)

## Accessibility
- ปุ่มมี `aria-label` ชัด เช่น "สลับเป็นธีมมืด"
- Toggle 2 สถานะ: `aria-pressed` ตามค่าปัจจุบัน
- Segmented: `role="radiogroup"` + `role="radio"` + `aria-checked`
- คีย์บอร์ด: `Tab` โฟกัส; `Enter` / `Space` สลับ; ลูกศรซ้ายขวาใน radiogroup
- Focus ที่มองเห็น: `color-focus-ring`
- พื้นที่แตะ ≥ **40×40px**

## Reference snippet
กันจอกระพริบ (วางใน `<head>` ก่อน CSS):
```html
<script>
  (function () {
    var t = localStorage.getItem('i24-theme');
    if (!t) t = matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
    document.documentElement.setAttribute('data-theme', t);
  })();
</script>
```

ปุ่ม toggle:
```html
<button type="button" aria-label="สลับธีม" aria-pressed="false"
        class="h-10 w-10 grid place-items-center rounded-full
               focus-visible:outline-2 focus-visible:outline-[--color-focus-ring]"
        onclick="(function(){var h=document.documentElement,n=h.getAttribute('data-theme')==='dark'?'light':'dark';h.setAttribute('data-theme',n);localStorage.setItem('i24-theme',n);})()">
  🌓
</button>
```
