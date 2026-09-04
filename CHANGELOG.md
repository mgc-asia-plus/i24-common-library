# Changelog

ทุกการเปลี่ยนแปลงสำคัญของ i24-common-library บันทึกที่นี่
รูปแบบอิง [Keep a Changelog](https://keepachangelog.com/) · เวอร์ชันแบบ SemVer

## [Unreleased]

### Changed — ธีม Luxury Clear Glass (sync จาก prototype)
- **Accent เปลี่ยน coral → navy** (`#1E3A8A`; 400 `#2E4EA6`, 600 `#152C63`); coral จากโลโก้ไม่ใช้เป็น accent แล้ว (เหลือเฉพาะในตัวโลโก้)
- **Neutral → slate/charcoal** (`ink-900 #1A1D24`, `ink-700 #333A46`, `ink-500 #6B7482`, `ink-300 #D2D7DF`, `black #0A0C11`)
- เพิ่มสี **gold** (`#A8811C`/`#E7C873`) สำหรับ status text ในตาราง
- **Gradient brand เป็นแดงล้วน** (`#E11D27 → #A81319`) + gradient accent navy (`#2A4AA0 → #152C63`)
- **Clear glass** (blur 3px + เคลือบเงา 4 ชั้น gloss/sheen/top/tint + เงาหลายชั้น) แทน frosted; page-bg `#EEF0F4`/`#0A0C11`; blob แดง/น้ำเงิน/เทา
- status: danger `#C1121F`, success `#137A47`, warning `#B7791F`, info navy
- components: button เพิ่ม variant `accent`; badge เพิ่ม `status` (glass + gold), brand/accent เป็น gradient
- sync `docs/brand/{palette,design-tokens,theme-tailwind,effects}.md` ให้ตรง `prototype/index.html`
- ⚠️ a11y: `gold` บน light ≈ 3.6:1 (ใช้ text หนา/ใหญ่ หรือเฉดเข้มขึ้น); `white` บน `red-500` ≈ 4.4:1
- nav-header: ใช้ **โลโก้จริง `i24_LOGO.svg`** (ทั้ง nav + footer) แทนกล่องตัวอักษร; active link = `color-text` (ไม่ใช่แดง)
- sync component ที่ค้างธีมเก่า: `nav-header` (glass pill + logo), `table` (selected/hover = `grad-brand-soft`, status = badge gold), `input` (focus = navy ring); เพิ่ม semantic `color-bg/surface/border`; แก้ตัวอย่าง token ใน `naming.md`

### Added — v1 (documentation)
- โครงเอกสารกลาง: `README.md`, `docs/README.md`
- `docs/brand/`: `palette.md` (สีจากโลโก้ marked), `design-tokens.md` (primitive + semantic light/dark), `theme-tailwind.md` (Tailwind v4 `@theme`)
- `docs/components/`: README + button, badge, card, input, table, nav-header, alert, theme-mode, footer
- `docs/components/footer.md`: 🔒 "Powered by i24" — **มาตรฐานบังคับทุกระบบที่มี UI** (ผูกเข้า checklist ของ go-monolith, nextjs และ scaffolding); เพิ่ม footer ใน `prototype/index.html`
- `docs/stacks/`: `go-monolith.md`, `nextjs.md`, `nestjs.md`, `expressjs.md` (เต็มทั้งหมด)
- `docs/conventions/`: project-structure, naming, git, json-api
- `docs/scaffolding.md`: checklist เริ่มโปรเจกต์
- `prototype/index.html`: หน้า preview self-contained (swatch สีจริง + ทุก component + toggle light/dark)

### Added — v1.1 (backend เต็ม)
- `docs/stacks/nestjs.md`: layering controller→service→repository, ValidationPipe/DTO, exception filter + transform interceptor (envelope), logging, auth (แนวทาง)
- `docs/stacks/expressjs.md`: layering route→controller→service→repository, zod validation, error middleware (envelope), request-id/logging, auth (แนวทาง)
- backend envelope + JSON snake_case ตรงกันทั้ง Nest.js และ Express.js

### Added — Modern theme (gradient + glass)
- `docs/brand/effects.md`: มาตรฐาน gradient + glass (glassmorphism) — tokens, recipe, ambient background (neutral, ไม่ปนแดง), a11y (contrast, `prefers-reduced-transparency`, fallback `@supports`), performance
- design-tokens/theme-tailwind: เพิ่ม `gradient-brand`, glass tokens, `page-bg`; อัปเดต `font-sans` (-apple-system → Inter → Noto Sans Thai) + web font loading
- palette: เพิ่ม Brand gradient (`#EC2129 → #F4574B → #F48569`)
- components: เพิ่ม variant `glass` (button, card) + หลักการ modern (gradient เฉพาะ element ห้ามที่ bg หน้า/ตัวหนังสือ)
- `prototype/index.html`: รีดีไซน์แนว modern glass + gradient + โหลดฟอนต์ Inter/Noto Sans Thai; ambient background โทน neutral; ตัวหนังสือ/พื้นหลังไม่ใช้ gradient แดง

### Changed
- ลบ `.kiro/steering/{product,tech,structure,session-boot}.md` (ของ i24-etax-service ที่ก็อปมาผิดโปรเจกต์); คงเหลือ `aidlc.md` (shim ของ common library)

### Changed — ยืนยันค่าสีจริง
- **ยืนยัน brand color จากไฟล์ vector ทางการ `i24_LOGO.svg`**: `brand-red-500 = #EC2129`, `brand-coral-400 = #F48569`, `white = #FFFFFF` (fill จริงในไฟล์)
- (ก่อนหน้า sample จาก PNG ได้ `#EC2028` — ต่างจาก vector 1 หน่วย, ยึดค่า vector `#EC2129`)
- Footer/prototype ใช้ `i24_LOGO.svg` (vector คมทุกจอ) แทน PNG
- ปรับเฉด derived รอบสีหลัก: red-{50 `#FDECED`,100 `#FBD0D2`,400 `#F04E52`,600 `#C81B22`,700 `#AA171D`}, coral-{300 `#F7A48A`,500 `#F1684D`}
- อัปเดตค่าใน `docs/brand/{palette,design-tokens,theme-tailwind}.md` + blueprints + context
- คำนวณ contrast: white/red-500 ≈ 4.37:1 (ผ่าน text ใหญ่/ปุ่ม), white/red-600 ≈ 5.78:1 (ผ่าน AA ทุกขนาด)

### Pending / ต้องทำก่อน lock (production)
- ⚠️ หากมี **brand guide ทางการ** ให้เทียบค่ากับที่ sample แล้วยึด brand guide เป็นหลัก
- ตรวจ WCAG contrast เต็มด้วยเครื่องมือ + assistive tech (โดยเฉพาะ white text เล็กบนพื้นแดง → ใช้ red-600)

### Out of scope (v1)
- ยังไม่ publish เป็น package จริง (ใช้โหมด reference/clone)
- ยังไม่มี docs site เต็มรูปแบบ
- backend template ไม่รวม auth/DB/ORM สำเร็จรูป
- ยังไม่รองรับ i18n / ไม่มี CI auto-publish
