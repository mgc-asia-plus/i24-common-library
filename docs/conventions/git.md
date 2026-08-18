# Convention: Git

## Branch
- `main` = พร้อม deploy เสมอ
- ทำงานบน branch: `feat/<สั้น>`, `fix/<สั้น>`, `chore/<สั้น>`, `docs/<สั้น>`
- ห้าม push ตรงเข้า `main` — ผ่าน PR/MR

## Commit (Conventional Commits)
```
<type>(<scope>): <subject>
```
- type: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`, `style`, `perf`
- subject สั้น กระชับ (< 70 ตัวอักษร), ปัจจุบันกาล
- ตัวอย่าง: `feat(button): add danger variant`, `docs(brand): confirm logo hex values`

## Pull Request
- title กระชับ < 70 ตัวอักษร
- body: สรุปการเปลี่ยนแปลง + สิ่งที่ทดสอบ + สิ่งที่ยัง block
- 1 PR = 1 เรื่อง (diff เล็กที่สุดที่ถูกต้อง — ไม่ refactor แถม)

## กติกาความปลอดภัย
- ห้าม commit secret / `.env` / credential
- ไม่แก้ git config ของเครื่องรวม
- destructive (`push --force`, `reset --hard`) ทำเมื่อจำเป็นและรู้ผลเท่านั้น
- ไม่ข้าม hook (`--no-verify`) เว้นแต่จำเป็นและตั้งใจ

## เอกสาร/มาตรฐาน
- แก้ค่าสี/tokens/spec ที่ common-library → commit `docs(...)` + อัปเดต [`../../CHANGELOG.md`](../../CHANGELOG.md)
