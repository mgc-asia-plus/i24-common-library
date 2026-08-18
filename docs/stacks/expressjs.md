# Stack: Express.js (Backend)

**สถานะ: v1.1 (เต็ม)** — แนวทาง setup Backend API (REST) ฝั่ง Node/TypeScript ให้ตรงมาตรฐาน i24
*ไม่ใช่ template code สำเร็จ — เป็นแนวทาง + snippet อ้างอิง; response/JSON ยึด [`../conventions/json-api.md`](../conventions/json-api.md)*

## เหมาะกับ
Backend ที่ต้องการโครงเบา ควบคุมเองได้มาก ไม่ต้องการ framework หนัก (service เล็ก-กลาง)

## Layering (บังคับ)
```
route  → controller → service    → repository   → (db/external)
                        (business)   (data access)
```
| ชั้น | หน้าที่ | ห้าม |
|------|---------|------|
| route | ผูก path + middleware + controller | ห้ามมี logic |
| controller | parse/validate, เรียก service, ส่ง response ผ่าน helper | ห้ามมี business logic |
| service | business rule, orchestration | ห้ามแตะ req/res |
| repository | query DB / external | ห้ามมี business rule |

## โครงไดเรกทอรี
```
src/
  index.ts               bootstrap: middleware order, PORT จาก env
  app.ts                 สร้าง express app + attach routes/middleware
  routes/
    index.ts
    <feature>.route.ts
  controllers/
    <feature>.controller.ts
  services/
    <feature>.service.ts
  repositories/
    <feature>.repository.ts
  middlewares/
    error.middleware.ts        → error envelope
    request-id.middleware.ts
    not-found.middleware.ts
    validate.middleware.ts      → zod validator
  schemas/
    <feature>.schema.ts         (zod)
  lib/
    response.ts                 → helper success/error envelope
  config/
    env.ts                      โหลด+validate env
```

## 1) Bootstrap + middleware order
```ts
// app.ts
const app = express();
app.use(requestId);
app.use(express.json());
app.use("/api", routes);
app.use(notFound);      // 404
app.use(errorHandler);  // ต้องอยู่ท้ายสุด (4 args)
```
```ts
// index.ts
app.listen(env.PORT, () => log.info(`listening on ${env.PORT}`));
```
- env โหลด+validate (zod) ใน `config/env.ts` — throw ถ้าไม่ครบ (แอปไม่ start)

## 2) Validation (zod ที่ boundary)
```ts
export const createInvoiceSchema = z.object({
  invoice_no: z.string().min(1).max(50),
  total_amount: z.number(),
});
// validate.middleware: schema.parse(req.body) → 400 + error envelope ถ้าไม่ผ่าน
```
- field `snake_case` ตรง JSON convention

## 3) Response envelope (ของกลาง backend — ตรงกับ Nest.js)
```ts
// lib/response.ts
export const ok  = (res, data, meta = {}) => res.json({ data, error: null, meta });
export const fail = (res, status, code, message, details = []) =>
  res.status(status).json({ data: null, error: { code, message, details } });
```
error middleware กลาง:
```ts
export function errorHandler(err, req, res, next) {
  const status = err.status ?? 500;
  fail(res, status, err.code ?? "internal_error", err.message, err.details);
}
```
โครง envelope ตรงกับ [`nestjs.md`](nestjs.md) — client เดียวใช้ได้ทั้งสอง

## 4) HTTP status
- controller โยน error ที่มี `status`+`code` → error middleware แปลงเป็น envelope
- 201 สร้าง, 200 ทั่วไป, 4xx validation/auth, 5xx server (ดู [`../conventions/json-api.md`](../conventions/json-api.md))

## 5) Logging
- `request-id.middleware` แนบ correlation id + logger (pino/winston) structured
- log level จาก env

## 6) Auth (แนวทาง — ไม่รวม implement สำเร็จ, out-of-scope v1)
- middleware ตรวจ token (เช่น JWT) ก่อนถึง controller
- secret จาก env — ห้าม hardcode
- implement ปล่อยแต่ละโปรเจกต์ (ยังไม่มี template auth กลาง)

## 7) Testing convention
- unit: service (mock repository)
- integration: route ผ่าน `supertest`
- ตั้งชื่อ `*.test.ts`

## Checklist เริ่มโปรเจกต์
- [ ] โครง `routes/controllers/services/repositories/middlewares/schemas`
- [ ] middleware order: requestId → json → routes → notFound → errorHandler
- [ ] env validate (zod) ตอน boot
- [ ] response helper (envelope) + validate middleware
- [ ] envelope + JSON snake_case ตรง [`../conventions/json-api.md`](../conventions/json-api.md)
- [ ] naming/structure/git ตาม [`../conventions/`](../conventions/project-structure.md)
