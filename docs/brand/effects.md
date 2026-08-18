# Effects — Gradient & Glass (Modern UI)

มาตรฐานลุค modern ของ i24: **gradient แบรนด์** + **glass (glassmorphism สไตล์ Apple)**
> อ้างอิงจริงดูได้ที่ `prototype/index.html`

## หลักการ (สำคัญ)
- **Gradient ใช้กับ "องค์ประกอบ" ไม่ใช้กับ "พื้นหลังหน้า" และ "ตัวหนังสือ"**
  - ✅ ปุ่ม primary, โลโก้, badge เน้น, ไอคอน accent
  - ❌ พื้นหลังหน้า (page background), ❌ ข้อความ (gradient text)
- **พื้นหลังหน้า**: ใช้โทน neutral/เย็น + ambient glow จาง ๆ (ไม่ปนแดง) เพื่อความลึก
- **Glass**: ใช้กับ panel/card/nav/footer/ปุ่มรอง — โปร่งแสง + เบลอฉากหลัง + ขอบ hairline + inner highlight
- ต้องคง **contrast ของข้อความ** และมี **fallback** เมื่อเบราว์เซอร์ไม่รองรับ

## Gradient tokens
| Token | ค่า | ใช้กับ |
|-------|-----|--------|
| `grad-brand` | `linear-gradient(135deg, #EC2129 0%, #F4574B 45%, #F48569 100%)` | ปุ่ม primary, โลโก้, badge เน้น |
| `grad-brand-soft` | `linear-gradient(135deg, rgba(236,33,41,.14), rgba(244,133,105,.14))` | hover เบา, chip accent |

## Glass tokens (theme-aware)
| Token | Light | Dark |
|-------|-------|------|
| `glass-bg` | `rgba(255,255,255,.55)` | `rgba(255,255,255,.06)` |
| `glass-bg-strong` | `rgba(255,255,255,.72)` | `rgba(255,255,255,.10)` |
| `glass-border` | `rgba(255,255,255,.70)` | `rgba(255,255,255,.14)` |
| `glass-hairline` | `rgba(20,20,24,.08)` | `rgba(255,255,255,.10)` |
| `glass-shadow` | `0 8px 32px rgba(31,20,20,.12), inset 0 1px 0 rgba(255,255,255,.6)` | `0 8px 32px rgba(0,0,0,.5), inset 0 1px 0 rgba(255,255,255,.10)` |
| `glass-blur` | `22px` (saturate 160%) | `22px` |

> ข้อความหนา ๆ ให้ใช้ `glass-bg-strong` (ทึบขึ้น) เพื่อ contrast

## Ambient background (page)
โทน neutral เย็น (ไม่ปนแดง) — blob เบลอ 3 จุดหลังเนื้อหา
| Token | Light | Dark |
|-------|-------|------|
| `page-bg` | `#f4f5f8` | `#0a0a0f` |
| `blob-1` | `rgba(99,110,150,.16)` | `rgba(80,92,140,.30)` |
| `blob-2` | `rgba(120,140,175,.14)` | `rgba(70,95,145,.24)` |
| `blob-3` | `rgba(120,90,220,.10)` | `rgba(95,120,235,.22)` |

## Glass recipe (CSS)
```css
.glass {
  background: var(--glass-bg);
  backdrop-filter: blur(22px) saturate(160%);
  -webkit-backdrop-filter: blur(22px) saturate(160%);
  border: 1px solid var(--glass-border);
  box-shadow: var(--glass-shadow);
  border-radius: 20px;
}
/* fallback: เบราว์เซอร์ที่ไม่รองรับ backdrop-filter → ใช้พื้นทึบ */
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .glass { background: var(--color-surface); }
}
```

## Gradient button recipe
```css
.btn-primary {
  background: var(--grad-brand); color:#fff;
  box-shadow: 0 8px 22px rgba(236,33,41,.42);
}
.btn-primary:hover { box-shadow: 0 12px 30px rgba(236,33,41,.55); transform: translateY(-1px); }
```

## Accessibility (สำคัญ)
- **Contrast**: ข้อความบน glass ต้องผ่าน WCAG AA — ถ้าไม่ผ่านให้เพิ่มความทึบ (`glass-bg-strong`) หรือใช้พื้นทึบ
- **prefers-reduced-transparency**: ผู้ใช้ที่ตั้งค่าลดความโปร่งใส → ให้ fallback เป็นพื้นทึบ
  ```css
  @media (prefers-reduced-transparency: reduce) {
    .glass { background: var(--color-surface); backdrop-filter: none; -webkit-backdrop-filter: none; }
  }
  ```
- **prefers-reduced-motion**: ถ้ามี animation ของ blob/hover ให้ปิดเมื่อผู้ใช้ตั้งค่าลดการเคลื่อนไหว
- **ไม่พึ่ง gradient สื่อความหมาย**: gradient เป็นการตกแต่ง สถานะยังต้องมีข้อความ/ไอคอน
- การยืนยัน a11y เต็มต้องทดสอบด้วยเครื่องมือ + assistive tech

## Performance
- จำกัดจำนวน element ที่ใช้ `backdrop-filter` (แพงต่อการ render) — ใช้กับ panel หลัก ไม่ใช่ทุกชิ้นเล็ก
- blob ใช้ `filter: blur()` + `position:fixed` 1 ชั้น (`z-index:-1`) พอ
