# Component: Toast Notification

**สถานะ: v1.2 (Complete)** — ระบบแจ้งเตือนสถานะลอยมุมจอ (Feedback Notification)  
*อ้าง SSOT ที่ [`../brand/design-tokens.md`](../brand/design-tokens.md) และ [`alert.md`](alert.md)*

---

## 1. Purpose (วัตถุประสงค์)
ใช้แสดงการแจ้งเตือนสั้น ๆ หลังผู้ใช้ทำรายการสำเร็จหรือล้มเหลว (เช่น "บันทึกข้อมูลเรียบร้อย", "ไม่สามารถเชื่อมต่อเซิร์ฟเวอร์ได้") โดยลอยอยู่ที่มุมจอและหายไปเองอัตโนมัติ (Auto-dismiss) ไม่ขัดจังหวะการทำงาน

> [!IMPORTANT]
> **การออกแบบตามธีม i24**:
> - **Floating Surface**: การ์ดกระจกขาวใส (White Translucent Glass `rgba(255, 255, 255, 0.88)` + blur 24px) **ไร้เส้นขอบ (`border: none;`)**
> - **Shape**: ทรงแคปซูลมนหรูหรา (`border-radius: 9999px;` หรือ `18px;`)
> - **Colors**:
>   - **Success**: จุดไฟสถานะสีเขียวสด (`#10B981`)
>   - **Error / Danger**: จุดไฟหรือไอคอนสี **Deep Crimson (`#B0141B`)**
>   - **Info**: จุดสี **Navy Solid (`#0A2540`)**
>   - **Warning**: จุดสี Amber (`#F59E0B`)

---

## 2. Anatomy (ส่วนประกอบ)
1. **Toast Container**: พื้นที่กำหนดตำแหน่งคงที่ (Fixed Position) มุมขวาล่าง (`bottom-right`)
2. **Toast Item (Card)**: การ์ดลอยแก้วใส
3. **Status Indicator / Dot**: จุดไฟสีแสดงผลลัพธ์
4. **Message Text**: ข้อความกระชับ เข้าใจง่าย
5. **Close Button**: ปุ่มปิดแบบกากบาท (ถ้าต้องการปิดก่อนเวลา)

---

## 3. Tokens & Dimensions

| ส่วน | ค่าที่ใช้ | Token |
|---|---|---|
| Container Position | `bottom: 24px; right: 24px;` | Viewport Edge |
| Z-Index | `9999` | Top-level Overlay |
| Toast Surface | `rgba(255, 255, 255, 0.88)` / Dark: `rgba(26, 29, 36, 0.92)` | Floating Glass |
| Border | `none !important;` | ไร้ขอบ |
| Shadow | `0 12px 32px -4px rgba(0, 0, 0, 0.12)` | Floating Toast Shadow |
| Radius | `9999px` (Pill) หรือ `18px` | `radius-pill` |
| ความกว้าง | `320px - 400px` | Toast Width |
| Duration | `4000ms` (4 วินาที) | Auto-dismiss Time |

---

## 4. Accessibility (a11y)
1. **ARIA Live Region**:
   - Container ต้องมี `aria-live="polite"` และ `aria-atomic="true"` สำหรับแจ้งเตือนทั่วไป
   - กรณี Error สำคัญ ใช้ `role="alert"` หรือ `aria-live="assertive"`
2. **Dismissible**: มีปุ่มปิดชัดเจนสำหรับผู้ใช้ที่ต้องการปิดเองก่อนเวลา

---

## 5. Ready-to-use Template (Pure CSS & JS Manager)

```html
<!-- Toast Fixed Container (วางไว้ใน root layout) -->
<div id="i24-toast-container" class="i24-toast-container" aria-live="polite"></div>
```

```css
/* Container มุมขวาล่าง */
.i24-toast-container {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 9999;
  display: flex;
  flex-direction: column;
  gap: 10px;
  pointer-events: none;
}

/* Toast Card (White Glass ไร้ขอบ) */
.i24-toast-item {
  pointer-events: auto;
  min-width: 300px;
  max-width: 420px;
  padding: 12px 18px;
  border-radius: 9999px; /* ทรงแคปซูล */
  background: rgba(255, 255, 255, 0.90);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);
  border: none !important;
  box-shadow: 0 12px 32px -6px rgba(0, 0, 0, 0.12);
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  transform: translateY(20px) scale(0.95);
  opacity: 0;
  transition: transform 0.25s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.25s ease;
}

[data-theme="dark"] .i24-toast-item {
  background: rgba(26, 29, 36, 0.92);
  color: #FFFFFF;
}

.i24-toast-item.show {
  transform: translateY(0) scale(1);
  opacity: 1;
}

.i24-toast-item.hide {
  transform: translateY(-10px) scale(0.95);
  opacity: 0;
}

.i24-toast-content {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 13px;
  font-weight: 500;
  color: #1A1A1A;
}
[data-theme="dark"] .i24-toast-content {
  color: #FFFFFF;
}

/* Status Dots */
.i24-toast-dot {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  flex-shrink: 0;
}
.i24-toast-dot.success { background: #10B981; box-shadow: 0 0 8px rgba(16, 185, 129, 0.5); }
.i24-toast-dot.error   { background: #B0141B; box-shadow: 0 0 8px rgba(176, 20, 27, 0.5); }
.i24-toast-dot.info    { background: #0A2540; box-shadow: 0 0 8px rgba(10, 37, 64, 0.4); }

.i24-toast-close {
  background: transparent;
  border: none;
  font-size: 14px;
  color: #9CA3AF;
  cursor: pointer;
  padding: 2px 6px;
  border-radius: 9999px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: color 0.15s;
}
.i24-toast-close:hover {
  color: #1A1A1A;
}
```

```javascript
// Lightweight Toast Manager Singleton
const i24Toast = {
  show(message, type = 'info', duration = 4000) {
    const container = document.getElementById('i24-toast-container');
    if (!container) return;

    const toast = document.createElement('div');
    toast.className = 'i24-toast-item';
    toast.innerHTML = `
      <div class="i24-toast-content">
        <span class="i24-toast-dot ${type}"></span>
        <span>${message}</span>
      </div>
      <button type="button" class="i24-toast-close" aria-label="ปิด">✕</button>
    `;

    container.appendChild(toast);

    // Trigger enter animation
    requestAnimationFrame(() => {
      toast.classList.add('show');
    });

    const dismiss = () => {
      toast.classList.remove('show');
      toast.classList.add('hide');
      setTimeout(() => toast.remove(), 250);
    };

    toast.querySelector('.i24-toast-close').onclick = dismiss;
    if (duration > 0) setTimeout(dismiss, duration);
  },

  success(msg, dur) { this.show(msg, 'success', dur); },
  error(msg, dur)   { this.show(msg, 'error', dur); },
  info(msg, dur)    { this.show(msg, 'info', dur); }
};
```
