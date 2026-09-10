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
  /* brand red */
  --color-red-500:#EC2129; --color-red-600:#B0141B; --color-red-700:#7E0E14;
  /* navy accent */
  --color-navy-400:#2E4EA6; --color-navy-500:#1E3A8A; --color-navy-600:#152C63;
  /* slate */
  --color-ink-900:#1A1D24; --color-ink-700:#333A46; --color-ink-500:#6B7482; --color-ink-300:#D2D7DF; --color-black:#0A0C11;

  /* semantic (ผูก CSS var) */
  --color-text:var(--i24-text); --color-text-muted:var(--i24-text-muted);
  --color-primary:var(--i24-primary); --color-on-primary:var(--i24-on-primary);
  --color-accent:var(--i24-accent); --color-focus:var(--i24-focus); --color-gold:var(--i24-gold);

  /* gradients */
  --gradient-brand: linear-gradient(135deg, #E11D27 0%, #A81319 100%);
  --gradient-accent: linear-gradient(135deg, #2A4AA0 0%, #152C63 100%);

  --radius-pill:9999px; --radius-lg:20px;
  --font-sans:-apple-system, BlinkMacSystemFont, "Inter", "Noto Sans Thai", system-ui, sans-serif;
}
```

## 2) ค่าตาม theme mode
```css
:root, [data-theme="light"] {
  --i24-text:#1A1D24; --i24-text-muted:#5C6675;
  --i24-primary:#EC2129; --i24-on-primary:#fff;
  --i24-accent:#1E3A8A; --i24-focus:#2E4EA6; --i24-gold:#A8811C;
  --i24-page-bg:#EEF0F4;
  /* clear glass */
  --i24-glass-tint:linear-gradient(135deg,rgba(255,255,255,.13),rgba(255,255,255,.02));
  --i24-glass-top:linear-gradient(180deg,rgba(255,255,255,.38),transparent 26%);
  --i24-glass-sheen:radial-gradient(135% 95% at 15% -14%,rgba(255,255,255,.50),transparent 50%);
  --i24-glass-gloss:linear-gradient(122deg,transparent 34%,rgba(255,255,255,.42) 45%,rgba(255,255,255,.10) 52%,transparent 62%);
  --i24-glass-border:rgba(255,255,255,.60); --i24-glass-hairline:rgba(20,28,50,.09);
  --i24-glass-bg-strong:rgba(255,255,255,.20);
}
[data-theme="dark"] {
  --i24-text:#EDEFF4; --i24-text-muted:#98A1B2;
  --i24-primary:#EC2129; --i24-on-primary:#fff;
  --i24-accent:#7C93E0; --i24-focus:#7C93E0; --i24-gold:#E7C873;
  --i24-page-bg:#0A0C11;
  --i24-glass-tint:linear-gradient(135deg,rgba(255,255,255,.07),rgba(255,255,255,.012));
  --i24-glass-top:linear-gradient(180deg,rgba(255,255,255,.16),transparent 26%);
  --i24-glass-sheen:radial-gradient(135% 95% at 15% -14%,rgba(255,255,255,.18),transparent 50%);
  --i24-glass-gloss:linear-gradient(122deg,transparent 34%,rgba(255,255,255,.18) 45%,rgba(255,255,255,.04) 52%,transparent 62%);
  --i24-glass-border:rgba(255,255,255,.16); --i24-glass-hairline:rgba(255,255,255,.08);
  --i24-glass-bg-strong:rgba(255,255,255,.075);
}
```

## 3) Web fonts + glass utility
```html
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Noto+Sans+Thai:wght@400;500;600;700&display=swap" rel="stylesheet">
```
```css
.glass {
  background: var(--i24-glass-gloss), var(--i24-glass-top), var(--i24-glass-sheen), var(--i24-glass-tint);
  backdrop-filter: blur(3px) saturate(135%) brightness(1.04);
  -webkit-backdrop-filter: blur(3px) saturate(135%) brightness(1.04);
  border:1px solid var(--i24-glass-border); border-radius:20px;
  box-shadow:
    0 0 0 1px rgba(20,28,50,.045), 0 1px 2px rgba(16,22,45,.05), 0 18px 42px rgba(16,22,45,.12),
    inset 0 1px 0 rgba(255,255,255,.95), inset 0 -1px 0 rgba(20,28,50,.05);
}
@supports not ((backdrop-filter:blur(1px)) or (-webkit-backdrop-filter:blur(1px))) { .glass{ background:var(--i24-glass-bg-strong);} }
@media (prefers-reduced-transparency: reduce) { .glass{ backdrop-filter:none; -webkit-backdrop-filter:none; background:var(--i24-glass-bg-strong);} }
```

## 3) ใช้ใน markup
```html
<body class="text-[--color-text]" style="background:var(--i24-page-bg)">
  <button class="rounded-pill px-6 h-11 text-white" style="background:var(--gradient-brand)">เริ่มใช้งาน</button>
  <button class="rounded-pill px-6 h-11 text-white" style="background:var(--gradient-accent)">ดูเอกสาร</button>
  <section class="glass rounded-[20px] p-7"> ... </section>
</body>
```

## หมายเหตุต่อ stack
- **Go monolith**: build CSS นี้ → `go:embed` (ดู [`../stacks/go-monolith.md`](../stacks/go-monolith.md))
- **Next.js**: import ที่ root layout (ดู [`../stacks/nextjs.md`](../stacks/nextjs.md))
- สลับ `data-theme` โดย [`../components/theme-mode.md`](../components/theme-mode.md); gradient/glass/a11y เต็มที่ [`effects.md`](effects.md)
