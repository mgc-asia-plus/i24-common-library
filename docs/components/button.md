# Button — Navy Solid & Frosted Gray Glass

## Purpose
ปุ่มมาตรฐานของระบบ i24 สำหรับ action สำคัญและ action รอง
- **Primary**: **Navy Solid** (`#0A2540`) — สีกรมท่าเข้มทึบ คมชัด โดดเด่น Contrast สูง AAA สำหรับ Action หลัก
- **Secondary**: **เทากระจกใสทะลุ** (`rgba(0, 0, 0, 0.06)` light / `rgba(255, 255, 255, 0.12)` dark + blur 16px) — ใช้สำหรับ Action รอง หรือการควบคุมทั่วไป

---

## Variants & Styles

| Variant | สไตล์ & พื้นผิว | ขอบ & เงา | ข้อความ | เมื่อไหร่ที่ใช้ |
|---|---|---|---|---|
| `primary` (Navy Solid) | สีกรมท่าทึบ `#0A2540` (Dark: `#153965`) | ไร้ขอบ (`border: none; box-shadow: none;`) | ขาว `#FFFFFF` (Contrast สูง AAA) | Action หลัก (บันทึก, จอง, ยืนยัน) |
| `secondary` (Gray Glass) | `rgba(0, 0, 0, 0.06)` (Dark: `rgba(255, 255, 255, 0.12)`) + `backdrop-filter: blur(16px)` | ไร้ขอบ (`border: none; box-shadow: none;`) | สีข้อความตามธีม (`#1A1A1A` / `#FFFFFF`) | Action รอง (ยกเลิก, รายละเอียด, ย้อนกลับ) |
| `primary-glass` (Option) | `rgba(10, 37, 64, 0.75)` + `backdrop-filter: blur(16px)` | ไร้ขอบ | ขาว `#FFFFFF` | Action ทางเลือกแบบโปร่งแสง |
| `danger` | สีแดง `#DC2626` ทึบ | ไร้ขอบ | ขาว `#FFFFFF` | Action ลบหรือทำลายข้อมูล |
| `ghost` | พื้นโปร่งใส (transparent) | ไร้ขอบ | สีตามธีม หรือ Navy | เมนูใน Toolbar / Action เบา |

### ความมน (Border Radius)
> **ทุกปุ่มในระบบใช้ความมนเท่ากับ Badges คือทรง Pill Capsule: `border-radius: 9999px;` (`rounded-full`)**
> ความมนกลมเนียนแบบแคปซูล ไร้ขอบ (border: none; box-shadow: none;) สไตล์ iOS / Instagram

---

## Ready-to-use Templates (คัดลอกไปใช้ได้ทันที)

### 1. Pure CSS

```css
/* ทุกปุ่มใช้ความมนแคปซูลเท่า Badges (9999px) และไร้ขอบ */
.btn-primary,
.btn-navy-solid,
.btn-navy-glass,
.btn-secondary,
.btn-gray-glass,
.btn-danger,
.btn-ghost {
  border-radius: 9999px; /* มนแคปซูลเท่า Badges */
  border: none;
  box-shadow: none;
  height: 40px;
  padding: 0 22px;
  font-weight: 600;
  font-size: 14px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  cursor: pointer;
  text-decoration: none;
  transition: background 0.15s ease, transform 0.15s ease;
}
.btn-primary:active,
.btn-navy-solid:active,
.btn-navy-glass:active,
.btn-secondary:active,
.btn-gray-glass:active {
  transform: scale(0.98);
}

/* ===================================================
   PRIMARY: Navy Solid (#0A2540) ไร้ขอบ มนเท่า Badges
   =================================================== */
.btn-primary,
.btn-navy-solid {
  background: #0A2540;
  color: #FFFFFF;
}
.btn-primary:hover,
.btn-navy-solid:hover {
  background: #06182B;
  transform: translateY(-1px);
}
[data-theme="dark"] .btn-primary,
.dark .btn-primary,
[data-theme="dark"] .btn-navy-solid,
.dark .btn-navy-solid {
  background: #153965;
  color: #FFFFFF;
}
[data-theme="dark"] .btn-primary:hover,
.dark .btn-primary:hover,
[data-theme="dark"] .btn-navy-solid:hover,
.dark .btn-navy-solid:hover {
  background: #1D4B82;
}

/* Option: Navy ใสทะลุ (Navy Glass Variant) */
.btn-navy-glass {
  background: rgba(10, 37, 64, 0.75);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  color: #FFFFFF;
}
.btn-navy-glass:hover {
  background: rgba(10, 37, 64, 0.88);
  transform: translateY(-1px);
}

/* ===================================================
   SECONDARY: เทากระจกใสทะลุ (Pill ไร้ขอบ)
   =================================================== */
.btn-gray-glass {
  background: rgba(0, 0, 0, 0.06);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  color: #1A1A1A;
}
.btn-gray-glass:hover {
  background: rgba(0, 0, 0, 0.10);
  transform: translateY(-1px);
}

/* Dark Mode สำหรับ Gray Glass */
[data-theme="dark"] .btn-gray-glass,
.dark .btn-gray-glass {
  background: rgba(255, 255, 255, 0.12);
  color: #FFFFFF;
}
[data-theme="dark"] .btn-gray-glass:hover,
.dark .btn-gray-glass:hover {
  background: rgba(255, 255, 255, 0.18);
}

/* ===================================================
   DANGER & GHOST (Pill แคปซูลเท่ากัน)
   =================================================== */
.btn-danger {
  background: #DC2626;
  color: #FFFFFF;
}
.btn-danger:hover {
  background: #B91C1C;
  transform: translateY(-1px);
}
.btn-ghost {
  background: transparent;
  color: #0A2540;
}
.btn-ghost:hover {
  background: rgba(10, 37, 64, 0.06);
}
[data-theme="dark"] .btn-ghost {
  color: #9CA3AF;
}
[data-theme="dark"] .btn-ghost:hover {
  background: rgba(255, 255, 255, 0.08);
  color: #FFFFFF;
}
```

---

### 2. HTML Markup

```html
<!-- ทุกปุ่มมนแคปซูลเท่า Badges (border-radius: 9999px) ไร้ขอบ -->
<button type="button" class="btn-primary">
  บันทึกข้อมูล (Primary Navy Solid)
</button>

<button type="button" class="btn-gray-glass">
  ยกเลิก (Secondary Gray)
</button>

<button type="button" class="btn-danger">
  ลบรายการ (Danger)
</button>

<button type="button" class="btn-ghost">
  ดูตัวอย่าง (Ghost)
</button>
```

---

### 3. Tailwind CSS Classes

```html
<!-- Primary: Navy ใสทะลุ ทรงแคปซูลเท่า Badges -->
<button class="h-10 px-6 rounded-full border-none shadow-none bg-[#0A2540]/75 backdrop-blur-md text-white font-semibold hover:bg-[#0A2540]/88 active:scale-95 transition-all">
  บันทึกข้อมูล
</button>

<!-- Secondary: เทากระจกใสทะลุ ทรงแคปซูลเท่า Badges -->
<button class="h-10 px-6 rounded-full border-none shadow-none bg-black/[0.06] dark:bg-white/[0.12] backdrop-blur-md text-[#1A1A1A] dark:text-white font-semibold hover:bg-black/[0.10] dark:hover:bg-white/[0.18] active:scale-95 transition-all">
  ยกเลิก
</button>

<!-- Danger: ทรงแคปซูลเท่า Badges -->
<button class="h-10 px-6 rounded-full border-none shadow-none bg-red-600 hover:bg-red-700 text-white font-semibold active:scale-95 transition-all">
  ลบรายการ
</button>
```

---

## Sizes & Dimensions
| Size | สูง (Height) | Padding แนวนอน | ขนาดตัวอักษร | การใช้งาน |
|---|---|---|---|---|
| `sm` | 34px | `14px` | `13px` | ใน Table row, Filter bar, Mobile compact |
| `md` (default) | 42px | `20px` (Pill: `24px`) | `14px` | ฟอร์มทั่วไป, Modal actions, การ์ด |
| `lg` | 48px | `26px` (Pill: `30px`) | `15px` | Hero CTA, หน้า Landing, ยืนยันหลัก |

---

## Accessibility & Guidelines
1. **WCAG AAA Contrast**: ตัวหนังสือสีขาว (`#FFFFFF`) บน Primary Navy Solid (`#0A2540`) ให้ Contrast Ratio สูงถึง **14.8:1** (ผ่านเกณฑ์ระดับ AAA 7.0:1 อย่างสบาย ชัดเจนสูงสุด)
2. **Backdrop Filter Support**: ในกรณีที่เบราว์เซอร์ไม่รองรับ `backdrop-filter` สำหรับ Secondary Gray Glass, ระบบจะมี Fallback พื้นทึบอัตโนมัติ:
   ```css
   @supports not (backdrop-filter: blur(1px)) {
     .btn-gray-glass { background: #E5E7EB; }
     [data-theme="dark"] .btn-gray-glass { background: #2A2F3A; }
   }
   ```
3. **Focus States**: มี `focus-visible: outline 2px solid rgba(10, 37, 64, 0.6)` เสมอเพื่อการใช้งานผ่าน Keyboard

