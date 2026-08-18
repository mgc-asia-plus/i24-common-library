# Footer — "Powered by i24"

> 🔒 **มาตรฐานบังคับ (required)** — ทุกระบบ/โปรเจกต์ที่มี UI (SSR หรือ frontend) **ต้อง** แสดง footer นี้ทุกหน้า

## Purpose
แสดงเครดิตแบรนด์ท้ายทุกหน้า ("Powered by" + โลโก้ i24) เพื่ออัตลักษณ์ที่สม่ำเสมอทุกระบบ

## ขอบเขตการบังคับ
| ประเภท | บังคับ? |
|--------|---------|
| Go monolith (SSR), Next.js (frontend) และระบบที่มี UI | ✅ ต้องมีทุกหน้า |
| Backend API ล้วน (Nest.js/Express.js ที่ไม่มีหน้าเว็บ) | ไม่บังคับ (ไม่มี UI) |

## Anatomy
```
──────────────────────────────
        Powered by  [i24 logo]
──────────────────────────────
```
- ข้อความ "Powered by" (`color-text-muted`)
- โลโก้ i24 (asset ทางการ) สูงประมาณ 20–24px
- เส้นคั่นบน (`color-border`) + พื้น `color-surface`
- วางกลาง (หรือชิดขวาได้ตาม layout) ท้ายทุกหน้า

## Variants
| Variant | ใช้เมื่อ |
|---------|----------|
| `minimal` (default) | "Powered by" + โลโก้ เท่านั้น |
| `with-meta` | เพิ่มบรรทัดรอง เช่น เวอร์ชัน / ปีลิขสิทธิ์ ใต้เครดิต |

## Tokens used
`color-surface`, `color-border`, `color-text-muted`, `space-6`

## โลโก้ (asset)
- ใช้ไฟล์โลโก้ทางการ **SVG** (`i24_LOGO.svg`) เพื่อคมทุกจอ (มี PNG `i24_LOGO.png` เป็น fallback)
- แต่ละ stack วางโลโก้เป็น static asset ของตัวเอง:
  - Go monolith: `internal/template/static/i24_LOGO.svg` (`go:embed`)
  - Next.js: `public/i24_LOGO.svg`
- ในไลบรารีนี้ asset อ้างอิงคือ `i24_LOGO.svg` ที่ root (ใช้ใน `prototype/index.html`)

## Accessibility
- โลโก้ต้องมี `alt="i24"` (ไม่ปล่อยว่าง เพราะสื่อความหมายแบรนด์)
- ถ้าโลโก้ลิงก์กลับเว็บหลัก i24 ใช้ `<a>` + `aria-label`
- คง contrast ของข้อความ "Powered by" บนพื้น footer ให้ผ่าน (ใช้ `color-text-muted` บน `color-surface`)
- อยู่ใน `<footer>` (landmark) — ต่อหน้า 1 อัน

## Reference snippet
HTML / Go template (partial กลาง `partials/footer`):
```html
<footer class="border-t border-[--color-border] bg-[--color-surface]">
  <div class="mx-auto max-w-[1040px] px-6 py-6 flex items-center justify-center gap-2 text-sm text-[--color-text-muted]">
    <span>Powered by</span>
    <img src="/static/i24_LOGO.svg" alt="i24" class="h-[22px] w-auto" />
  </div>
</footer>
```
React (Next.js) — วางใน root layout ให้ติดทุกหน้า:
```tsx
export function PoweredByFooter() {
  return (
    <footer className="border-t border-[--color-border] bg-[--color-surface]">
      <div className="mx-auto max-w-[1040px] px-6 py-6 flex items-center justify-center gap-2 text-sm text-[--color-text-muted]">
        <span>Powered by</span>
        <img src="/i24_LOGO.svg" alt="i24" className="h-[22px] w-auto" />
      </div>
    </footer>
  );
}
```

## Definition of done
- [ ] footer แสดงทุกหน้า (วางใน layout กลาง ไม่ใช่ต่อหน้า)
- [ ] โลโก้ i24 asset ทางการ + `alt="i24"`
- [ ] ใช้ semantic token (ไม่ hardcode สี)
