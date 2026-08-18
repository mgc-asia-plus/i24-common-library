# Theme — Tailwind v4

วิธีแปลง [design tokens](design-tokens.md) → Tailwind CSS v4 โดยใช้ `@theme` + CSS variables สำหรับสลับ light/dark

> snippet ด้านล่างเป็น **ตัวอย่างอ้างอิง** ไม่ใช่ไฟล์สำเร็จที่ต้อง maintain — แต่ละโปรเจกต์ก็อปตั้งต้นแล้วปรับได้

## แนวคิด
- primitive + semantic (light) ประกาศใน `@theme` เพื่อให้ Tailwind gen utility (`bg-primary`, `text-muted` ฯลฯ)
- ค่า semantic ผูกกับ CSS variable → `dark` mode แค่ override ตัวแปร ไม่ต้องเปลี่ยน class

## 1) นิยาม theme (`app.css`)
```css
@import "tailwindcss";

@theme {
  /* primitive — brand (ค่าจาก palette.md; red-500/coral-400 ยืนยันจากโลโก้) */
  --color-brand-red-50:  #FDECED;
  --color-brand-red-100: #FBD0D2;
  --color-brand-red-400: #F04E52;
  --color-brand-red-500: #EC2129;
  --color-brand-red-600: #C81B22;
  --color-brand-red-700: #AA171D;
  --color-brand-coral-300: #F7A48A;
  --color-brand-coral-400: #F48569;
  --color-brand-coral-500: #F1684D;

  /* semantic — ผูกกับ CSS var เพื่อสลับ theme */
  --color-bg:            var(--i24-bg);
  --color-surface:       var(--i24-surface);
  --color-border:        var(--i24-border);
  --color-text:          var(--i24-text);
  --color-text-muted:    var(--i24-text-muted);
  --color-primary:       var(--i24-primary);
  --color-primary-hover: var(--i24-primary-hover);
  --color-on-primary:    var(--i24-on-primary);
  --color-accent:        var(--i24-accent);

  /* radius / shadow / font */
  --radius-md: 8px;
  --radius-pill: 9999px;
  --font-sans: "Inter", "Noto Sans Thai", system-ui, sans-serif;
}
```

## 2) ค่าตาม theme mode
```css
:root, [data-theme="light"] {
  --i24-bg: #FFFFFF;        --i24-surface: #F7F7F8;
  --i24-border: #D1D5DB;    --i24-text: #1A1A1A;
  --i24-text-muted: #6B7280;
  --i24-primary: #EC2129;   --i24-primary-hover: #C81B22;
  --i24-on-primary: #FFFFFF; --i24-accent: #F48569;
}
[data-theme="dark"] {
  --i24-bg: #0F1115;        --i24-surface: #171A21;
  --i24-border: #2A2F3A;    --i24-text: #F3F4F6;
  --i24-text-muted: #9CA3AF;
  --i24-primary: #EC2129;   --i24-primary-hover: #F04E52;
  --i24-on-primary: #FFFFFF; --i24-accent: #F7A48A;
}
```

## 3) ใช้ใน markup
```html
<body class="bg-bg text-text">
  <button class="bg-primary text-on-primary rounded-pill px-5 py-2 hover:bg-primary-hover">
    บันทึก
  </button>
  <p class="text-text-muted">คำอธิบายรอง</p>
</body>
```

## หมายเหตุต่อ stack
- **Go monolith**: ไฟล์ CSS นี้ build ด้วย Tailwind CLI แล้ว `go:embed` (ดู [`../stacks/go-monolith.md`](../stacks/go-monolith.md))
- **Next.js**: import `app.css` ที่ root layout (ดู [`../stacks/nextjs.md`](../stacks/nextjs.md))
- การสลับค่า `data-theme` ทำโดย component ใน [`../components/theme-mode.md`](../components/theme-mode.md)

## กติกา
- แก้ค่าสีที่ [`palette.md`](palette.md)/[`design-tokens.md`](design-tokens.md) ก่อน แล้วสะท้อนมาที่ snippet นี้
- ห้ามเพิ่มสีนอก token ลงใน `@theme` โดยไม่ผ่านการอัปเดต tokens
