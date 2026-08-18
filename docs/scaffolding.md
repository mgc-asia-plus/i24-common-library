# Scaffolding — เริ่มโปรเจกต์ใหม่

ไม่มี generator อัตโนมัติ (มติ: เอกสาร-based). ใช้ checklist ด้านล่างเริ่มโปรเจกต์ด้วยมือให้ตรงมาตรฐาน i24

## ขั้นตอนร่วม (ทุก stack)
1. เลือก stack → เปิดเอกสารใน [`stacks/`](stacks/go-monolith.md)
2. วางโครงไดเรกทอรีตาม layering ([`conventions/project-structure.md`](conventions/project-structure.md))
3. ตั้งธีม/สีจาก [`brand/`](brand/design-tokens.md) — **ห้าม hardcode hex** ใช้ token
4. เพิ่ม theme mode (light/dark) ตาม [`components/theme-mode.md`](components/theme-mode.md) + FOUC guard
5. สร้าง nav-header + component ที่ใช้ ตาม [`components/`](components/README.md)
6. ตั้ง convention JSON/naming/git ([`conventions/`](conventions/naming.md))
7. อ้าง common-library เป็น reference (submodule / คัดลอก `docs/` / ลิงก์)

## Checklist ต่อ stack

### Go monolith (v1) — [รายละเอียด](stacks/go-monolith.md)
- [ ] โครง `cmd/` + `internal/{domain,repository,usecase,handler,template}`
- [ ] Tailwind v4 `@theme` จาก tokens → build `app.css` → `go:embed`
- [ ] layout + FOUC guard + nav-header + theme toggle
- [ ] `npm run build:css` ก่อน `go build`

### Next.js (v1) — [รายละเอียด](stacks/nextjs.md)
- [ ] Next.js App Router + TS
- [ ] `styles/app.css` (`@theme` + `[data-theme]`) + import ใน `layout.tsx`
- [ ] FOUC guard + ThemeProvider
- [ ] `components/ui/` ตาม spec + fetcher (JSON snake_case)

### Nest.js / Express.js (v1.1 — outline)
- [ ] โครง controller/service/repository ([nestjs](stacks/nestjs.md) / [expressjs](stacks/expressjs.md))
- [ ] validation + error envelope + JSON snake_case ([`conventions/json-api.md`](conventions/json-api.md))
- [ ] config/env validate ตอน boot
- (รายละเอียด backend เต็มจะเติมใน v1.1)

## ก่อนถือว่าเสร็จ
- [ ] สีถูกต้องตาม token ([`brand/palette.md`](brand/palette.md))
- [ ] สลับ light/dark ได้ ไม่มีจอกระพริบ
- [ ] 🔒 **footer "Powered by i24" แสดงทุกหน้า** (ระบบที่มี UI) — [`components/footer.md`](components/footer.md)
- [ ] component ผ่าน a11y ขั้นต่ำในแต่ละ spec
- [ ] JSON/naming/git ตาม convention
