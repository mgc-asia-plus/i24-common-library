# Convention: Project Structure

หลักการจัดโครงโปรเจกต์ที่ใช้ร่วมทุก stack ที่เอกสารรับรอง (`go-monolith`, `nextjs`, `nestjs`, `expressjs`)

**Read convention:** ชุด ConventionSet ต้องครบ 4 ไฟล์ — [`project-structure.md`](project-structure.md) · [`naming.md`](naming.md) · [`git.md`](git.md) · [`json-api.md`](json-api.md) — ขาดไฟล์ใด = ผิดสัญญา

ขั้นตอน setup / ต่อ theme / footer อยู่ที่ stack guide — convention นี้อธิบายชั้นและโฟลเดอร์เท่านั้น:
- [`../stacks/go-monolith.md`](../stacks/go-monolith.md)
- [`../stacks/nextjs.md`](../stacks/nextjs.md)
- [`../stacks/nestjs.md`](../stacks/nestjs.md)
- [`../stacks/expressjs.md`](../stacks/expressjs.md)

ค่าสีและ token อยู่ที่ [`../brand/`](../brand/design-tokens.md) — ห้ามสำเนาตาราง palette / hex ในไฟล์ convention

## หลักการร่วม
- **แยกชั้นชัด (layering)**: HTTP/handler ↔ business ↔ data — ห้ามข้ามชั้น
- **ไม่มี business logic ใน handler/controller/route**: parse/encode + map status เท่านั้น
- **domain/types ไม่พึ่ง I/O**
- **config จาก env** — ไม่ hardcode; validate ตอน boot
- **ไฟล์เดียว = ความรับผิดชอบเดียว**; โฟลเดอร์จัดตาม feature/domain ไม่ใช่ตามชนิดไฟล์อย่างเดียวเมื่อโปรเจกต์โต

## Layering มาตรฐาน
```
(HTTP) handler/controller/route
   → usecase/service      (business rule, validation, orchestration)
     → repository          (DB, cache, external — no HTTP)
       → domain            (types, params, results — no I/O)
```

## ต่อ stack (สรุปโครง)
| Stack | id | HTTP | business | data |
|-------|----|------|----------|------|
| Go monolith | `go-monolith` | `internal/handler` (+ `internal/template` สำหรับ HTML) | `internal/usecase` | `internal/repository` ; domain ที่ `internal/domain` |
| Next.js | `nextjs` | `app/` (App Router) + `lib/fetcher` | — (ไม่มี business layer ฝั่ง FE) | เรียก API ตาม [`json-api.md`](json-api.md) |
| Nest.js | `nestjs` | `*.controller.ts` ใน `modules/<feature>/` | `*.service.ts` | `*.repository.ts` |
| Express.js | `expressjs` | `routes/` + `controllers/` | `services/` | `repositories/` |

โครงโฟลเดอร์ละเอียดและขั้นตอน bootstrap ดู stack guide ของ stack นั้น — อย่าคัดลอก checklist/setup มาที่นี่

JSON ที่ชั้น HTTP (Go `*Handler`, Nest controller, Express controller) ใช้ envelope ตาม [`json-api.md`](json-api.md)

## กติกา
- ดึงมาตรฐานร่วมจากเอกสารกลางนี้ — อย่า fork convention เองต่อโปรเจกต์
- โฟลเดอร์จัดตาม feature/domain ตามตารางด้านบน — ไม่ผสมชั้นข้าม stack ในโมดูลเดียวกัน
- ชื่อไฟล์/type ตาม [`naming.md`](naming.md); branch/commit ตาม [`git.md`](git.md)
