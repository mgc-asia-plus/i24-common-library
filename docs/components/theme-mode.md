# Theme Mode

## Purpose
ปุ่ม/ตัวควบคุมสลับธีมของแอประหว่าง **light / dark** (และ optional **system**) โดยเปลี่ยนค่า `data-theme` ที่ root

## กลไก
- ค่าปัจจุบันเก็บที่ attribute `data-theme` บน `<html>` (`light` | `dark`)
- ค่าถูกอ่านจาก [`../brand/theme-tailwind.md`](../brand/theme-tailwind.md) (`[data-theme="dark"]` override CSS variables)
- จำค่าที่ผู้ใช้เลือกใน `localStorage` key `i24-theme`
- โหมด `system`: ไม่ตั้งค่าตายตัว ตามด้วย `prefers-color-scheme`

## Variants
- `icon-toggle` (default) — ปุ่มไอคอน ☀/🌙 สลับ 2 ค่า
- `segmented` — ตัวเลือก 3 ค่า: Light / Dark / System

## States
- สะท้อนค่าปัจจุบัน (ไอคอน/ตัวเลือกที่ active)
- **focus**: ring `color-focus-ring`
- เปลี่ยนทันทีเมื่อคลิก (ไม่ต้อง reload)

## ลำดับการตัดสินค่าเริ่มต้น (init)
1. มีค่าใน `localStorage['i24-theme']` → ใช้ค่านั้น
2. ไม่มี → ตาม `prefers-color-scheme`
3. เขียน `data-theme` ให้ `<html>` **ก่อน paint** เพื่อกันจอกระพริบ (FOUC)

## Tokens used
`color-text`, `color-surface`, `color-focus-ring`, `radius-pill` — และค่าทั้งชุดสลับผ่าน semantic tokens

## Accessibility
- ปุ่มมี `aria-label` ชัด เช่น "สลับเป็นธีมมืด"
- ถ้าใช้ toggle แบบ 2 สถานะ พิจารณา `aria-pressed`
- segmented ใช้ `role="radiogroup"` + `role="radio"`
- ต้องใช้คีย์บอร์ดได้

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
<button type="button" aria-label="สลับธีม"
        class="h-9 w-9 grid place-items-center rounded-pill hover:bg-[--color-surface]"
        onclick="(function(){var h=document.documentElement,n=h.getAttribute('data-theme')==='dark'?'light':'dark';h.setAttribute('data-theme',n);localStorage.setItem('i24-theme',n);})()">
  🌓
</button>
```
> Go/HTMX: ปุ่มนี้เป็น static (JS เล็กฝั่ง client). React/Next.js: ห่อด้วย context provider ที่ set `documentElement` + persist
