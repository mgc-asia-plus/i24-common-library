# Theme — Tailwind v4 (Luxury Clear Glass)

แปลง [design tokens](design-tokens.md) → Tailwind CSS v4 + CSS variables สำหรับ light/dark
> snippet เป็น **ตัวอย่างอ้างอิง** — sync จาก `prototype/index.html`; แต่ละโปรเจกต์ก็อปตั้งต้นแล้วปรับได้

## แนวคิด
- semantic + effect ผูกกับ CSS variable → `[data-theme="dark"]` override ค่า
- surface หลักใช้ clear glass (ดู [`effects.md`](effects.md))

## 1) นิยาม theme (`app.css`)
```css
@import "tailwindcss";

@theme {
  /* brand solid palette */
  --color-brand-red: #B0141B;
  --color-brand-navy: #0A2540;

  /* semantic (ผูก CSS var) */
  --color-text: var(--i24-text);
  --color-text-muted: var(--i24-text-muted);
  --color-page-bg: var(--i24-page-bg);
  --color-surface: var(--i24-surface);
  --color-border: var(--i24-border);

  /* Buttons */
  --color-primary: var(--i24-primary); /* Navy Solid หลัก */
  --color-primary-hover: var(--i24-primary-hover);
  --color-secondary-glass: var(--i24-secondary-glass);
  --color-on-primary: #FFFFFF;

  /* radius */
  --radius-btn: 9999px; /* ทุกปุ่มมนแคปซูลเท่า Badges */
  --radius-box: 20px;   /* card ขาวใส */
  --radius-pill: 9999px;

  --font-sans: -apple-system, BlinkMacSystemFont, "Inter", "Noto Sans Thai", system-ui, sans-serif;
}
```

## 2) ค่าตาม theme mode
```css
:root, [data-theme="light"] {
  --i24-text: #1A1A1A;
  --i24-text-muted: #6B7280;
  --i24-page-bg: #FFFFFF;
  --i24-surface: rgba(255, 255, 255, 0.70);
  --i24-border: transparent;

  /* Primary: Navy Solid (#0A2540) หลัก */
  --i24-primary: #0A2540;
  --i24-primary-hover: #06182B;

  /* Secondary: เทากระจกใสทะลุ */
  --i24-secondary-glass: rgba(0, 0, 0, 0.06);
  --i24-secondary-glass-hover: rgba(0, 0, 0, 0.10);
  --i24-secondary-glass-border: transparent;
}

[data-theme="dark"] {
  --i24-text: #F3F4F6;
  --i24-text-muted: #9CA3AF;
  --i24-page-bg: #0A0A0F;
  --i24-surface: rgba(255, 255, 255, 0.07);
  --i24-border: transparent;

  /* Primary: Navy Solid (Dark Mode) */
  --i24-primary: #153965;
  --i24-primary-hover: #1D4B82;

  /* Secondary: เทากระจกใสทะลุ (Smoke) */
  --i24-secondary-glass: rgba(255, 255, 255, 0.12);
  --i24-secondary-glass-hover: rgba(255, 255, 255, 0.18);
  --i24-secondary-glass-border: transparent;
}
```

## 3) Web fonts + glass utility
```html
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Noto+Sans+Thai:wght@400;500;600;700&display=swap" rel="stylesheet">
```
```css
.glass {
  background: rgba(255, 255, 255, 0.70);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);
  border: none;
  box-shadow: 0 10px 30px -5px rgba(0, 0, 0, 0.04);
  border-radius: 20px;
}
[data-theme="dark"] .glass {
  background: rgba(255, 255, 255, 0.07);
  backdrop-filter: blur(24px);
  border: none;
  box-shadow: none;
}
```

## 4) ใช้ใน markup
```html
<body class="text-[--color-text]" style="background:var(--i24-page-bg)">
  <!-- Primary: Navy Solid หลัก (#0A2540) ทรงแคปซูลไร้ขอบ -->
  <button class="btn-primary">เริ่มใช้งาน</button>
  
  <!-- Secondary: เทากระจกใสทะลุ ทรงแคปซูลไร้ขอบ -->
  <button class="btn-secondary">ดูเอกสาร</button>
</body>
```

## หมายเหตุต่อ stack
- **Go monolith**: build CSS นี้ → `go:embed` (ดู [`../stacks/go-monolith.md`](../stacks/go-monolith.md))
- **Next.js**: import ที่ root layout (ดู [`../stacks/nextjs.md`](../stacks/nextjs.md))
- สลับ `data-theme` โดย [`../components/theme-mode.md`](../components/theme-mode.md); gradient/glass/a11y เต็มที่ [`effects.md`](effects.md)
