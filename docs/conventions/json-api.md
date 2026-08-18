# Convention: JSON / API

## Field naming
- ทุก field ใน JSON payload = **`snake_case`** (`created_at`, `tax_id`, `total_amount`)
- ฝั่ง TS ที่ต้องการ camelCase ให้ map ที่ boundary (fetcher/serializer) ไม่ใช่กลาง ๆ

## Response envelope (ใช้ร่วม backend ทุกตัว)
สำเร็จ:
```json
{ "data": { }, "error": null, "meta": { } }
```
ผิดพลาด:
```json
{ "data": null, "error": { "code": "validation_error", "message": "อธิบายสั้น", "details": [] } }
```
- `meta` ใช้กับ pagination: `{ "page": 1, "page_size": 20, "total": 137 }`
- `error.code` เป็น machine-readable (`snake_case`), `message` สำหรับแสดงผล

## HTTP status
- map status ที่ชั้น handler/controller เท่านั้น
- 200 สำเร็จ, 201 สร้าง, 400 validation, 401/403 auth, 404 not found, 409 conflict, 422 unprocessable, 5xx server
- error envelope แนบทุก 4xx/5xx

## Pagination
- query: `?page=1&page_size=20`
- คืน `meta.page / page_size / total`

## Dates / numbers
- วันที่/เวลา = ISO 8601 (`2026-08-17T09:00:00+07:00`)
- เงิน: ส่งเป็น string หรือ integer หน่วยย่อย (ระบุให้ชัดต่อ API) เพื่อกัน float error

## กติกา
- consistent ทุก service — client ตัวเดียวจัดการได้
- อย่าคืนโครงต่างกันในแต่ละ endpoint โดยไม่จำเป็น
