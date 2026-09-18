# Scaffolding — เริ่มโปรเจกต์ใหม่

**ไม่มี CLI generator** — ไม่มี `create-i24`, สคริปต์ scaffold, หรือเครื่องมือสร้างโปรเจกต์อัตโนมัติ ทีมเริ่มโปรเจกต์**ด้วยมือ**ตาม checklist นี้เท่านั้น (มติ: เอกสาร-based)

**Document contract: Read scaffolding** — ไฟล์นี้ต้องมีขั้นร่วมทุก stack **และ** checklist แยกต่อ `StackName` ทั้ง 4 (`go-monolith`, `nextjs`, `nestjs`, `expressjs`). ขาด stack ใด หรือขาดขั้น footer **"Powered by i24"** สำหรับเส้นทาง UI = ผิดสัญญา

ใช้ checklist ด้านล่างให้ตรงมาตรฐาน i24 — ไม่ใช่ skeleton โปรเจกต์เต็ม

## ขั้นตอนร่วม (ทุก stack)

ทำขั้นนี้ก่อน แล้วไป checklist ของ stack ที่เลือก

1. เลือก **หนึ่ง** `StackName` แล้วเปิด guide ใน [`stacks/`](stacks/go-monolith.md):
   - [`go-monolith`](stacks/go-monolith.md) — has_ui
   - [`nextjs`](stacks/nextjs.md) — has_ui
   - [`nestjs`](stacks/nestjs.md) — backend, no UI
   - [`expressjs`](stacks/expressjs.md) — backend, no UI
2. วางโครงไดเรกทอรีตาม layering — [`conventions/project-structure.md`](conventions/project-structure.md)
3. ตั้งชื่อไฟล์/type ตาม [`conventions/naming.md`](conventions/naming.md) และ branch/commit ตาม [`conventions/git.md`](conventions/git.md)
4. **สีและ theme จาก SSOT เท่านั้น** — อ้าง**ชื่อ token** จาก [`brand/design-tokens.md`](brand/design-tokens.md) และ [`brand/palette.md`](brand/palette.md) (เช่น `color-primary`, `color-text`, `color-sidebar-bg`) — **ห้าม hardcode hex** / ห้าม orphan brand hex ในโค้ดหรือในเอกสารนี้. ต่อ `@theme` ตาม [`brand/theme-tailwind.md`](brand/theme-tailwind.md)
5. **เส้นทาง UI** (บังคับเมื่อมีหน้าเว็บ): theme mode light/dark ตาม [`components/theme-mode.md`](components/theme-mode.md) + FOUC guard; nav-header และ component ตาม catalog [`components/`](components/README.md) — ลิงก์ spec ไม่สำเนา anatomy
6. 🔒 **เส้นทาง UI — footer "Powered by i24"** ใน layout กลางทุกหน้า ตาม [`components/footer.md`](components/footer.md). Backend ที่ไม่มี UI **ไม่ต้อง**ใส่ footer จนกว่าจะเพิ่มหน้าเว็บ
7. JSON API (backend และ client ที่เรียก API): envelope + `snake_case` ตาม [`conventions/json-api.md`](conventions/json-api.md)
8. อ้าง common-library เป็น reference (submodule / คัดลอก `docs/` / ลิงก์) — **อย่าสร้าง CLI generator**

## Checklist ต่อ stack

แต่ละ `StackName` มี ChecklistStep ของตัวเอง — **ห้ามรวม** Nest.js กับ Express.js เป็นชุดเดียว

### `go-monolith` — Go monolith (has_ui) — [รายละเอียด](stacks/go-monolith.md)

- [ ] โครง `cmd/` + `internal/{domain,repository,usecase,handler,template}` ตาม [`conventions/project-structure.md`](conventions/project-structure.md)
- [ ] Pin Tailwind **4.3.3** + `@theme` จากชื่อ token → build `app.css` → `go:embed` — ดู [`brand/theme-tailwind.md`](brand/theme-tailwind.md); อ้าง [`brand/design-tokens.md`](brand/design-tokens.md) **ห้ามใส่ hex ล้วน**
- [ ] layout + FOUC guard + nav-header + theme toggle ตาม [`components/theme-mode.md`](components/theme-mode.md) และ catalog [`components/`](components/README.md)
- [ ] 🔒 footer **"Powered by i24"** ใน layout กลางทุกหน้า — [`components/footer.md`](components/footer.md)
- [ ] JSON handler (`*Handler`) ใช้ envelope + `snake_case` ตาม [`conventions/json-api.md`](conventions/json-api.md)
- [ ] `npm run build:css` ก่อน `go build`

### `nextjs` — Next.js (has_ui) — [รายละเอียด](stacks/nextjs.md)

- [ ] Next.js App Router + TypeScript ตาม [`stacks/nextjs.md`](stacks/nextjs.md)
- [ ] Pin Tailwind **4.3.3** ใน `styles/app.css` (`@theme` + `[data-theme]`) แล้ว import ใน `layout.tsx` — ดู [`brand/theme-tailwind.md`](brand/theme-tailwind.md); อ้างชื่อ token จาก [`brand/design-tokens.md`](brand/design-tokens.md) **ห้ามใส่ hex ล้วน**
- [ ] FOUC guard + ThemeProvider ตาม [`components/theme-mode.md`](components/theme-mode.md)
- [ ] `components/ui/` ตาม catalog [`components/`](components/README.md) — ลิงก์ spec ไม่สำเนา anatomy
- [ ] 🔒 footer **"Powered by i24"** ใน root layout ทุกหน้า — [`components/footer.md`](components/footer.md)
- [ ] `lib/fetcher` ใช้ envelope + `snake_case` ตาม [`conventions/json-api.md`](conventions/json-api.md)

### `nestjs` — Nest.js (backend, no UI) — [รายละเอียด](stacks/nestjs.md)

- [ ] โครง `modules/` + `common/` + `config/` (controller → service → repository) ตาม [`stacks/nestjs.md`](stacks/nestjs.md) และ [`conventions/project-structure.md`](conventions/project-structure.md)
- [ ] `ValidationPipe` + Global Exception Filter + TransformInterceptor
- [ ] env schema validate ตอน boot
- [ ] success/error envelope + JSON `snake_case` ตาม [`conventions/json-api.md`](conventions/json-api.md)
- [ ] **ไม่บังคับ footer** — stack นี้ไม่มี UI. ถ้าเพิ่มหน้าเว็บภายหลัง ให้ทำขั้นร่วมเส้นทาง UI รวม footer **"Powered by i24"** ([`components/footer.md`](components/footer.md)) และต่อ theme จาก [`brand/theme-tailwind.md`](brand/theme-tailwind.md) (pin `tailwindcss@4.3.3`)

### `expressjs` — Express.js (backend, no UI) — [รายละเอียด](stacks/expressjs.md)

- [ ] โครง `routes/` + `controllers/` + `services/` + `repositories/` ตาม [`stacks/expressjs.md`](stacks/expressjs.md) และ [`conventions/project-structure.md`](conventions/project-structure.md)
- [ ] middleware order: requestId → json → routes → notFound → errorHandler
- [ ] env validate (zod) ตอน boot
- [ ] success/error envelope + JSON `snake_case` ตาม [`conventions/json-api.md`](conventions/json-api.md)
- [ ] **ไม่บังคับ footer** — stack นี้ไม่มี UI. ถ้าเพิ่มหน้าเว็บภายหลัง ให้ทำขั้นร่วมเส้นทาง UI รวม footer **"Powered by i24"** ([`components/footer.md`](components/footer.md)) และต่อ theme จาก [`brand/theme-tailwind.md`](brand/theme-tailwind.md) (pin `tailwindcss@4.3.3`)

## ก่อนถือว่าเสร็จ

- [ ] สีถูกต้องตาม**ชื่อ token** ([`brand/palette.md`](brand/palette.md), [`brand/design-tokens.md`](brand/design-tokens.md)) — ไม่มี hex ล้วนในโค้ด
- [ ] (UI) สลับ light/dark ได้ ไม่มีจอกระพริบ — [`components/theme-mode.md`](components/theme-mode.md)
- [ ] 🔒 **(UI เท่านั้น)** footer **"Powered by i24"** แสดงทุกหน้า — [`components/footer.md`](components/footer.md). Backend ไม่มี UI ไม่ต้องมี footer
- [ ] (UI) component ผ่าน a11y ขั้นต่ำในแต่ละ spec ที่ [`components/`](components/README.md)
- [ ] JSON envelope + `snake_case` ตาม [`conventions/json-api.md`](conventions/json-api.md)
- [ ] naming / structure / git ตาม [`conventions/naming.md`](conventions/naming.md), [`conventions/project-structure.md`](conventions/project-structure.md), [`conventions/git.md`](conventions/git.md)
