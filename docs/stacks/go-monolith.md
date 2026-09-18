# Stack: Go Monolith (Chi + HTMX + Tailwind v4)

**สถานะ: v1 (เต็ม)** — แนวทาง setup โปรเจกต์ full-stack SSR ให้ตรงมาตรฐาน i24
*ไม่ใช่ template code สำเร็จ — เป็นแนวทาง อ้าง SSOT ที่ [`../brand/`](../brand/design-tokens.md) และ [`../components/`](../components/README.md)*
**StackName:** `go-monolith` · **has_ui:** yes · **theme pin:** [`tailwindcss@4.3.3`](../brand/theme-tailwind.md)

## เหมาะกับ
บริการที่ render HTML ฝั่ง server + โต้ตอบด้วย HTMX (เช่น admin, dashboard, ระบบภายใน)

## Layering (บังคับ)
```
handler (page + API) → usecase → repository → domain
internal/template/   → SSR + HTMX partials (ไม่มี business logic)
```
| Layer | หน้าที่ |
|-------|---------|
| `internal/domain` | types/params/results — no I/O |
| `internal/repository` | DB, cache, queue — no HTTP |
| `internal/usecase` | business rule, validation, orchestration |
| `internal/handler` | HTTP parse/encode; `*PageHandler`=HTML, `*Handler`=JSON |
| `internal/template` | view model, engine, embedded templates/static |
| `cmd/` | wiring, env, migrations ตอน startup |

## โครงไดเรกทอรีแนะนำ
```
cmd/main.go                 API entry (APP_PORT)
cmd/worker/                 worker/cron (ถ้ามี)
internal/domain/
internal/repository/
internal/usecase/
internal/handler/
internal/template/
  layout.html  partials/  pages/
  static/app.css           ← Tailwind build output (go:embed)
docs/  (อ้าง common-library หรือ submodule)
```

## Theme setup (Tailwind v4.3.3 + go:embed)
1. เขียน `@theme` + `data-theme` ตาม [`../brand/theme-tailwind.md`](../brand/theme-tailwind.md) ลง `input.css` — pin `tailwindcss@4.3.3`; อ้างชื่อ token จาก [`../brand/`](../brand/design-tokens.md) ห้ามใส่ hex ล้วน
2. build: `npx @tailwindcss/cli@4.3.3 -i input.css -o internal/template/static/app.css`
3. `//go:embed static/*` แล้ว serve ผ่าน handler; รวม `<link rel="stylesheet" href="/static/app.css">` ใน layout
4. **CSS เปลี่ยน → build:css ก่อน `go build`** (เพราะ embed ตอน compile)

## HTMX partial convention
- component จาก [`../components/`](../components/README.md) → เป็น `{{define "partials/xxx"}}` ใน `internal/template/partials/`
- search/table pattern: หน้าเต็ม + endpoint `/{resource}/table` คืน `<tbody>`/บล็อก partial (ดู [`../components/table.md`](../components/table.md) — หัวตาราง Cool Slate)
- ปุ่ม/ฟอร์มยิง `hx-get/hx-post` → handler คืน partial

## Routing (Chi)
- `*PageHandler` → คืน HTML (full page หรือ partial ตาม `HX-Request`)
- `*Handler` → คืน JSON (snake_case, ดู [`../conventions/json-api.md`](../conventions/json-api.md))
- map HTTP status ใน handler เท่านั้น

## Convention อ้างอิง
- โครงสร้าง/naming/error/git → [`../conventions/`](../conventions/project-structure.md)
- error wrap: `fmt.Errorf("...: %w", err)` ไม่กลืน error เงียบ

## Checklist เริ่มโปรเจกต์ (สรุป — เต็มดู [`../scaffolding.md`](../scaffolding.md))
- [ ] วางโครง `cmd/` + `internal/` ตาม layering
- [ ] ตั้ง Tailwind `4.3.3` + `@theme` จาก [`../brand/theme-tailwind.md`](../brand/theme-tailwind.md) + build `app.css`
- [ ] `go:embed` templates/static + layout ที่มี FOUC guard theme
- [ ] สร้าง nav-header + theme-mode toggle
- [ ] 🔒 ใส่ footer **"Powered by i24"** ใน layout กลาง ([`../components/footer.md`](../components/footer.md), catalog [`../components/README.md`](../components/README.md)) — **บังคับทุกหน้า** + วางโลโก้เป็น static asset (`go:embed`)
- [ ] ยึด component spec ตอนสร้าง UI — ลิงก์ spec ไม่สำเนา anatomy
