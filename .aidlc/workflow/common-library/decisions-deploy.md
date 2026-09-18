# Deploy Decisions (D5)

## Context Summary
- Feature: `common-library` — documentation-based common library (Markdown SSOT) ไม่ใช่ runtime service
- Git host: `github.com/mgc-asia-plus/i24-common-library` บนสาขา `main` — **ไม่มี** `.github/workflows/`, IaC, Dockerfile, package manager
- มติ D3: merge `main` = ปล่อย; review properties ตอน PR; **ไม่มี CI script**; ไม่มี docs site ใน v1
- Observability: Minimal — CHANGELOG + PR
- ไม่มี DB / secrets / health endpoint
- Build report: passed-with-warnings (`colorSoT` ใน context/manifest ยังอ้างโลโก้แดง `#EC2129`)
- ทีมใหญ่ (9+) แต่ artifact คือเอกสาร ไม่ใช่บริการที่ต้อง promote หลาย env

---

## Decision Questions

### D5-1: CI/CD Platform
**Question**: จะรัน pipeline ของคลังเอกสารนี้บนแพลตฟอร์มไหน?
- 1) GitHub Actions — repo อยู่บน GitHub แล้ว (ใช้ได้ถ้าต้องการ workflow ตรวจเอกสารในอนาคต)
- 2) GitLab CI
- 3) AWS CodePipeline + CodeBuild
- 4) Other: GitHub เป็นที่เก็บ + PR review อย่างเดียว **ไม่สร้าง workflow** ตามมติไม่มี CI script **(Recommended)**

**Answer**: 4) Other: GitHub เป็นที่เก็บ + PR review อย่างเดียว ไม่สร้าง workflow

---

### D5-2: Deployment Target
**Question**: “ปล่อย” common-library หมายถึงอะไรใน production?
- 1) Docker → Cloud Run (GCP)
- 2) Docker → ECS Fargate (AWS)
- 3) Docker → Kubernetes
- 4) Serverless → Lambda / Cloud Functions
- 5) Static → S3 + CloudFront / Vercel / Netlify (docs site — นอกขอบเขต v1)
- 6) VM → EC2 / Compute Engine
- 7) Other: git repo เป็น SSOT — merge `main` = ปล่อย ไม่มี hosting **(Recommended)**

**Answer**: 7) Other: git repo เป็น SSOT — merge `main` = ปล่อย ไม่มี hosting

---

### D5-3: Deployment Strategy
**Question**: เวอร์ชันใหม่เข้า `main` อย่างไร?
- 1) Recreate เทียบเท่า — PR merge ทับเอกสารชุดก่อน (downtime ไม่มี เพราะไม่มี runtime) **(Recommended)**
- 2) Rolling update — ไม่เข้ากับเอกสาร
- 3) Blue-green
- 4) Canary
- 5) Other (please specify): _______

**Answer**: 1) Recreate เทียบเท่า — PR merge ทับเอกสารชุดก่อน

---

### D5-4: Environments
**Question**: ต้องการ environment ไหน?
- 1) dev + production
- 2) dev + staging + production
- 3) dev + staging + production + preview (per-PR)
- 4) Other: มีแค่ `main` = production ของเอกสาร + PR เป็นช่องตรวจ **(Recommended)**

**Answer**: 4) Other: มีแค่ `main` = production ของเอกสาร + PR เป็นช่องตรวจ

---

### D5-5: Environment Promotion
**Question**: ส่งเอกสารเข้า `main` อย่างไร?
- 1) Auto-deploy ตอน push `main` (ไม่มี hosting ให้ deploy)
- 2) Auto ทุกสภาพแวดล้อม
- 3) Manual ทั้งชุด
- 4) Other: รีวิว PR แล้ว merge `main` = ปล่อย **(Recommended)** — สอดคล้อง lifecycle D3

**Answer**: 4) Other: รีวิว PR แล้ว merge `main` = ปล่อย

---

### D5-6: Secrets Management
**Question**: จัดการ credentials อย่างไร?
- 1) Platform-native — GitHub Secrets ถ้ามี workflow ในอนาคต **(Recommended)** — ตอนนี้ไม่มี secret ที่ต้องเก็บ
- 2) Cloud secret manager
- 3) HashiCorp Vault
- 4) Other: ไม่มี secrets **(ใช้ได้ถ้าไม่มี CI)**

**Answer**: 1) Platform-native — GitHub Secrets ถ้ามี workflow ในอนาคต (ตอนนี้ไม่มี secret)

---

### D5-7: Infrastructure as Code
**Question**: ต้อง provision infra คู่กับเอกสารไหม?
- 1) None — ไม่มีเซิร์ฟเวอร์/CDN ใน v1 **(Recommended)**
- 2) Terraform
- 3) AWS CDK (TypeScript)
- 4) Pulumi
- 5) CloudFormation / SAM
- 6) Other (please specify): _______

**Answer**: 1) None — ไม่มีเซิร์ฟเวอร์/CDN ใน v1

---

### D5-8: Rollback Strategy
**Question**: ถ้า merge เอกสารผิด กู้คืนอย่างไร?
- 1) Redeploy เวอร์ชันก่อน = `git revert` / revert PR แล้ว merge ใหม่ **(Recommended)**
- 2) Platform-native rollback (ไม่มี runtime revision)
- 3) Blue-green switch
- 4) Other (please specify): _______

**Answer**: 1) Redeploy เวอร์ชันก่อน = `git revert` / revert PR แล้ว merge ใหม่

---

### D5-9: Database Migrations
**Question**: มี schema DB ที่ต้องปล่อยคู่เอกสารไหม?
- 1) รัน migration ใน CI ก่อน deploy
- 2) รันตอนแอปสตาร์ท
- 3) DBA ทำมือ
- 4) ไม่มี database / ไม่ต้อง migrate **(Recommended)**
- 5) Other (please specify): _______

**Answer**: 4) ไม่มี database / ไม่ต้อง migrate

---

### D5-10: Post-Deploy Verification
**Question**: ตรวจว่า “ปล่อยสำเร็จ” อย่างไร?
- 1) Health check `/health` — ไม่มี runtime
- 2) Smoke tests บน environment ที่ deploy
- 3) Full E2E
- 4) Traffic monitoring
- 5) Other: checklist review properties บน PR + ไฟล์ SSOT เปิดได้หลัง merge **(Recommended)**

**Answer**: 5) Other: checklist review properties บน PR + ไฟล์ SSOT เปิดได้หลัง merge

---

## Decisions Summary
<!-- Machine-readable compact summary. Downstream phases: read ONLY this section. -->
- D5-1 CI/CD Platform: GitHub repo + PR review only — no workflow file
- D5-2 Deployment Target: git repo SSOT — merge `main` = release, no hosting
- D5-3 Deployment Strategy: recreate-equivalent via PR merge
- D5-4 Environments: `main` only (PR = review channel)
- D5-5 Environment Promotion: PR review then merge `main`
- D5-6 Secrets Management: GitHub Secrets if needed later — none today
- D5-7 Infrastructure as Code: None
- D5-8 Rollback Strategy: `git revert` / revert PR then merge
- D5-9 Database Migrations: none
- D5-10 Post-Deploy Verification: PR review properties + SSOT files readable after merge

---

**Instructions**: Fill in your answers above and respond with "done"
