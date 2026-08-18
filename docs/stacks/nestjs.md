# Stack: Nest.js (Backend)

**สถานะ: v1.1 (เต็ม)** — แนวทาง setup Backend API (REST) ฝั่ง TypeScript ให้ตรงมาตรฐาน i24
*ไม่ใช่ template code สำเร็จ — เป็นแนวทาง + snippet อ้างอิง; response/JSON ยึด [`../conventions/json-api.md`](../conventions/json-api.md)*

## เหมาะกับ
Backend ที่ต้องการโครง modular + Dependency Injection + decorator ครบ (ทีมกลาง-ใหญ่, โดเมนหลายโมดูล)

## Layering (บังคับ)
```
controller  → service      → repository   → (db/external)
 (HTTP)        (business)     (data access)
```
| ชั้น | หน้าที่ | ห้าม |
|------|---------|------|
| controller | parse/validate input, เรียก service, map HTTP status | ห้ามมี business logic |
| service | business rule, orchestration, transaction | ห้ามแตะ HTTP (req/res) |
| repository | query DB / external | ห้ามมี business rule |
| dto | รูปร่าง input/output + validation | — |

## โครงไดเรกทอรี
```
src/
  main.ts                 bootstrap: ValidationPipe, filter, CORS, PORT จาก env
  app.module.ts
  modules/
    <feature>/
      <feature>.controller.ts
      <feature>.service.ts
      <feature>.repository.ts
      <feature>.module.ts
      dto/
        create-<feature>.dto.ts
        <feature>-response.dto.ts
  common/
    filters/http-exception.filter.ts     → error envelope
    interceptors/transform.interceptor.ts → success envelope + snake_case
    interceptors/logging.interceptor.ts
    middleware/request-id.middleware.ts
    guards/                               (auth — แนวทางเท่านั้น)
  config/
    env.validation.ts                     schema validate ตอน boot
    configuration.ts
```

## 1) Bootstrap + config
```ts
// main.ts
const app = await NestFactory.create(AppModule);
app.useGlobalPipes(new ValidationPipe({ whitelist: true, transform: true }));
app.useGlobalFilters(new HttpExceptionFilter());
app.useGlobalInterceptors(new TransformInterceptor());
await app.listen(process.env.PORT ?? 3000);
```
- env ผ่าน `@nestjs/config` + validate ด้วย schema (zod/joi) — แอปไม่ boot ถ้า env ไม่ครบ

## 2) Validation (DTO)
```ts
export class CreateInvoiceDto {
  @IsString() @Length(1, 50) invoice_no: string;
  @IsNumber() total_amount: number;
}
```
- ใช้ `class-validator` + `whitelist:true` กัน field แปลกปลอม
- field เป็น `snake_case` ให้ตรง JSON convention

## 3) Response envelope (ของกลาง backend)
success ผ่าน `TransformInterceptor`:
```ts
// { data, error: null, meta }
return next.handle().pipe(map((data) => ({ data, error: null, meta: {} })));
```
error ผ่าน `HttpExceptionFilter`:
```ts
// { data: null, error: { code, message, details } }
const status = exception instanceof HttpException ? exception.getStatus() : 500;
res.status(status).json({ data: null, error: { code, message, details } });
```
โครงตรงกับ [`expressjs.md`](expressjs.md) เป๊ะ — client ตัวเดียวใช้ได้ทั้งสอง

## 4) HTTP status
- map ใน controller (throw `BadRequestException`, `NotFoundException`, ...) → filter แปลงเป็น envelope
- 201 สำหรับสร้าง, 200 ทั่วไป, 4xx validation/auth, 5xx server (ดู [`../conventions/json-api.md`](../conventions/json-api.md))

## 5) Logging
- `LoggingInterceptor` + `RequestIdMiddleware` → structured log พร้อม correlation id ต่อ request
- log level จาก env

## 6) Auth (แนวทาง — ไม่รวม implement สำเร็จ, out-of-scope v1)
- ใช้ `Guard` + strategy (เช่น JWT) ที่ระดับ controller/route
- แยก config secret จาก env — ห้าม hardcode
- รายละเอียด implement ปล่อยให้แต่ละโปรเจกต์ (ยังไม่ทำ template auth กลาง)

## 7) Testing convention
- unit: service (mock repository)
- e2e: controller ผ่าน `Test.createTestingModule`
- ตั้งชื่อไฟล์ `*.spec.ts`

## Checklist เริ่มโปรเจกต์
- [ ] `nest new` + โครง `modules/`, `common/`, `config/`
- [ ] `ValidationPipe` + `HttpExceptionFilter` + `TransformInterceptor` global
- [ ] env schema validate ตอน boot
- [ ] request-id + logging interceptor
- [ ] envelope + JSON snake_case ตรง [`../conventions/json-api.md`](../conventions/json-api.md)
- [ ] naming/structure/git ตาม [`../conventions/`](../conventions/project-structure.md)
