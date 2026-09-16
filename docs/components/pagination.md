# Component: Pagination

**สถานะ: v1.2 (Complete)** — แถบควบคุมการแบ่งหน้าข้อมูล  
*อ้าง SSOT ที่ [`../brand/design-tokens.md`](../brand/design-tokens.md) และ [`../conventions/json-api.md`](../conventions/json-api.md)*

---

## 1. Purpose (วัตถุประสงค์)
ใช้ควบคุมการเปลี่ยนหน้าข้อมูลในตาราง (Table) หรือรายการการ์ด (Grid) ที่มีข้อมูลจำนวนมาก เพื่อให้ผู้ใช้สามารถข้ามไปยังหน้าที่ต้องการได้ง่าย สอดคล้องกับมาตรฐาน Pagination API ของ i24

> [!IMPORTANT]
> **การออกแบบตามธีม i24**:
> - **Active Page**: **Navy Solid (`#0A2540`)** ตัวหนังสือสีขาว ทรงกลม/แคปซูล (`border-radius: 9999px`) ไร้ขอบ
> - **Inactive Page & Navigation Buttons**: ปุ่มเทากระจกใส (Frosted Gray Glass `rgba(0, 0, 0, 0.05)`)
> - **Disabled State**: ปิดการคลิกเมื่ออยู่ที่หน้าแรก (`< Prev`) หรือหน้าสุดท้าย (`Next >`)

---

## 2. Anatomy (ส่วนประกอบ)
1. **Result Summary**: ข้อความสรุป เช่น "แสดง 1 - 20 จาก 137 รายการ"
2. **Previous Button (`<`)**: ปุ่มย้อนกลับไปหน้าที่แล้ว
3. **Page Numbers**: ตัวเลขลำดับหน้า (พร้อมเครื่องหมายจุดละสายตา `...` หากมีหลายหน้า)
4. **Next Button (`>`)**: ปุ่มไปยังหน้าถัดไป

---

## 3. สอดคล้องกับ API Convention

ตรงกับ Response Envelope ใน [`../conventions/json-api.md`](../conventions/json-api.md):

```json
{
  "data": [ ... ],
  "error": null,
  "meta": {
    "page": 1,
    "page_size": 20,
    "total": 137
  }
}
```

---

## 4. Tokens & Dimensions

| ส่วน | ค่าที่ใช้ | Token |
|---|---|---|
| Page Button Size | `36px × 36px` | Small Pill Button |
| Active Page BG | `#0A2540` / Dark: `#153965` | `color-primary` (Navy Solid) |
| Active Page Text | `#FFFFFF` | Text White |
| Inactive Page BG | `rgba(0, 0, 0, 0.05)` / Dark: `rgba(255, 255, 255, 0.08)` | Gray Glass |
| Border | `none !important;` | ไร้ขอบ |
| Radius | `9999px` (Circle/Pill) | `radius-pill` |

---

## 5. Accessibility (a11y)
1. **Semantic HTML**: ครอบด้วยแท็ก `<nav aria-label="Pagination Navigation">`
2. **Current Page**: หน้าปัจจุบันต้องใส่ `aria-current="page"`
3. **Disabled State**: ปุ่มย้อนกลับ/ถัดไปที่กดไม่ได้ให้ใส่ `disabled` และ `aria-disabled="true"`

---

## 6. Ready-to-use Template (Pure CSS & HTML)

```html
<nav class="i24-pagination" aria-label="Pagination">
  <div class="i24-pagination-summary">
    แสดง <strong>1 - 20</strong> จาก <strong>137</strong> รายการ
  </div>

  <div class="i24-pagination-controls">
    <!-- Prev -->
    <button type="button" class="i24-page-btn" disabled aria-disabled="true">
      ‹ ย้อนกลับ
    </button>

    <!-- Pages -->
    <button type="button" class="i24-page-btn active" aria-current="page">1</button>
    <button type="button" class="i24-page-btn">2</button>
    <button type="button" class="i24-page-btn">3</button>
    <span class="i24-page-ellipsis">…</span>
    <button type="button" class="i24-page-btn">7</button>

    <!-- Next -->
    <button type="button" class="i24-page-btn">
      ถัดไป ›
    </button>
  </div>
</nav>
```

```css
.i24-pagination {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
  padding: 16px 4px;
  font-size: 13px;
}

.i24-pagination-summary {
  color: #6B7280;
}
[data-theme="dark"] .i24-pagination-summary {
  color: #9CA3AF;
}

.i24-pagination-controls {
  display: flex;
  align-items: center;
  gap: 6px;
}

/* Page Button (Pill Capsule ไร้ขอบ) */
.i24-page-btn {
  height: 36px;
  min-width: 36px;
  padding: 0 12px;
  border-radius: 9999px;
  background: rgba(0, 0, 0, 0.05);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: none !important;
  color: #1A1A1A;
  font-size: 13px;
  font-weight: 600;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.15s ease, transform 0.15s ease;
}

.i24-page-btn:hover:not(:disabled):not(.active) {
  background: rgba(0, 0, 0, 0.09);
  transform: translateY(-1px);
}

[data-theme="dark"] .i24-page-btn {
  background: rgba(255, 255, 255, 0.08);
  color: #FFFFFF;
}
[data-theme="dark"] .i24-page-btn:hover:not(:disabled):not(.active) {
  background: rgba(255, 255, 255, 0.14);
}

/* Active Page: Navy Solid #0A2540 */
.i24-page-btn.active {
  background: #0A2540;
  color: #FFFFFF !important;
  cursor: default;
}
[data-theme="dark"] .i24-page-btn.active {
  background: #153965;
}

.i24-page-btn:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

.i24-page-ellipsis {
  color: #9CA3AF;
  padding: 0 4px;
}
```
