# Effects — Navy Translucent Glass & Frosted Gray Glass

มาตรฐานการจัดการพื้นผิวและเอฟเฟกต์ "ใสทะลุ" (Translucent Glassmorphism) สำหรับ i24-common-library

---

## 1. Primary Navy Solid Recipe (สีกรมท่าทึบ คมชัด ไร้ขอบ มนแคปซูลเท่า Badges)

```css
/* ปุ่มหลักสีกรมท่าทึบ ไร้ขอบ (มนแคปซูลเท่า Badges) */
.btn-primary, .btn-navy-solid {
  background: #0A2540;
  border: none;
  box-shadow: none;
  color: #FFFFFF;
  border-radius: 9999px; /* มนแคปซูลเท่า Badges */
  padding: 0 22px;
  font-weight: 600;
  transition: background 0.15s ease, transform 0.15s ease;
}
.btn-primary:hover, .btn-navy-solid:hover {
  background: #06182B;
  transform: translateY(-1px);
}
.btn-primary:active, .btn-navy-solid:active {
  transform: scale(0.98);
}

/* Dark Mode */
[data-theme="dark"] .btn-primary,
.dark .btn-primary {
  background: #153965;
  color: #FFFFFF;
}
[data-theme="dark"] .btn-primary:hover,
.dark .btn-primary:hover {
  background: #1D4B82;
}

/* Option: Navy ใสทะลุ (Variant) */
.btn-navy-glass {
  background: rgba(10, 37, 64, 0.75);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: none;
  box-shadow: none;
  color: #FFFFFF;
  border-radius: 9999px;
  padding: 0 22px;
}
.btn-navy-glass:hover {
  background: rgba(10, 37, 64, 0.88);
  transform: translateY(-1px);
}
```

---

## 2. Secondary เทากระจกใสทะลุ Recipe (ไร้ขอบ มนแคปซูลเท่า Badges)

```css
/* ปุ่มรองสีเทากระจกใสทะลุ ไร้ขอบ */
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
