# Card

## Purpose
กล่องจัดกลุ่มเนื้อหาที่เกี่ยวข้อง (สรุป, รายการ, ฟอร์มย่อย) — พื้นผิวมาตรฐานคือ **White Clear Glass ไร้ขอบ** ตามแคตตาล็อก

## Anatomy
```
┌─────────────────────────┐
│ Header (title + action?) │
├─────────────────────────┤
│ Body (เนื้อหา)           │
├─────────────────────────┤
│ Footer (action?)         │  ← optional
└─────────────────────────┘
```
- บังคับ: surface + body
- ทางเลือก: header, footer, action ในหัวการ์ด

## Variants

| Variant | เมื่อไหร่ที่ใช้ | Visual |
|---------|----------------|--------|
| `white-glass` (แนะนำ) | พื้นผิวมาตรฐาน มองทะลุพื้นหลัง | Recipe `surface-white-glass` — พื้น `color-surface`; มน `radius-card` (20px); ไร้ขอบ |
| `elevated` | การ์ดลอยบนแคนวาส | พื้น `color-bg`; เงาตาม recipe `surface-white-glass` (light) |
| `outlined` | พื้นที่มีเงาไม่เหมาะ | เส้น `color-border` / `glass-hairline`; ไม่มีเงา |
| `filled` | เน้นแยกจากพื้นหลัง | พื้น `color-surface` โดยไม่อ้าง blur เพิ่ม |

คลาสที่ล็อกของตัวแนะนำ: `.card-white-glass` / `.surface-white-glass`

Blur / opacity / เงาอ้างสูตรใน [`../brand/effects.md`](../brand/effects.md) เท่านั้น — ห้ามคิดค่าใหม่; `prefers-reduced-transparency` ตาม recipe เดียวกัน

## Sizes

| Size | Padding | Radius |
|------|---------|--------|
| `md` (default) | 24px | `radius-card` (20px) |
| `compact` | 16px | `radius-card` (20px) |

ความกว้างตาม layout แม่ — การ์ดไม่มีขนาดความสูงคงที่

## States

| State | พฤติกรรม |
|-------|----------|
| **default** | static — ไม่โต้ตอบ |
| **hover** | เฉพาะ interactive card — ใช้เงาจาก recipe `surface-white-glass` (light); `cursor: pointer` |
| **focus** | interactive card ต้องมีวงแหวน `color-focus-ring` (ค่า = `color-primary` / `--i24-primary` `#0F172A`) |
| **disabled** | interactive card ที่ปิดแล้ว — ไม่รับคลิก; `aria-disabled`; ไม่มี hover |

Interactive card ทั้งใบต้องเป็น `<a>` หรือ `<button>` (หรือมี role ที่ถูกต้อง) — ห้าม `<div onclick>`

## Tokens used
- `color-surface` — พื้น white glass (`rgba(255, 255, 255, 0.70)` light / `rgba(255, 255, 255, 0.07)` dark)
- `color-bg` — แคนวาส / elevated
- `color-border` / `glass-hairline` — outlined
- `color-text` (`#1A1A1A` / `#F3F4F6`) — หัวข้อ
- `color-text-muted` — เนื้อหารอง
- `radius-card` (20px)
- `color-focus-ring` — focus ของ interactive card (กฎร่วม SpecIndex); ค่าวงแหวน = `color-primary` / `--i24-primary` (`#0F172A`)
- Effect: `surface-white-glass` — [`../brand/effects.md`](../brand/effects.md)

ชื่อ token จาก [`../brand/design-tokens.md`](../brand/design-tokens.md)

## Accessibility
- การ์ด static: ไม่มี role พิเศษ; หัวข้อใช้ heading จริง (`h2`/`h3`)
- Interactive: ใช้ลิงก์/ปุ่ม; คีย์บอร์ด `Tab` + `Enter` / `Space`; focus `color-focus-ring`
- พื้นที่แตะของ action บนการ์ด ≥ **40×40px**
- ข้อความบนแก้วต้อง contrast ตาม [`../brand/palette.md`](../brand/palette.md); fallback ทึบเมื่อไม่รองรับ `backdrop-filter` อยู่ใน recipe

## Reference snippet
```html
<article class="card-white-glass surface-white-glass">
  <header>
    <h3>หัวข้อการ์ด</h3>
  </header>
  <p>เนื้อหาภายในการ์ดขาวใส ไร้ขอบ</p>
</article>

<a href="/detail" class="card-white-glass focus-visible:outline-2 focus-visible:outline-[--color-focus-ring]">
  การ์ดที่คลิกได้
</a>
```
