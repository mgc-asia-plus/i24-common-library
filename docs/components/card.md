# Card

## Purpose
กล่องจัดกลุ่มเนื้อหาที่เกี่ยวข้อง (สรุป, รายการ, ฟอร์มย่อย)

## Anatomy
```
┌─────────────────────────┐
│ Header (title + action?) │
├─────────────────────────┤
│ Body (เนื้อหา)           │
├─────────────────────────┤
│ Footer (action?)         │  ← optional
└─────────────────────────┘
```

## Variants
| Variant | ลักษณะ | ใช้เมื่อ |
|---------|--------|----------|
| `white-glass` (แนะนำ) | พื้นขาวใส `rgba(255,255,255,0.45)` + blur 24px + ขอบสะท้อนแสงบางเบา | พื้นผิวมาตรฐาน ลุคหรูหรา มองทะลุเห็นพื้นหลัง |
| `elevated` | พื้นทึบ `color-bg` + `shadow-sm` | card ลอยบนพื้นทั่วไป |
| `outlined` | border `color-border`, ไม่มีเงา | บนพื้นที่มีเงาไม่เหมาะ |
| `filled` | พื้น `color-surface` | เน้นแยกจากพื้นหลัง |

## States
- static เป็นหลัก
- **interactive card** (ทั้งใบคลิกได้): เพิ่ม hover ยกเงา (`shadow-md`) + focus ring + `cursor-pointer`; ต้องเป็น `<a>`/`<button>` ครอบหรือมี role ที่ถูกต้อง

## Tokens used
`card-white-glass-bg`, `color-border`, `color-text`, `radius-lg`, `space-4/6`

---

## Ready-to-use Templates (การ์ดสีขาวใส)

### 1. Pure CSS
```css
/* Card สีขาวใส ไร้ขอบ บนพื้นหลังสีขาว #FFFFFF (White Translucent Glass — Borderless) */
.card-white-glass {
  background: rgba(255, 255, 255, 0.70);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);
  border: none;                                 /* ❌ ไร้ขอบ 100% */
  box-shadow: 0 10px 30px -5px rgba(0, 0, 0, 0.04); /* เงาฟุ้งลอยบางเฉียบ นุ่มตา ไม่ใช่เส้นขอบ */
  border-radius: 20px;
  padding: 24px;
}

/* Dark Mode (Smoke Clear Glass) */
[data-theme="dark"] .card-white-glass {
  background: rgba(255, 255, 255, 0.07);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  border: none;
  box-shadow: none;
}
```

### 2. HTML Markup
```html
<div class="card-white-glass">
  <header class="flex items-center justify-between mb-4">
    <h3 class="text-base font-bold text-[#1A1A1A] dark:text-white">หัวข้อการ์ด</h3>
  </header>
  <div class="text-sm text-[#4B5563] dark:text-[#9CA3AF]">
    เนื้อหาภายในการ์ดสีขาวใส ไร้ขอบ มองเห็นแสงสีจากพื้นหลังทะลุผ่านเนียนตา
  </div>
</div>
```

### 3. Tailwind CSS
```html
<!-- Card ขาวใส ไร้ขอบ 100% -->
<div class="p-6 rounded-[20px] border-none shadow-none bg-white/50 dark:bg-white/[0.07] backdrop-blur-2xl">
  <!-- Content -->
</div>
```
