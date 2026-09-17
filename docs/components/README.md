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
- **Modern look (gradient + glass)**: surface (card/nav/footer/ปุ่มรอง) ใช้ **glass** ได้; ปุ่ม primary/badge เน้น/โลโก้ใช้ **gradient** ได้ — แต่ **ห้าม gradient ที่พื้นหลังหน้า/ตัวหนังสือ**. ค่า token + a11y (contrast, `prefers-reduced-transparency`, fallback) ดู [`../brand/effects.md`](../brand/effects.md)

## รายการคอมโพเนนต์ (v1.2 — Complete)
| Component | ไฟล์ | ประเภท | สรุป |
|---|---|---|---|
| Button | [button.md](button.md) | Basic | ปุ่ม action หลัก (Navy Solid) / ปุ่มรอง (Gray Glass) |
| Badge | [badge.md](badge.md) | Basic | ป้ายสถานะ ทรง Pill — ตารางใช้ success/warning/danger จาก etax |
| Card | [card.md](card.md) | Layout | กล่องเนื้อหา White Clear Glass ไร้ขอบ |
| Input | [input.md](input.md) | Form | ช่องกรอกข้อความ + validation |
| Table | [table.md](table.md) | Data | ตาราง — หัว Cool Slate + สถานะ success/warning/danger |
| Nav / Header | [nav-header.md](nav-header.md) | Navigation | แถบนำทางบนสุดทรงแคปซูล |
| Alert | [alert.md](alert.md) | Feedback | แจ้งเตือนแบบ inline |
| Theme mode | [theme-mode.md](theme-mode.md) | Utility | สลับ light/dark |
| Footer | [footer.md](footer.md) | Layout | 🔒 "Powered by i24" — **บังคับทุกระบบที่มี UI** |
| Modal / Dialog | [modal.md](modal.md) | Complex | หน้าต่างป๊อปอัปยืนยัน + Backdrop blur |
| Select / Dropdown | [select.md](select.md) | Complex | เมนูเลือกข้อมูลคัสตอม ผิวกระจกใส |
| Toast Notification | [toast.md](toast.md) | Complex | การ์ดแจ้งเตือนลอยมุมจอ Auto-dismiss |
| Pagination | [pagination.md](pagination.md) | Complex | แถบเปลี่ยนหน้าตาราง ผูกกับ JSON API |

## มาตรฐานบังคับ (required ทุกระบบที่มี UI)
- **Footer "Powered by i24"** ([footer.md](footer.md)) — ต้องแสดงทุกหน้า วางใน layout กลาง
