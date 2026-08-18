# Convention: Project Structure

หลักการจัดโครงโปรเจกต์ที่ใช้ร่วมทุก stack (รายละเอียดต่อ stack ดู [`../stacks/`](../stacks/go-monolith.md))

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

## ต่อ stack (สรุป)
| Stack | HTTP | business | data |
|-------|------|----------|------|
| Go monolith | `internal/handler` | `internal/usecase` | `internal/repository` |
| Nest.js | `*.controller.ts` | `*.service.ts` | `*.repository.ts` |
| Express.js | `routes/`+`controllers/` | `services/` | `repositories/` |
| Next.js (FE) | route/page + `lib/fetcher` | — | เรียก API |

## กติกา
- ดึงมาตรฐานร่วมจากเอกสารกลางนี้ — อย่า fork convention เองต่อโปรเจกต์
- โฟลเดอร์ที่ Go เป็นเจ้าของ vs Laravel/อื่น ๆ ให้ชัด (กรณี monorepo ผสม)
