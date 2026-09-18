# Footer — "Powered by i24"

## Purpose
แสดงเครดิตแบรนด์ท้ายทุกหน้า ("Powered by" + โลโก้ i24) เพื่ออัตลักษณ์ที่สม่ำเสมอทุกระบบ

**บังคับ (required)** — ทุกระบบ/โปรเจกต์ที่มี UI (SSR หรือ frontend) **ต้อง** แสดง footer นี้ทุกหน้า วางใน layout กลาง ไม่ใช่ต่อหน้า  
Backend API ล้วน (ไม่มีหน้าเว็บ) ไม่บังคับ

## Anatomy
```
──────────────────────────────
        Powered by  [i24 logo]
──────────────────────────────
```
- ข้อความ **"Powered by"** (`color-text-muted`) + โลโก้ i24 = ชุดที่ต้องมีครบ (อ่านรวมเป็น "Powered by i24")
- โลโก้ทางการ SVG `i24_LOGO.svg` (PNG `i24_LOGO.png` เป็น fallback) สูงประมาณ 20–24px
- เส้นคั่นบน `glass-hairline` (`color-border`) + พื้น `color-surface` สูตร `surface-white-glass`
- วางกลาง (หรือชิดขวาตาม layout) ภายใน `<footer>` หนึ่งอันต่อหน้า
- asset: Go `internal/template/static/i24_LOGO.svg` (`go:embed`); Next.js `public/i24_LOGO.svg`; ในไลบรารีนี้ไฟล์อ้างอิงคือ `i24_LOGO.svg` ที่ root

## Variants
| Variant | เมื่อไหร่ | visual |
|---------|----------|--------|
| `minimal` (default) | ทุกหน้าแอป | "Powered by" + โลโก้ เท่านั้น |
| `with-meta` | ต้องการเวอร์ชัน / ปีลิขสิทธิ์ | เหมือน `minimal` + บรรทัดรอง `color-text-muted` ใต้เครดิต |

ห้ามตัดข้อความ "Powered by" หรือแทนโลโก้ด้วยตัวอักษร "i24" อย่างเดียว

## Sizes
| ส่วน | ค่า |
|------|-----|
| โลโก้ | สูง 20–24px, กว้างอัตโนมัติ |
| padding แถบ | 24px (แนวตั้งและขอบ container) |
| ช่องว่างข้อความ–โลโก้ | 8px |
| ความกว้างเนื้อหาสูงสุด | ~1040px กึ่งกลาง |
| ถ้าโลโก้เป็นลิงก์ | เป้าแตะขั้นต่ำ 40×40px |

## States
| State | พฤติกรรม |
|-------|----------|
| `default` | พื้น `color-surface`; ข้อความ `color-text-muted`; โลโก้คม ไม่มี hover |
| `hover` (เมื่อโลโก้เป็นลิงก์) | โลโก้/ลิงก์ชัดขึ้นเล็กน้อย — ไม่เปลี่ยนสีข้อความเป็นแดง |
| `focus` | ถ้าโลโก้เป็น `<a>` ต้องมีวง focus ที่มองเห็น (`color-focus-ring` = `color-primary` / `#0F172A`) |
| `disabled` | ไม่ใช้กับ footer บังคับ — ต้องแสดงและโต้ตอบได้ทุกหน้าที่มี UI |

## Tokens used
| Token | บทบาท |
|-------|--------|
| `color-surface` | พื้น footer (recipe `surface-white-glass`) |
| `glass-hairline` (`color-border`) | เส้นคั่นบน |
| `color-text-muted` | ข้อความ "Powered by" และบรรทัด meta |
| `color-primary` / `--i24-primary` | วง `color-focus-ring` ของลิงก์โลโก้ (`#0F172A`) |

สูตรพื้น: `surface-white-glass` — อ้าง [`../brand/effects.md`](../brand/effects.md) ห้ามคิด blur เอง

## Accessibility
- อยู่ใน `<footer>` (landmark) — หนึ่งอันต่อหน้า
- โลโก้ต้องมี `alt="i24"` (ไม่ปล่อยว่าง เพราะสื่อความหมายแบรนด์)
- ถ้าโลโก้ลิงก์กลับเว็บหลัก i24 ใช้ `<a>` + `aria-label` (เช่น "i24"); เป้าแตะ ≥ 40×40px; Tab แล้ว Enter เปิดลิงก์
- วง focus ที่มองเห็นบนลิงก์ (`color-focus-ring` = `color-primary` / `#0F172A`)
- คง contrast ของ "Powered by": `color-text-muted` บน `color-surface` (ดู [`../brand/effects.md`](../brand/effects.md) เมื่อใช้แก้ว)

## Reference snippet
```html
<footer class="app">
  <div class="inner">
    <span>Powered by</span>
    <img src="/static/i24_LOGO.svg" alt="i24" />
  </div>
</footer>
```
วางใน layout กลางให้ติดทุกหน้า — ชุด "Powered by" + โลโก้ i24 ห้ามตัด
