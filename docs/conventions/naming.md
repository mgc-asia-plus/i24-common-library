# Convention: Naming

## ทั่วไป
- ชื่อสื่อความหมาย หลีกเลี่ยงตัวย่อกำกวม
- ภาษาอังกฤษสำหรับ identifier; ข้อความ UI เป็นไทยได้

## ต่อภาษา
| สิ่ง | Go | TypeScript |
|------|-----|-----------|
| ตัวแปร/ฟังก์ชัน | `camelCase` (exported = `PascalCase`) | `camelCase` |
| type/class | `PascalCase` | `PascalCase` |
| ค่าคงที่ | `PascalCase`/`camelCase` (ใกล้ที่ใช้) | `UPPER_SNAKE` หรือ `camelCase` |
| ไฟล์ | `snake_case.go` / ตามแพ็กเกจ | `kebab-case.ts` หรือ `PascalCase.tsx` (component) |
| แพ็กเกจ/โฟลเดอร์ | สั้น ตัวเล็ก | `kebab-case` |

## JSON / API
- **field เป็น `snake_case`** เสมอ (ดู [`json-api.md`](json-api.md))

## Design tokens
- token: `kebab-case` มีลำดับชั้น เช่น `brand-red-500`, `color-text-muted`
- semantic นำหน้าด้วยหมวด: `color-*`, `radius-*`, `space-*`, `shadow-*`, `text-*`, `font-*`

## Handler/usecase (จาก stack Go)
- `*PageHandler` = คืน HTML, `*Handler` = คืน JSON
- usecase เรียก business ("ไม่ใช่ service" ในบริบท Go monolith — ใช้คำว่า usecase)

## Component (UI)
- ชื่อ component = `PascalCase` (`NavHeader`, `ThemeToggle`)
- variant/size เป็น string literal ตาม spec (`"primary"`, `"sm"`)
