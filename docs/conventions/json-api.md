# Convention: JSON / API

สัญญา **JsonEnvelope** ที่ backend ทุกตัวในชุดที่ล็อก (Go JSON handler, Nest.js, Express.js) และ client (Next.js `lib/fetcher`) ต้องใช้ชุดเดียวกัน

ชุด ConventionSet: [`project-structure.md`](project-structure.md) · [`naming.md`](naming.md) · [`git.md`](git.md) · [`json-api.md`](json-api.md)

- **field_case** = `snake_case`
- **success_shape** / **error_shape** ตามด้านล่าง — ห้ามคิด envelope ใหม่
- **pagination** อยู่ใน `meta` เท่านั้น

Implement ต่อ stack ดู [`../stacks/`](../stacks/nestjs.md) — convention นี้ไม่คัดลอก interceptor/helper

## Field naming (`field_case`)
- ทุก field ใน JSON payload = **`snake_case`** (`created_at`, `tax_id`, `total_amount`, `page_size`)
- ฝั่ง TS ที่ต้องการ camelCase ให้ map ที่ boundary (fetcher/serializer) ไม่ใช่กลาง ๆ
- ชื่อ field ในโค้ดตาม [`naming.md`](naming.md)

## Response envelope

### success_shape
```json
{ "data": { }, "error": null, "meta": { } }
```

### error_shape
```json
{ "data": null, "error": { "code": "validation_error", "message": "อธิบายสั้น", "details": [] } }
```

- `error.code` เป็น machine-readable (`snake_case`), `message` สำหรับแสดงผล

## Pagination (ใน `meta`)
- query: `?page=1&page_size=20`
- คืนใน `meta` เท่านั้น: `{ "page": 1, "page_size": 20, "total": 137 }`
- ห้ามย้าย `page` / `page_size` / `total` ไปที่ `data` เป็นค่าเริ่มต้นของรายการ

## HTTP status
- map status ที่ชั้น handler/controller เท่านั้น
- 200 สำเร็จ, 201 สร้าง, 400 validation, 401/403 auth, 404 not found, 409 conflict, 422 unprocessable, 5xx server
- error envelope แนบทุก 4xx/5xx

## Dates / numbers
- วันที่/เวลา = ISO 8601 (`2026-08-17T09:00:00+07:00`)
- เงิน: ส่งเป็น string หรือ integer หน่วยย่อย (ระบุให้ชัดต่อ API) เพื่อกัน float error

## กติกา
- consistent ทุก service — client ตัวเดียวจัดการได้
- อย่าคืนโครงต่างกันในแต่ละ endpoint โดยไม่จำเป็น
