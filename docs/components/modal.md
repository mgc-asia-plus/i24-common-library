# Component: Modal / Dialog

**สถานะ: v1.2 (Complete)** — หน้าต่างป๊อปอัปยืนยันการทำรายการหรือแบบฟอร์มย่อย  
*อ้าง SSOT ที่ [`../brand/design-tokens.md`](../brand/design-tokens.md) และ [`button.md`](button.md)*

---

## 1. Purpose (วัตถุประสงค์)
ใช้สำหรับดึงความสนใจของผู้ใช้เพื่อยืนยันการกระทำสำคัญ (เช่น ยืนยันการลบ, อนุมัติเอกสาร) หรือแสดงแบบฟอร์มขั้นตอนสั้น ๆ โดยไม่พาผู้ใช้ออกจากหน้าเดิม

> [!IMPORTANT]
> **การออกแบบตามธีม i24**:
> - **Backdrop**: มืดโปร่งแสง `rgba(0, 0, 0, 0.45)` พร้อม `backdrop-filter: blur(8px)`
> - **Modal Window**: พื้นผิวสีขาวใสทะลุ (White Translucent Glass) **ไร้ขอบ 100% (`border: none;`)** มนโค้งมนหรูหรา (`border-radius: 24px;`)
> - **Primary Button**: **Navy Solid (`#0A2540`)** ทรง Pill Capsule (`border-radius: 9999px`)
> - **Danger Button**: **Deep Crimson (`#B0141B`)** สำหรับการลบข้อมูลถาวร

---

## 2. Anatomy (ส่วนประกอบ)
1. **Backdrop (Overlay)**: ม่านพื้นหลังเบลอตัดการรบกวนจากหน้าจอหลัก
2. **Modal Card (Surface)**: กล่องลอยสีขาวใส ไร้ขอบ
3. **Header**: หัวข้อหน้าต่าง (Title) + ปุ่มปิดมุมขวา (Close icon)
4. **Body**: เนื้อหาข้อความชี้แจง หรืออินพุตฟอร์ม
5. **Footer Actions**: กลุ่มปุ่มควบคุม (ปุ่มหลักขวา, ปุ่มยกเลิกซ้าย)

---

## 3. Variants (รูปแบบ)

| Variant | การใช้งาน | ปุ่มแอ็กชันหลัก |
|---|---|---|
| **Confirm Dialog** | ยืนยันทั่วไป เช่น "ยืนยันการส่งข้อมูล" | `.btn-primary` (Navy Solid `#0A2540`) |
| **Danger / Destructive** | เตือนลบข้อมูลหรือการกระทำที่กู้คืนไม่ได้ | `.btn-danger` (Deep Crimson `#B0141B`) |
| **Form Modal** | มีช่องกรอกข้อมูลย่อย (1-3 ช่อง) | `.btn-primary` (Navy Solid `#0A2540`) |

---

## 4. Tokens & Dimensions

| ส่วน | ค่าที่ใช้ | Token |
|---|---|---|
| Window Surface | `rgba(255, 255, 255, 0.85)` / Dark: `rgba(26, 29, 36, 0.90)` | `color-surface` + Glass |
| Backdrop | `rgba(0, 0, 0, 0.45)` + blur 8px | Overlay Backdrop |
| Border | `none !important;` | ไร้เส้นขอบ |
| Shadow | `0 25px 50px -12px rgba(0, 0, 0, 0.18)` | Soft Floating Shadow |
| Radius | `24px` | `radius-2xl` |
| ความกว้าง (Confirm) | `420px - 480px` | Small Dialog |
| ความกว้าง (Form) | `560px - 640px` | Medium Dialog |

---

## 5. Accessibility (a11y)
1. **Role & Aria**: 
   - คอนเทนเนอร์กล่องต้องใส่ `role="dialog"` และ `aria-modal="true"`
   - มี `aria-labelledby="modal-title"` และ `aria-describedby="modal-desc"`
2. **Keyboard Handling**:
   - กดปุ่ม **`ESC`** ต้องปิด Modal ทันที
   - มี **Focus Trap**: เมื่อกด `Tab` โฟกัสต้องวนอยู่เฉพาะปุ่มภายใน Modal ไม่หลุดไปที่หน้าจอหลัก
3. **Scroll Lock**: เมื่อ Modal เปิด ต้องใส่ `overflow: hidden;` ให้กับ `<body>` เพื่อป้องกันการเลื่อนหน้าจอด้านหลัง

---

## 6. Ready-to-use Templates

### A. Pure CSS & HTML

```html
<!-- Backdrop Overlay -->
<div id="modal-overlay" class="i24-modal-overlay" aria-hidden="true">
  <!-- Modal Window (White Glass ไร้ขอบ) -->
  <div class="i24-modal-window" role="dialog" aria-modal="true" aria-labelledby="modal-title">
    <div class="i24-modal-header">
      <h3 id="modal-title" class="i24-modal-title">ยืนยันการบันทึกข้อมูล</h3>
      <button type="button" class="i24-modal-close" onclick="closeModal()" aria-label="ปิด">✕</button>
    </div>
    
    <div class="i24-modal-body">
      <p id="modal-desc">คุณต้องการบันทึกการจองรถคันนี้เข้าสู่ระบบ i24 ใช่หรือไม่?</p>
    </div>

    <div class="i24-modal-footer">
      <button type="button" class="btn btn-gray-glass" onclick="closeModal()">ยกเลิก</button>
      <button type="button" class="btn btn-primary" onclick="confirmAction()">ยืนยัน (Navy Solid)</button>
    </div>
  </div>
</div>
```

```css
/* Backdrop Overlay */
.i24-modal-overlay {
  position: fixed;
  inset: 0;
  z-index: 1000;
  background: rgba(0, 0, 0, 0.45);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.2s ease, visibility 0.2s ease;
}

.i24-modal-overlay.open {
  opacity: 1;
  visibility: visible;
}

/* Modal Window (White Glass ไร้ขอบ) */
.i24-modal-window {
  background: rgba(255, 255, 255, 0.88);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);
  border: none !important;
  border-radius: 24px;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.20);
  width: 100%;
  max-width: 460px;
  padding: 24px;
  transform: scale(0.95);
  transition: transform 0.2s ease;
}

[data-theme="dark"] .i24-modal-window {
  background: rgba(26, 29, 36, 0.92);
  color: #FFFFFF;
}

.i24-modal-overlay.open .i24-modal-window {
  transform: scale(1);
}

.i24-modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 12px;
}

.i24-modal-title {
  font-size: 18px;
  font-weight: 700;
  color: #0A2540;
  margin: 0;
}
[data-theme="dark"] .i24-modal-title {
  color: #FFFFFF;
}

.i24-modal-close {
  background: transparent;
  border: none;
  font-size: 16px;
  cursor: pointer;
  color: #6B7280;
  padding: 4px 8px;
  border-radius: 9999px;
  transition: background 0.15s;
}
.i24-modal-close:hover {
  background: rgba(0, 0, 0, 0.05);
  color: #1A1A1A;
}

.i24-modal-body {
  font-size: 14px;
  color: #4B5563;
  line-height: 1.6;
  margin-bottom: 24px;
}
[data-theme="dark"] .i24-modal-body {
  color: #9CA3AF;
}

.i24-modal-footer {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: 10px;
}
```

### B. Vanilla JavaScript Controller

```javascript
function openModal() {
  const overlay = document.getElementById('modal-overlay');
  overlay.classList.add('open');
  overlay.setAttribute('aria-hidden', 'false');
  document.body.style.overflow = 'hidden'; // Scroll lock

  // Close on Backdrop Click
  overlay.onclick = (e) => {
    if (e.target === overlay) closeModal();
  };

  // Close on Escape key
  document.addEventListener('keydown', handleEsc);
}

function closeModal() {
  const overlay = document.getElementById('modal-overlay');
  overlay.classList.remove('open');
  overlay.setAttribute('aria-hidden', 'true');
  document.body.style.overflow = '';
  document.removeEventListener('keydown', handleEsc);
}

function handleEsc(e) {
  if (e.key === 'Escape') closeModal();
}
```
