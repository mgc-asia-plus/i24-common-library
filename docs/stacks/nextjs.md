# Stack: Next.js (Frontend)

**สถานะ: v1 (เต็ม)** — แนวทาง setup frontend ให้ใช้ธีม/component มาตรฐาน i24
*อ้าง SSOT ที่ [`../brand/`](../brand/design-tokens.md) และ [`../components/`](../components/README.md)*

## เหมาะกับ
SPA/SSR ฝั่ง React ที่ต้องการ UI แบรนด์ i24 (คู่กับ backend Nest.js/Express.js หรือ Go API)

## โครงไดเรกทอรีแนะนำ (App Router)
```
app/
  layout.tsx          root: import ธีม + ThemeProvider + FOUC guard
  page.tsx
  (routes)/...
components/
  ui/                 component กลางตาม spec (Button, Badge, Card, ...)
  layout/             NavHeader, ThemeToggle
lib/                  fetcher, utils
styles/
  app.css             Tailwind v4 @theme (ดู brand/theme-tailwind.md)
```

## Theme setup (Tailwind v4)
1. `styles/app.css` = `@import "tailwindcss";` + `@theme` + `[data-theme]` ตาม [`../brand/theme-tailwind.md`](../brand/theme-tailwind.md)
2. import `app.css` ใน `app/layout.tsx`
3. **FOUC guard**: ใส่ inline script set `data-theme` ใน `<head>` ก่อน hydrate (ดู [`../components/theme-mode.md`](../components/theme-mode.md))
4. ThemeProvider (client) จัดการ toggle + persist `localStorage['i24-theme']`

## Component convention
- component กลางอยู่ `components/ui/` implement ตาม spec ใน [`../components/`](../components/README.md)
- ตั้ง props ตามที่ spec แนะ (`variant`, `size`, `loading`, ...)
- ใช้ Tailwind class ที่ผูก semantic token (`bg-primary`, `text-text`, ...) — ห้าม hardcode hex
- แยก server/client component ตามการใช้ state; theme toggle เป็น client

## Data / API
- เรียก backend ผ่าน `lib/fetcher` — payload JSON snake_case ตาม [`../conventions/json-api.md`](../conventions/json-api.md) (map เป็น camelCase ที่ boundary ถ้าต้องการ)
- จัดการ error state ตาม [`../components/alert.md`](../components/alert.md)

## Accessibility
- ตาม a11y ในแต่ละ component spec
- ใช้ semantic HTML + `next/link` สำหรับ nav

## Checklist เริ่มโปรเจกต์ (สรุป — เต็มดู [`../scaffolding.md`](../scaffolding.md))
- [ ] สร้าง Next.js (App Router, TS)
- [ ] ตั้ง Tailwind v4 + `styles/app.css` จาก tokens
- [ ] เพิ่ม FOUC guard + ThemeProvider ใน layout
- [ ] สร้าง `components/ui/` ตาม spec + NavHeader + ThemeToggle
- [ ] 🔒 ใส่ `<PoweredByFooter/>` ใน root layout ([`../components/footer.md`](../components/footer.md)) — **บังคับทุกหน้า** + วางโลโก้ที่ `public/`
- [ ] ตั้ง fetcher + convention JSON
