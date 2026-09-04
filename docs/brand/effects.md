# Effects — Clear Glass & Gradient (Luxury theme)

มาตรฐานลุค **Luxury Clear Glass** ของ i24: กระจก**ใสจริง** (blur น้อย) เคลือบเงาหลายชั้น + gradient แบรนด์/accent + พื้นหลังไล่แสงนุ่ม
> อ้างอิงจริง: `prototype/index.html`

## หลักการ
- **Clear glass** = โปร่งใส (blur ~3px) + เคลือบเงา 4 ชั้น (tint + sheen + top highlight + diagonal gloss) + เงาหลายชั้น + ขอบสว่าง — **ไม่ขุ่น** (ต่างจาก frosted)
- **Gradient ใช้กับ element** (ปุ่ม/โลโก้/badge) — **ไม่ใช้กับพื้นหลังหน้า/ตัวหนังสือ**
- **พื้นหลังหน้า** = โทน neutral + blob แสงนุ่ม (แดง/น้ำเงิน/เทา) เบลอแรง ไม่มีลายกริด
- ต้องมี **fallback** + เคารพ `prefers-reduced-transparency`

## Gradient tokens
| Token | ค่า |
|-------|-----|
| `grad-brand` | `linear-gradient(135deg, #E11D27 0%, #A81319 100%)` |
| `grad-accent` | `linear-gradient(135deg, #2A4AA0 0%, #152C63 100%)` |
| `grad-brand-soft` (light) | `linear-gradient(135deg, rgba(225,29,39,.06), rgba(30,58,138,.08))` |
| `grad-brand-soft` (dark) | `linear-gradient(135deg, rgba(236,33,41,.12), rgba(46,78,166,.16))` |

## Clear-glass tokens (theme-aware)
| Token | Light | Dark |
|-------|-------|------|
| `glass-tint` | `linear-gradient(135deg, rgba(255,255,255,.13), rgba(255,255,255,.02))` | `…(.07),(.012)` |
| `glass-sheen` | `radial-gradient(135% 95% at 15% -14%, rgba(255,255,255,.50), transparent 50%)` | `…(.18)` |
| `glass-top` | `linear-gradient(180deg, rgba(255,255,255,.38), transparent 26%)` | `…(.16)` |
| `glass-gloss` | `linear-gradient(122deg, transparent 34%, rgba(255,255,255,.42) 45%, rgba(255,255,255,.10) 52%, transparent 62%)` | `…(.18),(.04)` |
| `glass-bg` | `rgba(255,255,255,.09)` | `rgba(255,255,255,.04)` |
| `glass-bg-strong` | `rgba(255,255,255,.20)` | `rgba(255,255,255,.075)` |
| `glass-border` | `rgba(255,255,255,.60)` | `rgba(255,255,255,.16)` |
| `glass-hairline` | `rgba(20,28,50,.09)` | `rgba(255,255,255,.08)` |
| `glass-blur` | `3px` (nav `7px`) · saturate `135%` · brightness `1.04` | เท่ากัน |

`glass-shadow` (light) — เงาหลายชั้น + ขอบสว่าง:
```
0 0 0 1px rgba(20,28,50,.045),
0 1px 2px rgba(16,22,45,.05),
0 18px 42px rgba(16,22,45,.12),
inset 0 1px 0 rgba(255,255,255,.95),
inset 0 -1px 0 rgba(20,28,50,.05)
```

## Ambient background (page)
| Token | Light | Dark |
|-------|-------|------|
| `page-bg` | `#EEF0F4` | `#0A0C11` |
| `blob-red` | `rgba(225,29,39,.08)` | `rgba(236,33,41,.18)` |
| `blob-blue` | `rgba(30,58,138,.11)` | `rgba(46,78,166,.26)` |
| `blob-gray` | `rgba(90,100,125,.11)` | `rgba(70,80,105,.20)` |

## Clear-glass recipe (CSS)
```css
.glass {
  background: var(--glass-gloss), var(--glass-top), var(--glass-sheen), var(--glass-tint);
  backdrop-filter: blur(3px) saturate(135%) brightness(1.04);
  -webkit-backdrop-filter: blur(3px) saturate(135%) brightness(1.04);
  border: 1px solid var(--glass-border);
  box-shadow: var(--glass-shadow);
  border-radius: 20px;
}
/* fallback / reduced transparency */
@supports not ((backdrop-filter:blur(1px)) or (-webkit-backdrop-filter:blur(1px))) { .glass{ background:var(--glass-bg-strong);} }
@media (prefers-reduced-transparency: reduce) {
  .glass { backdrop-filter:none; -webkit-backdrop-filter:none; background:var(--glass-bg-strong); }
}
```
> ปุ่มสี (`primary`/`accent`) เพิ่ม gloss streak ด้วย `::after` overlay ขาวจาง ๆ

## Accessibility & performance
- **Contrast**: ข้อความบน glass ต้องผ่าน AA — ข้อความหนาใช้ `glass-bg-strong`; **gold บน light ≈ 3.6:1** → ใช้กับ text หนา/ใหญ่ หรือใช้เฉดเข้มขึ้น (`#8A6A15`)
- **prefers-reduced-transparency / reduced-motion**: fallback พื้นทึบ + ปิด animation blob
- **ไม่พึ่ง gradient/สีสื่อความหมาย** — สถานะต้องมีข้อความ/ไอคอน
- **Performance**: จำกัด element ที่ใช้ `backdrop-filter`; blob 1 ชั้น `position:fixed z-index:-1`
- a11y เต็มต้องทดสอบด้วยเครื่องมือ + assistive tech
