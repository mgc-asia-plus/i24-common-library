# Deployment: common-library

## Summary
- **CI/CD**: GitHub — ไม่มี workflow; ปล่อยผ่าน PR แล้ว merge `main`
- **Target**: git repo เป็น SSOT — ไม่มี hosting / docs site / container
- **Strategy**: Recreate เทียบเท่า — merge ทับเอกสารชุดก่อน (ไม่มี downtime)
- **Environments**: `main` เท่านั้น — PR เป็นช่องตรวจ
- **IaC**: None
- **Secrets**: GitHub Secrets สำรองในอนาคต — ตอนนี้ไม่มี secret
- **Rollback**: `git revert` หรือ revert PR แล้ว merge ใหม่
- **Verification**: review properties บน PR + เปิดไฟล์ SSOT ได้หลัง merge

---

## Pipeline Architecture

ไม่มี CI job. “pipeline” คือ git + GitHub PR

### Stages

| # | Stage | Trigger | Purpose | Key Actions |
|---|---|---|---|---|
| 1 | Author | สาขา `feat/` `fix/` `docs/` `chore/` | แก้เอกสาร | ตาม `docs/conventions/git.md` |
| 2 | Review | เปิด PR เข้า `main` | ตรวจมาตรฐาน | checklist review properties ของ unit ที่แตะ + CHANGELOG |
| 3 | Release | merge PR เข้า `main` | ปล่อย SSOT | `main` = เวอร์ชันที่ทีมอื่นอ้าง |

### Flow Diagram

```
feature/fix/docs branch
        │
        ▼
   GitHub Pull Request
        │  reviewer: review properties + CHANGELOG
        ▼
   merge → main     =====  RELEASE
        │
        ▼
   consumers อ่าน docs/ จาก main
```

---

## Target Infrastructure

ไม่มีเซิร์ฟเวอร์ โหลดบาลานเซอร์ หรือ CDN ใน v1

### Topology

| Component | Service/Resource | Environment | Configuration |
|---|---|---|---|
| Source of truth | GitHub repo `mgc-asia-plus/i24-common-library` | `main` | Markdown ใน `docs/` + `prototype/index.html` |
| Preview | ไฟล์ใน PR / editor | PR | ไม่มี preview env |
| Brand SSOT | `docs/brand/` | `main` | Navy `#0F172A` |
| UI specs | `docs/components/` + `prototype/` | `main` | 14 spec |
| Delivery | `docs/stacks/` `docs/conventions/` `docs/scaffolding.md` | `main` | ไม่มี generator |

### Environment Layout

| Environment | Purpose | Trigger | Auto-deploy | Protection |
|---|---|---|---|---|
| PR | ตรวจเอกสารก่อนปล่อย | เปิด PR | ไม่มี deploy | reviewer + checklist |
| `main` | production ของคลังเอกสาร | merge PR | ไม่มี hosting | ห้าม push ตรง (กติกา git.md) |

---

## Promotion Flow

```
branch → PR (review) → merge main → ทีมอ่าน SSOT
```

- **PR**: ช่องเดียวก่อนปล่อย — ตรวจ properties ตาม unit (brand / components / delivery)
- **main**: ปล่อยทันทีเมื่อ merge — ไม่มี staging

---

## Security & Secrets

### Secrets Required

ไม่มี secret สำหรับปล่อยเอกสาร

| Secret | Purpose | Environments | Storage |
|---|---|---|---|
| — | ไม่ใช้ | — | ถ้ามี workflow ในอนาคต ใช้ GitHub Secrets |

### Network & Access

- เข้าถึงผ่าน GitHub permissions ของ org
- ห้าม commit secret / `.env` (ดู `docs/conventions/git.md`)
- ไม่มี secret injection เพราะไม่มี deploy job

---

## Operations Integration

operations design ไม่ได้ระบุเป็น `design/operations.md` — ใช้มติ Minimal จาก D3

### Health & Readiness

| Check | Endpoint/Method | Timeout | Failure Action |
|---|---|---|---|
| SSOT readable | เปิดไฟล์ใน `docs/` บน `main` | — | revert PR |
| Review properties | checklist ใน PR | ก่อน merge | อย่า merge |

ไม่มี `/health` — ไม่มี runtime

### Observability

- **Logging**: `CHANGELOG.md` + git history + บันทึก PR
- **Metrics**: ไม่มี
- **Alerting**: ไม่มี — ผู้ดูแลดู PR/issue

### Graceful Shutdown

ไม่ใช้ — ไม่มีโปรเซส

---

## Rollback Strategy

- **Method**: `git revert` ของ merge commit หรือ GitHub “Revert” PR แล้ว merge กลับ `main`
- **Trigger**: เอกสารผิด / ทำ SSOT ใช้ไม่ได้ / reviewer พบหลัง merge
- **Steps**:
  1. Revert merge บนสาขาใหม่
  2. เปิด PR อธิบายเหตุผล
  3. Merge เข้า `main`
  4. บันทึกใน `CHANGELOG.md`
- **Recovery time**: รอบ PR (นาที–ชั่วโมง)
- **Data considerations**: ไม่มี DB

---

## Files to Generate

ไม่มีไฟล์ pipeline / Docker / IaC / `.env` ตาม D5

| File | Purpose | Notes |
|---|---|---|
| *(none)* | ไม่สร้าง `.github/workflows/*` | D5-1: PR only |
| *(none)* | ไม่สร้าง `Dockerfile` / `infra/` | D5-2 + D5-7 |

ขั้น generate จะไม่เขียนไฟล์คอนฟิกใหม่ — ยืนยันว่ากติกาปล่อยอยู่ใน `docs/conventions/git.md` แล้ว (ห้าม push ตรง `main`, PR, Conventional Commits, CHANGELOG)

---

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Merge โดยไม่ผ่าน review checklist | Med | Med | บังคับ PR ใน git.md; reviewer ใช้ properties ของ unit |
| `colorSoT` ใน context ยังอ้างโลโก้แดง | High (มีอยู่แล้ว) | Low | หนี้เอกสาร — palette จริงที่ `docs/brand/`; แก้ context แยกงาน |
| ไม่มี CI ตรวจลิงก์เสีย | Med | Low | ตรวจมือตอน PR; เพิ่ม Actions ได้ภายหลัง |
| Push ตรง `main` | Low | High | branch protection บน GitHub (ตั้งมือใน org — ไม่ใช้ IaC) |

---

## Cost Estimate

| Resource | Environment | Estimated Monthly | Notes |
|---|---|---|---|
| GitHub repo | org | ตามแผน org | ไม่มี compute/CDN ของคลังนี้ |

**Total estimated**: ~$0 ส่วนเพิ่มจาก hosting ของ common-library /เดือน

*Note: ไม่คิดค่า Cloud Run/ECS — ไม่มี workload. ค่า GitHub org เป็นขององค์กรอยู่แล้ว.*
