# Effects — Navy Translucent Glass & Frosted Gray Glass

มาตรฐานการจัดการพื้นผิวและเอฟเฟกต์ "ใสทะลุ" (Translucent Glassmorphism) สำหรับ i24-common-library

สีในสูตรอ้างชื่อ token จาก [`design-tokens.md`](design-tokens.md) — hex / rgba ที่แสดงด้านล่างคือค่าปัจจุบันของ token ไม่ใช่ค่าอิสระ

---

## Document contract — Read effects

ไฟล์นี้คือ **SSOT ของสูตร glass / gradient** (`EffectRecipe`).

- Component spec, prototype, และ stack guide **ต้องอ้างชื่อ recipe จากไฟล์นี้**
- **ห้ามคิดค่า `blur` / `opacity` / sheen / capsule radius เอง** และห้ามใส่ `backdrop-filter` ที่ไม่ตรง recipe
- ผิดสัญญา: component ใส่ blur/opacity เอง, หรือใช้ Navy เก่า `rgba(10, 37, 64, …)` / `#0A2540` แทน `#0F172A` (`--i24-primary`)

---

## EffectRecipe registry

| Recipe | Token / CSS var | Blur | Opacity | Sheen | Radius | Shadow |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `btn-navy-solid` | `color-primary` / `--i24-primary` `#0F172A` | none | 1.0 (solid) | none | `radius-btn` **9999px** | none |
| `btn-navy-glass` | `primary-glass-bg` `rgba(15, 23, 42, 0.75)` | **16px** | 0.75 / hover 0.88 | none (borderless) | **9999px** | none |
| `btn-gray-glass` | `color-secondary-glass` Frosted Gray | **16px** | 0.06 light / 0.12 dark | `secondary-glass-sheen` | **9999px** | none (borderless pill) |
| `surface-white-glass` | `color-surface` | **24px** | 0.70 light / 0.07 dark | hairline `glass-hairline` | `radius-card` **20px** | light: `0 10px 30px -5px rgba(0,0,0,0.04)` |
| `crimson-glass-tint` | `color-logout-hover` / `status-danger-bg` Deep Crimson | none | 0.12 light / 0.18 dark | none | inherited | none |
| `grad-table-row-hover` | `grad-table-row-hover` | none | crimson `rgba(176,20,27,0.06)` + navy `rgba(15,23,42,0.08)` | none | inherited | none |

Navy ในสูตรแก้ว / gradient ใช้ **`rgba(15, 23, 42, …)`** เท่านั้น (`#0F172A`) — ห้าม `rgba(10, 37, 64, …)`.

---

## 1. Primary Navy Solid Recipe (สีกรมท่าทึบ คมชัด ไร้ขอบ มนแคปซูลเท่า Badges)

```css
/* ปุ่มหลักสีกรมท่าทึบ ไร้ขอบ (มนแคปซูลเท่า Badges)
   color-primary / --i24-primary = #0F172A */
.btn-primary, .btn-navy-solid {
  background: var(--i24-primary, #0F172A);
  border: none;
  box-shadow: none;
  color: var(--color-on-primary, #FFFFFF);
  border-radius: 9999px; /* radius-btn — มนแคปซูลเท่า Badges */
  padding: 0 22px;
  font-weight: 600;
  transition: background 0.15s ease, transform 0.15s ease;
}
.btn-primary:hover, .btn-navy-solid:hover {
  background: #06182B; /* color-primary-hover (light) */
  transform: translateY(-1px);
}
.btn-primary:active, .btn-navy-solid:active {
  transform: scale(0.98);
}

/* Dark Mode — primary คง Navy Solid เดียวกันทั้งสองโหมด */
[data-theme="dark"] .btn-primary,
.dark .btn-primary {
  background: var(--i24-primary, #0F172A);
  color: var(--color-on-primary, #FFFFFF);
}
[data-theme="dark"] .btn-primary:hover,
.dark .btn-primary:hover {
  background: #1D4B82; /* color-primary-hover (dark) */
}

/* Option: Navy ใสทะลุ (Variant) — primary-glass-bg / primary-glass-hover */
.btn-navy-glass {
  background: rgba(15, 23, 42, 0.75);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: none;
  box-shadow: none;
  color: #FFFFFF;
  border-radius: 9999px;
  padding: 0 22px;
}
.btn-navy-glass:hover {
  background: rgba(15, 23, 42, 0.88);
  transform: translateY(-1px);
}
```

---

## 2. Secondary เทากระจกใสทะลุ Recipe (Frosted Gray Glass — ไร้ขอบ มนแคปซูลเท่า Badges)

```css
/* ปุ่มรองสีเทากระจกใสทะลุ ไร้ขอบ — color-secondary-glass
   sheen token: secondary-glass-sheen (ใช้กับพื้นผิวแก้วที่มีไฮไลต์;
   ปุ่มแคปซูลไร้ขอบคง box-shadow: none ตามสูตร pill) */
.btn-gray-glass {
  background: rgba(0, 0, 0, 0.06);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: none;
  box-shadow: none;
  color: #1A1A1A;
  border-radius: 9999px; /* มนแคปซูลเท่า Badges */
  padding: 0 22px;
  font-weight: 600;
  transition: background 0.15s ease, transform 0.15s ease;
}
.btn-gray-glass:hover {
  background: rgba(0, 0, 0, 0.10);
  transform: translateY(-1px);
}
.btn-gray-glass:active {
  transform: scale(0.98);
}

/* Dark Mode Smoke Glass */
[data-theme="dark"] .btn-gray-glass {
  background: rgba(255, 255, 255, 0.12);
  color: #FFFFFF;
}
[data-theme="dark"] .btn-gray-glass:hover {
  background: rgba(255, 255, 255, 0.18);
}

/* Sheen — secondary-glass-sheen (พื้นผิว Frosted Gray ที่ไม่ใช่ปุ่มแคปซูลไร้ขอบ) */
.frosted-gray-sheen {
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.75);
}
[data-theme="dark"] .frosted-gray-sheen {
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.20);
}
```

---

## 3. Pill Capsule Variant (ไร้ขอบ)

```css
.btn-navy-glass.pill {
  border-radius: 9999px;
  border: none;
  padding: 0 22px;
}
.btn-gray-glass.pill {
  border-radius: 9999px;
  border: none;
  padding: 0 22px;
}
```

---

## 4. White Translucent Glass (surface / card)

```css
/* color-surface — blur 24px; radius-card 20px */
.surface-white-glass {
  background: rgba(255, 255, 255, 0.70);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);
  border: none;
  box-shadow: 0 10px 30px -5px rgba(0, 0, 0, 0.04);
  border-radius: 20px;
}
[data-theme="dark"] .surface-white-glass {
  background: rgba(255, 255, 255, 0.07);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  box-shadow: none;
}
```

---

## 5. Deep Crimson glass + row-hover gradient

Navy ใน gradient ต้องเป็น `rgba(15, 23, 42, …)` ไม่ใช่ `rgba(10, 37, 64, …)`.

```css
/* color-logout-hover / status-danger-bg — Deep Crimson #B0141B */
.crimson-glass-tint {
  background: rgba(176, 20, 27, 0.12);
}
[data-theme="dark"] .crimson-glass-tint {
  background: rgba(176, 20, 27, 0.18);
}

/* grad-table-row-hover */
.mac-table tbody tr:hover {
  background: linear-gradient(135deg, rgba(176, 20, 27, 0.06), rgba(15, 23, 42, 0.08));
}
[data-theme="dark"] .mac-table tbody tr:hover {
  background: linear-gradient(135deg, rgba(236, 33, 41, 0.12), rgba(46, 78, 166, 0.16));
}
```

---

## Accessibility

- Contrast ของข้อความบนปุ่ม primary: `color-on-primary` `#FFFFFF` บน `--i24-primary` `#0F172A` — ดูตารางใน [`palette.md`](palette.md)
- `prefers-reduced-transparency`: ปิด blur แล้วใช้พื้นทึบเทียบเท่า opacity ของ recipe
- เบราว์เซอร์ที่ไม่รองรับ `backdrop-filter` ใช้ fallback ทึบ — ห้ามคิดค่าใหม่

```css
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .btn-navy-glass { background: #0F172A; }
  .btn-gray-glass { background: #E5E7EB; }
  [data-theme="dark"] .btn-gray-glass { background: #2A2F3A; }
  .surface-white-glass { background: #FFFFFF; }
  [data-theme="dark"] .surface-white-glass { background: #16161C; }
}

@media (prefers-reduced-transparency: reduce) {
  .btn-navy-glass,
  .btn-gray-glass,
  .surface-white-glass {
    backdrop-filter: none;
    -webkit-backdrop-filter: none;
  }
  .btn-navy-glass { background: #0F172A; }
  .btn-gray-glass { background: #E5E7EB; }
  [data-theme="dark"] .btn-gray-glass { background: #2A2F3A; }
  .surface-white-glass { background: #FFFFFF; }
  [data-theme="dark"] .surface-white-glass { background: #16161C; }
}
```
