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
| `elevated` (default) | พื้น `color-bg` + `shadow-sm` | card ลอยบนพื้น |
| `outlined` | border `color-border`, ไม่มีเงา | บนพื้นที่มีเงาไม่เหมาะ |
| `filled` | พื้น `color-surface` | เน้นแยกจากพื้นหลัง |

## States
- static เป็นหลัก
- **interactive card** (ทั้งใบคลิกได้): เพิ่ม hover ยกเงา (`shadow-md`) + focus ring + `cursor-pointer`; ต้องเป็น `<a>`/`<button>` ครอบหรือมี role ที่ถูกต้อง

## Tokens used
`color-bg`, `color-surface`, `color-border`, `color-text`, `shadow-sm`, `shadow-md`, `radius-lg`, `space-4/6`

## Accessibility
- อย่าซ้อน control คลิกได้หลายตัวใน interactive card (กันสับสน keyboard/aria)
- header ใช้ heading ที่ถูกลำดับ (`<h2>`/`<h3>`)

## Reference snippet
```html
<section class="bg-[--color-bg] rounded-lg shadow-sm p-6">
  <header class="flex items-center justify-between mb-4">
    <h3 class="text-lg font-semibold text-[--color-text]">สรุปยอด</h3>
  </header>
  <div class="text-[--color-text]"> ... </div>
</section>
```
