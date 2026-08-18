# Product — i24-common-library

## Summary
- **Product**: documentation-based common library ของ i24 — ชุดไฟล์ `.md` ที่อธิบายมาตรฐานกลาง (brand/สี, design tokens, component spec, convention, วิธี setup ต่อ stack)
- **Users**: นักพัฒนาภายใน (ยึดเป็น SSOT ตอนเริ่ม/พัฒนาโปรเจกต์)
- **Type / Scope**: Greenfield / new — เป็น knowledge base ไม่ใช่ code generator

## Overview
repo กลางที่เก็บ "ข้อตกลง/มาตรฐาน" ของทุกโปรเจกต์ i24 ในรูปเอกสาร Markdown ที่อ่านชัดเจน — ครอบคลุมอัตลักษณ์แบรนด์ (สีจากโลโก้ พร้อม hex code), design tokens (light/dark), spec ของแต่ละ component, convention การเขียนโค้ด และแนวทาง setup แต่ละ tech stack. เป้าหมายคือให้ทุกทีมอ่านแล้ว implement ได้เองอย่างสม่ำเสมอ โดย **ไม่ต้อง maintain code template หลายชุด** — แก้ที่เอกสารกลางที่เดียว.

## Problem Statement
การเก็บ code template ครบทุก stack ต้อง maintain หลายชุดและ drift ง่าย. ต้องการแทนที่ด้วย "เอกสารกลางที่ชัดเจน" เป็น single source of truth ของแบรนด์+มาตรฐาน ให้แต่ละทีมนำไป implement ตาม stack ของตัวเอง.

## Target Users
- **Developer เริ่มโปรเจกต์ใหม่**: อ่านเอกสารเพื่อ set up ธีม/โครง/convention ให้ตรงมาตรฐาน
- **Developer ระหว่างพัฒนา**: อ้าง component spec + token เวลาสร้าง UI
- **Maintainer ของ common**: ดูแลเอกสารกลางให้เป็นปัจจุบัน
- **Team lead**: ใช้เป็นมาตรฐานบังคับ/ตรวจ review

## Key Features (เป็นเอกสาร .md ทั้งหมด)
- **Brand & color**: สีจากโลโก้ พร้อม hex code, usage, do/don't
- **Design tokens**: color/typography/spacing/radius/shadow + semantic light/dark
- **Theme guide**: วิธี map tokens → Tailwind v4 `@theme` (สั้น ๆ พออ้างอิง)
- **Component specs**: แต่ละ component = anatomy, variants, states, tokens ที่ใช้, accessibility
- **Stack setup guides**: แนวทาง setup + convention ต่อ Go monolith / Next.js / Nest.js / Express.js
- **Conventions**: naming, project structure, git, JSON
- **Scaffolding checklist**: ขั้นตอนเริ่มโปรเจกต์ใหม่ (แทน generator อัตโนมัติ)

## Domain Language
| Term | Definition | Example |
|------|------------|---------|
| Design token | ค่าดีไซน์พื้นฐานที่ตั้งชื่อ | `brand-red-500 = #E4181E` |
| Semantic token | token ที่สื่อความหมาย map ต่อ theme | `surface`, `text-primary` (light/dark) |
| Component spec | เอกสารอธิบาย component 1 ตัว | `components/button.md` |
| Stack guide | เอกสาร setup ต่อ tech stack | `stacks/nextjs.md` |
| Scaffolding checklist | ขั้นตอนเริ่มโปรเจกต์ด้วยมือ | `scaffolding.md` |

## Brand Palette (จากไฟล์ vector ทางการ i24_LOGO.svg)
| Token | Hex | บทบาท |
|-------|------|-------|
| `brand-red-500` | `#EC2129` ✅ | สีหลักแบรนด์ (จากโลโก้) |
| `brand-red-600` | `#C81B22` | hover/active + white text เล็กบนพื้นแดง |
| `brand-red-400` | `#F04E52` | เน้นรอง / focus ring |
| `brand-red-50` | `#FDECED` | tint พื้นหลังอ่อน |
| `brand-coral-400` | `#F48569` ✅ | accent (blob โลโก้) |
| `brand-coral-300` | `#F7A48A` | accent อ่อน |
| `white` | `#FFFFFF` ✅ | ตัวอักษร/พื้น card |
| `ink-900` | `#1A1A1A` | ข้อความหลัก |
| `ink-500` | `#6B7280` | ข้อความรอง |
| `paper-muted` | `#F7F7F8` | surface |

> ✅ = ยืนยันจากโลโก้; เฉดอื่น derived. SSOT จริงอยู่ที่ `docs/brand/palette.md`

## Success Criteria
- เอกสารครบและอ่านแล้ว implement ได้เองโดยไม่ต้องถามเพิ่ม
- สี/มาตรฐานตรงกันทุกโปรเจกต์เพราะยึดเอกสารเดียว
- แก้มาตรฐานที่เอกสารกลางที่เดียว (ไม่มี code หลายชุดให้ sync)

## Constraints & Assumptions
- **Constraints**: deliverable เป็น `.md` เท่านั้น (code snippet มีได้เท่าที่จำเป็นเพื่ออธิบาย ไม่เก็บเป็น template code ครบชุด)
- **Assumptions**: ค่าสีเป็นค่าประมาณจากโลโก้ ต้องยืนยันก่อน lock; อ่านโดย developer ที่รู้ stack ของตัวเองอยู่แล้ว

## Project Type
- **Type**: Greenfield
- **Scope**: New product (documentation knowledge base)
