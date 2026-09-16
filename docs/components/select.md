# Component: Select / Dropdown

**สถานะ: v1.2 (Complete)** — กล่องเลือกข้อมูลแบบคัสตอม ผิวกระจกใส ไม่พึ่งพา native select  
*อ้าง SSOT ที่ [`../brand/design-tokens.md`](../brand/design-tokens.md)*

---

## 1. Purpose (วัตถุประสงค์)
ใช้แทนแท็ก `<select>` แบบเดิมของเบราว์เซอร์ เพื่อให้หน้าตาการเลือกข้อมูลสอดคล้องกับธีม **Corporate Glassmorphism** (มีพื้นผิวแก้วใส, มนโค้งสวยงาม, แสดงไฮไลต์สี Navy ได้คมชัด และสามารถขยายเป็น Searchable Combobox ได้)

> [!TIP]
> **การออกแบบตามธีม i24**:
> - **Select Trigger**: ทรงแคปซูลหรือโค้งมน `radius-lg (14px)` ผิวกระจกใส `rgba(0, 0, 0, 0.04)` ไร้เส้นขอบหนา
> - **Dropdown Popover (Menu)**: เมนูลอยผิวขาวใส (White Translucent Glass) ลอยเหนือเลเยอร์อื่นด้วยเงาฟุ้งนุ่มตา `backdrop-filter: blur(20px)`
> - **Active / Hover Option**: ไฮไลต์ด้วยสีกรมท่า Navy Solid (`#0A2540`) หรือสีกระจกบางเบา

---

## 2. Anatomy (ส่วนประกอบ)
1. **Trigger Button**: แถบปุ่มแสดงค่าที่เลือกอยู่ปัจจุบัน + ไอคอนลูกศร (Chevron)
2. **Selected Value**: ข้อความแสดงตัวเลือกที่เลือก (หรือ Placeholder หากยังไม่ได้เลือก)
3. **Dropdown Menu (Popover)**: หน้าต่างแสดงรายการตัวเลือก
4. **Option Item**: แถวตัวเลือกแต่ละรายการ พร้อมสถานะ Hover / Selected

---

## 3. Tokens & Dimensions

| ส่วน | ค่าที่ใช้ | Token |
|---|---|---|
| Trigger Height | `42px` (Medium) / `36px` (Small) | Button Height |
| Trigger Surface | `rgba(0, 0, 0, 0.04)` / Dark: `rgba(255, 255, 255, 0.08)` | `color-surface` |
| Menu Surface | `rgba(255, 255, 255, 0.92)` / Dark: `rgba(26, 29, 36, 0.95)` | White Glass Surface |
| Border | `none !important;` | ไร้ขอบ |
| Menu Shadow | `0 16px 36px -8px rgba(0, 0, 0, 0.15)` | Popover Shadow |
| Menu Radius | `16px` | `radius-xl` |
| Selected Option BG | `rgba(10, 37, 64, 0.08)` (Light) / `rgba(255, 255, 255, 0.12)` (Dark) | Active Tint |

---

## 4. Accessibility (a11y)
1. **ARIA Roles**:
   - ปุ่ม Trigger: `role="combobox"`, `aria-haspopup="listbox"`, `aria-expanded="false/true"`
   - เมนูดรอปดาวน์: `role="listbox"`
   - ตัวเลือก: `role="option"`, `aria-selected="true/false"`
2. **Keyboard Navigation**:
   - กด `Space` หรือ `Enter` บน Trigger เพื่อเปิด/ปิดเมนู
   - กด `ArrowDown` / `ArrowUp` เพื่อเลื่อนไฮไลต์ตัวเลือก
   - กด `Enter` เพื่อเลือกค่าและปิดเมนู
   - กด `ESC` เพื่อปิดเมนูโดยไม่เปลี่ยนค่า

---

## 5. Ready-to-use Template (Pure CSS & Vanilla JS)

```html
<div class="i24-select-container" id="car-type-select">
  <!-- Trigger -->
  <button type="button" class="i24-select-trigger" aria-haspopup="listbox" aria-expanded="false" id="select-trigger">
    <span class="i24-select-label" id="select-label">เลือกประเภทรถ...</span>
    <svg class="i24-select-chevron" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
      <polyline points="6 9 12 15 18 9"></polyline>
    </svg>
  </button>

  <!-- Dropdown Menu -->
  <div class="i24-select-menu" role="listbox" aria-labelledby="select-trigger" tabindex="-1">
    <div class="i24-select-option" role="option" data-value="sedan">รถเก๋งซีดาน (Sedan)</div>
    <div class="i24-select-option" role="option" data-value="suv">รถอเนกประสงค์ (SUV)</div>
    <div class="i24-select-option" role="option" data-value="van">รถตู้โดยสาร (Van)</div>
    <div class="i24-select-option" role="option" data-value="ev">รถยนต์ไฟฟ้า (EV)</div>
  </div>
</div>
```

```css
.i24-select-container {
  position: relative;
  display: inline-block;
  width: 100%;
  max-width: 280px;
}

/* Trigger Button */
.i24-select-trigger {
  width: 100%;
  height: 42px;
  padding: 0 16px;
  border-radius: 9999px; /* Pill Capsule */
  background: rgba(0, 0, 0, 0.04);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: none !important;
  color: #1A1A1A;
  font-size: 14px;
  font-weight: 500;
  display: flex;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
  transition: background 0.15s ease, box-shadow 0.15s ease;
}

.i24-select-trigger:hover {
  background: rgba(0, 0, 0, 0.07);
}

[data-theme="dark"] .i24-select-trigger {
  background: rgba(255, 255, 255, 0.08);
  color: #FFFFFF;
}
[data-theme="dark"] .i24-select-trigger:hover {
  background: rgba(255, 255, 255, 0.12);
}

.i24-select-chevron {
  transition: transform 0.2s ease;
  color: #6B7280;
}
.i24-select-container.open .i24-select-chevron {
  transform: rotate(180deg);
}

/* Dropdown Menu (White Glass ไร้ขอบ) */
.i24-select-menu {
  position: absolute;
  top: calc(100% + 8px);
  left: 0;
  right: 0;
  z-index: 500;
  background: rgba(255, 255, 255, 0.92);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);
  border: none !important;
  border-radius: 18px;
  box-shadow: 0 16px 36px -6px rgba(0, 0, 0, 0.12);
  padding: 6px;
  opacity: 0;
  visibility: hidden;
  transform: translateY(-8px);
  transition: opacity 0.15s ease, transform 0.15s ease, visibility 0.15s;
}

[data-theme="dark"] .i24-select-menu {
  background: rgba(26, 29, 36, 0.95);
  box-shadow: 0 16px 36px -6px rgba(0, 0, 0, 0.40);
}

.i24-select-container.open .i24-select-menu {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

/* Option Items */
.i24-select-option {
  padding: 10px 14px;
  border-radius: 12px;
  font-size: 13px;
  font-weight: 500;
  color: #1A1A1A;
  cursor: pointer;
  transition: background 0.12s ease, color 0.12s ease;
}

[data-theme="dark"] .i24-select-option {
  color: #E5E7EB;
}

.i24-select-option:hover {
  background: rgba(10, 37, 64, 0.06);
  color: #0A2540;
}

[data-theme="dark"] .i24-select-option:hover {
  background: rgba(255, 255, 255, 0.10);
  color: #FFFFFF;
}

.i24-select-option.selected {
  background: #0A2540;
  color: #FFFFFF !important;
  font-weight: 600;
}
```

```javascript
// Vanilla JS Controller
const container = document.getElementById('car-type-select');
const trigger = document.getElementById('select-trigger');
const label = document.getElementById('select-label');
const options = container.querySelectorAll('.i24-select-option');

trigger.addEventListener('click', () => {
  const isOpen = container.classList.toggle('open');
  trigger.setAttribute('aria-expanded', isOpen);
});

options.forEach(opt => {
  opt.addEventListener('click', () => {
    options.forEach(o => o.classList.remove('selected'));
    opt.classList.add('selected');
    label.textContent = opt.textContent;
    container.classList.remove('open');
    trigger.setAttribute('aria-expanded', 'false');
  });
});

// Click outside to dismiss
document.addEventListener('click', (e) => {
  if (!container.contains(e.target)) {
    container.classList.remove('open');
    trigger.setAttribute('aria-expanded', 'false');
  }
});
```
