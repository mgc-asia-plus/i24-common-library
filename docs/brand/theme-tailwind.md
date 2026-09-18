# Theme — Tailwind v4 (Luxury Clear Glass)

แปลง [design tokens](design-tokens.md) → Tailwind CSS v4 `@theme` + CSS variables สำหรับ light/dark

**Pin:** `tailwindcss@4.3.3`  
**Document contract:** Read theme map — git read; ผลลัพธ์คือ snippet `@theme` + `:root` + `[data-theme="dark"]`  
ผิดสัญญาถ้าไฟล์นี้กลายเป็น application template เต็ม (layout / component CSS / JS)

> snippet เป็น **ตัวอย่างอ้างอิงสั้น** สำหรับ copy ตั้งต้น — ไม่ใช่ template แอป

## แนวคิด
- semantic ผูกกับ CSS variable → `[data-theme="dark"]` override ค่า
- glass / gradient อ้าง [`effects.md`](effects.md) ไม่ประกาศสูตรซ้ำที่นี่
- พื้น `.mac-sidebar` = `color-sidebar-bg` / `--i24-sidebar-bg` = `#0F172A` ทั้งสองโหมด

## สัญญา mapping (ชื่อ token → `--color-*` / `--i24-*`)

| Semantic token | Tailwind `@theme` | CSS var (`:root` / `[data-theme]`) |
| :--- | :--- | :--- |
| `color-bg` | `--color-bg` / `--color-page-bg` | `--i24-page-bg` |
| `color-surface` | `--color-surface` | `--i24-surface` |
| `color-border` | `--color-border` | `--i24-border` |
| `color-primary` | `--color-primary` | `--i24-primary` |
| `color-primary-hover` | `--color-primary-hover` | `--i24-primary-hover` |
| `color-secondary-glass` | `--color-secondary-glass` | `--i24-secondary-glass` |
| `color-on-primary` | `--color-on-primary` | `--i24-on-primary` |
| `color-text` | `--color-text` | `--i24-text` |
| `color-text-muted` | `--color-text-muted` | `--i24-text-muted` |
| `color-text-empty` | `--color-text-empty` | `--i24-text-empty` |
| `color-table-header-bg` | `--color-table-header-bg` | `--i24-table-header-bg` |
| `color-table-header-text` | `--color-table-header-text` | `--i24-table-header-text` |
| `color-table-cell-border` | `--color-table-cell-border` | `--i24-table-cell-border` |
| `color-success` | `--color-success` | `--i24-success` |
| `color-warning` | `--color-warning` | `--i24-warning` |
| `color-danger` | `--color-danger` | `--i24-danger` |
| `color-gold` | `--color-gold` | `--i24-gold` |
| `color-logout-hover` | `--color-logout-hover` | `--i24-logout-hover` |
| `color-sidebar-bg` | `--color-sidebar-bg` | `--i24-sidebar-bg` |
| `color-sidebar-*` (อื่น) | `--color-sidebar-*` | `--i24-sidebar-*` — ค่าเดียวทั้งสองโหมด ยกเว้น `footer-bg` |
| `radius-btn` / `radius-pill` | `--radius-btn` / `--radius-pill` | `9999px` |
| `radius-card` | `--radius-card` | `20px` |
| `radius-table` | `--radius-table` | `14px` |
| `radius-sidebar-item` | `--radius-sidebar-item` | `6px` |
| `radius-box` | `--radius-box` | `10px` (input / กล่องทั่วไป) |
| `sidebar-width` | — | `--i24-sidebar-width` (`260px`) |

ค่า hex อ้าง [`palette.md`](palette.md) / [`design-tokens.md`](design-tokens.md) — ไฟล์นี้เป็นแผนที่ชื่อ ไม่ใช่ SSOT ของสี

## 1) นิยาม theme (`app.css`)
```css
@import "tailwindcss"; /* pin: tailwindcss@4.3.3 */

@theme {
  /* brand solid palette */
  --color-brand-red: #B0141B;
  --color-brand-navy: #0F172A;

  /* semantic (ผูก CSS var) */
  --color-bg: var(--i24-page-bg);
  --color-page-bg: var(--i24-page-bg);
  --color-text: var(--i24-text);
  --color-text-muted: var(--i24-text-muted);
  --color-surface: var(--i24-surface);
  --color-border: var(--i24-border);
  --color-table-header-bg: var(--i24-table-header-bg);
  --color-table-header-text: var(--i24-table-header-text);
  --color-success: var(--i24-success);
  --color-warning: var(--i24-warning);
  --color-danger: var(--i24-danger);

  /* Buttons + sidebar */
  --color-primary: var(--i24-primary); /* Navy Solid หลัก */
  --color-primary-hover: var(--i24-primary-hover);
  --color-secondary-glass: var(--i24-secondary-glass);
  --color-on-primary: var(--i24-on-primary);
  --color-sidebar-bg: var(--i24-sidebar-bg);

  /* radius */
  --radius-btn: 9999px;
  --radius-pill: 9999px;
  --radius-card: 20px;
  --radius-table: 14px;
  --radius-sidebar-item: 6px;
  --radius-box: 10px;

  --font-sans: -apple-system, BlinkMacSystemFont, "Inter", "Noto Sans Thai", system-ui, sans-serif;
}
```

## 2) ค่าตาม theme mode
```css
:root, [data-theme="light"] {
  --i24-text: #1A1A1A;
  --i24-text-muted: #6B7280;
  --i24-page-bg: #F5F5F7;
  --i24-surface: rgba(255, 255, 255, 0.70);
  --i24-border: rgba(20, 28, 50, 0.09);

  /* Primary: Navy Solid (#0F172A) — ปุ่ม / pagination / พื้น sidebar */
  --i24-primary: #0F172A;
  --i24-primary-hover: #06182B;
  --i24-on-primary: #FFFFFF;
  --i24-sidebar-bg: #0F172A; /* ไม่สลับ theme */

  --i24-secondary-glass: rgba(0, 0, 0, 0.06);
  --i24-table-header-bg: #E2E8F0;
  --i24-table-header-text: #334155;
  --i24-success: #137A47;
  --i24-warning: #B7791F;
  --i24-danger: #B0141B;
}

[data-theme="dark"] {
  --i24-text: #F3F4F6;
  --i24-text-muted: #9CA3AF;
  --i24-page-bg: #0A0A0F;
  --i24-surface: rgba(255, 255, 255, 0.07);
  --i24-border: rgba(255, 255, 255, 0.06);

  --i24-primary: #0F172A;
  --i24-primary-hover: #1D4B82;
  --i24-on-primary: #FFFFFF;
  --i24-sidebar-bg: #0F172A; /* ไม่สลับ theme */

  --i24-secondary-glass: rgba(255, 255, 255, 0.12);
  --i24-table-header-bg: rgba(255, 255, 255, 0.06);
  --i24-table-header-text: #9CA3AF;
  --i24-success: #3BB273;
  --i24-warning: #D6A24A;
  --i24-danger: #B0141B;
}
```

## 3) Web fonts (optional)
```html
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Noto+Sans+Thai:wght@400;500;600;700&display=swap" rel="stylesheet">
```

สูตร `.glass` / gradient อยู่ที่ [`effects.md`](effects.md)

## 4) ใช้ใน markup
```html
<body class="text-[--color-text]" style="background:var(--i24-page-bg)">
  <button class="btn-primary">เริ่มใช้งาน</button>
  <button class="btn-secondary">ดูเอกสาร</button>
</body>
```

## หมายเหตุต่อ stack
- **Go monolith**: build CSS นี้ → `go:embed` (ดู [`../stacks/go-monolith.md`](../stacks/go-monolith.md))
- **Next.js**: import ที่ root layout (ดู [`../stacks/nextjs.md`](../stacks/nextjs.md))
- สลับ `data-theme` โดย [`../components/theme-mode.md`](../components/theme-mode.md); gradient/glass/a11y เต็มที่ [`effects.md`](effects.md)
