# Convention: Naming

กฎชื่อ (NamingRule) ที่ใช้ร่วมทุก stack — ครอบคลุม **ไฟล์**, **type**, และ **JSON field**

ชุด ConventionSet: [`project-structure.md`](project-structure.md) · [`naming.md`](naming.md) · [`git.md`](git.md) · [`json-api.md`](json-api.md)

## NamingRule (pattern)
| สิ่ง | pattern |
|------|---------|
| ไฟล์ | Go: `snake_case.go` (ตามแพ็กเกจ); TS: `kebab-case.ts`; React component: `PascalCase.tsx` |
| type / class | `PascalCase` (ทุกภาษาในชุด) |
| JSON field | `snake_case` เสมอ — ดู envelope ที่ [`json-api.md`](json-api.md) |

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

Nest.js ใช้ `*.spec.ts`; Express.js ใช้ `*.test.ts` — ไม่สลับ convention ทดสอบข้าม stack

## JSON / API
- **field เป็น `snake_case`** เสมอ (`created_at`, `tax_id`, `total_amount`) — รายละเอียด envelope ดู [`json-api.md`](json-api.md)
- ฝั่ง TS ที่ต้องการ camelCase ให้ map ที่ boundary ไม่ใช่กลาง ๆ

## Design tokens
- อ้าง **ชื่อ token** เท่านั้น — ค่าสีอยู่ที่ [`../brand/`](../brand/design-tokens.md) ห้ามใส่ hex ในโค้ดหรือในไฟล์ convention
- token: `kebab-case` มีลำดับชั้น เช่น `primary-solid`, `navy-500`, `color-text-muted`
- semantic นำหน้าด้วยหมวด: `color-*`, `radius-*`, `space-*`, `shadow-*`, `text-*`, `font-*`

## Handler/usecase (จาก stack Go)
- `*PageHandler` = คืน HTML, `*Handler` = คืน JSON
- usecase เรียก business ("ไม่ใช่ service" ในบริบท Go monolith — ใช้คำว่า usecase)
- Nest.js / Express.js ใช้คำว่า `service` สำหรับชั้น business ตาม [`project-structure.md`](project-structure.md)

## Component (UI)
- ชื่อ component = `PascalCase` (`NavHeader`, `ThemeToggle`)
- variant/size เป็น string literal ตาม spec (`"primary"`, `"sm"`) — anatomy ดู [`../components/`](../components/README.md)
