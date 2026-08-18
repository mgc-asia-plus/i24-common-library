# Components

spec ของ UI component กลาง — อธิบายพฤติกรรม/โครงสร้าง/token ที่ใช้ ให้ทุก stack implement ให้ตรงกัน

## เทมเพลตของทุก spec
แต่ละไฟล์ component เขียนตามหัวข้อนี้:
1. **Purpose** — ใช้ทำอะไร ใช้เมื่อไหร่
2. **Anatomy** — ส่วนประกอบ
3. **Variants** — รูปแบบ (เช่น primary/secondary)
4. **Sizes** — ขนาด (ถ้ามี)
5. **States** — default / hover / focus / active / disabled / loading
6. **Tokens used** — semantic token ที่อ้าง (จาก [`../brand/design-tokens.md`](../brand/design-tokens.md))
7. **Accessibility** — role, keyboard, aria ขั้นต่ำ
8. **Reference snippet** — ตัวอย่างสั้น (HTMX/HTML + React) พออธิบาย ไม่ใช่ template ครบ

## หลักการร่วม
- **สีจาก semantic token เท่านั้น** — ห้าม hardcode hex
- **Focus ที่มองเห็นได้**: ทุก element โต้ตอบได้ต้องมี focus ring (`color-focus-ring`)
- **ขนาดแตะขั้นต่ำ** 40x40px สำหรับ control บนมือถือ
- **Contrast** ต้องผ่าน WCAG AA (ตรวจจริงด้วยเครื่องมือ — a11y เต็มต้องทดสอบเพิ่ม)
- **Radius**: control ทั่วไป `radius-md`; ปุ่ม/แท็บสไตล์แบรนด์ใช้ `radius-pill` ได้
- **State ครบ**: อย่าลืม disabled และ focus-visible

## รายการ (v1)
| Component | ไฟล์ | สรุป |
|-----------|------|------|
| Button | [button.md](button.md) | ปุ่ม action หลัก/รอง |
| Badge | [badge.md](badge.md) | ป้ายสถานะ/ตัวเลข |
| Card | [card.md](card.md) | กล่องเนื้อหา |
| Input | [input.md](input.md) | ช่องกรอกข้อความ + validation |
| Table | [table.md](table.md) | ตารางข้อมูล |
| Nav / Header | [nav-header.md](nav-header.md) | แถบนำทางบนสุด |
| Alert | [alert.md](alert.md) | แจ้งเตือนแบบ inline |
| Theme mode | [theme-mode.md](theme-mode.md) | สลับ light/dark |
| Footer | [footer.md](footer.md) | 🔒 "Powered by i24" — **บังคับทุกระบบที่มี UI** |

## มาตรฐานบังคับ (required ทุกระบบที่มี UI)
- **Footer "Powered by i24"** ([footer.md](footer.md)) — ต้องแสดงทุกหน้า วางใน layout กลาง
