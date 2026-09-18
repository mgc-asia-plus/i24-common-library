# Deployment Summary — common-library

**Date**: 2026-09-18T13:49:00+07:00
**CI/CD Platform**: GitHub (PR review only — no workflow file)
**Deployment Target**: git repo SSOT (`mgc-asia-plus/i24-common-library`)
**Strategy**: Recreate-equivalent via PR merge into `main`

## Pipeline

| Stage | Trigger | Actions |
|---|---|---|
| Author | สาขา `feat/` `fix/` `docs/` `chore/` | แก้เอกสารตาม `docs/conventions/git.md` |
| Review | เปิด PR เข้า `main` | checklist review properties + CHANGELOG |
| Quality | ใน PR | ไม่มี lint/CI job — ตรวจมือตาม design |
| Release (`main`) | merge PR | `main` = ปล่อย SSOT ให้ทีมอื่นอ้าง |

## Environments

| Environment | Branch | Promotion | URL |
|---|---|---|---|
| PR | feature branches | manual review | GitHub PR |
| production (docs) | `main` | merge PR | `https://github.com/mgc-asia-plus/i24-common-library` |

## Files Generated

| File | Purpose |
|---|---|
| *(none)* | ไม่สร้าง `.github/workflows/`, Docker, IaC, `.env`, หรือ scripts |

กติกาปล่อยที่มีอยู่: [`docs/conventions/git.md`](../../../docs/conventions/git.md)

## Secrets Required

| Secret | Environment | Where to Configure |
|---|---|---|
| — | — | ไม่มี secret สำหรับปล่อยเอกสาร |

## Rollback

- **Strategy**: `git revert` ของ merge commit หรือ GitHub Revert PR แล้ว merge เข้า `main`
- **Trigger**: เอกสารผิด / SSOT ใช้ไม่ได้หลัง merge
- **Recovery time**: รอบ PR (นาที–ชั่วโมง)

## Post-Deployment Checklist

- [x] ไม่ต้องตั้ง secret ใน CI (ไม่มี workflow)
- [ ] (ถ้าต้องการ) เปิด branch protection บน `main` ใน GitHub org — ห้าม push ตรง, ต้องมี PR
- [ ] ปล่อยครั้งแรก = merge เอกสารชุดนี้เข้า `main`
- [ ] ตรวจว่า `docs/brand/`, `docs/components/`, `docs/stacks/`, `docs/scaffolding.md` เปิดได้บน `main`
- [ ] ไม่มี health check runtime — ไม่ใช้
- [ ] Runbook = `docs/conventions/git.md` + `CHANGELOG.md`
