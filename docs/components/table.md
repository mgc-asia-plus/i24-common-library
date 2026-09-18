# Table

## Purpose
แสดงข้อมูลเชิงแถว/คอลัมน์ แนว Cool Slate — ตารางในการ์ดกระจกมุมโค้ง ไม่มีเส้นกรอบหนา  
ล็อกคลาส: `.mac-table` **ต้อง** อยู่ใน `.mac-table-wrap` และ wrap นั้นอยู่ใน `.mac-section`  
หัวตารางใช้ Cool Slate เท่านั้น (`color-table-header-bg` / `color-table-header-text`) — ไม่ทาสีนี้ที่แถวข้อมูล, sidebar, ปุ่ม, หรือ badge

## Anatomy
```
┌ .mac-section  (surface-white-glass, radius-card) ┐
│  ┌ .mac-table-wrap  (radius-table; ตัดขอบเมื่ออยู่ใน section) ┐ │
│  │  thead  Cool Slate                                      │ │
│  │  tbody  แถวข้อมูล / empty / loading                      │ │
│  └─────────────────────────────────────────────────────────┘ │
│  slot pagination (ดู pagination.md)                           │
└──────────────────────────────────────────────────────────────┘
```
- `.mac-section` = การ์ดหุ้ม สูตร `surface-white-glass` จาก [`../brand/effects.md`](../brand/effects.md)
- เมื่อตารางอยู่ใน `.mac-section` ให้ตัดเส้นกรอบของ wrap ออก ให้หัวตารางติดขอบการ์ด
- สถานะในคอลัมน์ใช้ badge ข้อความ + จุด (ดู [badge.md](badge.md)) — ห้ามใช้ `color-gold` ทั้งคอลัมน์

## Variants
| Variant | เมื่อไหร่ | visual |
|---------|----------|--------|
| `default` | รายการทั่วไป | เส้น divider แนวนอน `color-table-cell-border` |
| `zebra` | แถวยาว อ่านยาก | สลับพื้นแถว `color-surface` |
| `compact` | หนาแน่น / ใน card แคบ | padding แถวลด |

**หัวตาราง (Cool Slate)** — `<thead>` เท่านั้น

| Token | Light | Dark |
| :--- | :--- | :--- |
| `color-table-header-bg` | `#E2E8F0` | `rgba(255, 255, 255, 0.06)` |
| `color-table-header-text` | `#334155` | `color-text-muted` (`#9CA3AF`) |

หัวตาราง: ตัวหนา 600, ไม่ตัดบรรทัด  
Dark **ห้าม** ใช้ Cool Slate ทึบ (`color-table-header-bg` / `#E2E8F0` หรือ `color-table-header-text` / `#334155`)

**คอลัมน์สถานะ** — map ตามความหมาย ไม่ใช้ `color-gold` ทั้งคอลัมน์

| Badge | Token | Light | Dark |
| :--- | :--- | :--- | :--- |
| `success` | `color-success` | `#137A47` | `#3BB273` |
| `warning` | `color-warning` | `#B7791F` | `#D6A24A` |
| `danger` | `color-danger` | `#B0141B` | `#B0141B` |
| `muted` | `color-text-muted` | `#6B7280` | `#9CA3AF` |
| `status` (ทางเลือก) | `color-gold` | `#A8811C` | `#E7C873` |

## Sizes
| ส่วน | ค่า |
|------|-----|
| ฟอนต์เซลล์ / หัว | 13px |
| padding เซลล์ | 8px 12px (`compact` = 6px 10px) |
| มุม `.mac-table-wrap` เดี่ยว | `radius-table` (14px) |
| มุม `.mac-section` | `radius-card` (20px) |
| ปุ่มเรียง / checkbox ในตาราง | เป้าแตะขั้นต่ำ 40×40px |
| pagination (slot) | ตาม [pagination.md](pagination.md) — หน้าปัจจุบันพื้น `color-primary` / `#0F172A` ตัวอักษร `color-on-primary` / `#FFFFFF` |

เซลล์ข้อมูล: `nowrap` + `ellipsis` (ข้อความยาวใช้ clamp 2–3 บรรทัด)

## States
| State | พฤติกรรม |
|-------|----------|
| `default` | แถวพื้นโปร่ง; หัว Cool Slate; เส้น `color-table-cell-border` |
| `hover` (แถว) | พื้น `grad-table-row-hover` (สูตรใน [`../brand/effects.md`](../brand/effects.md)) |
| `selected` | `grad-table-row-hover` + checkbox ที่เลือก |
| `focus` | ปุ่มเรียง / checkbox / ลิงก์ในเซลล์มีวง focus ที่มองเห็น (`color-focus-ring` = `color-primary` / `#0F172A`) |
| `disabled` | แถวหรือ control ที่กดไม่ได้: `color-text-muted`, ไม่มี hover, `aria-disabled` / `disabled` |
| `empty` | ข้อความ `color-text-empty` / `#6E6E73` กึ่งกลาง |
| `loading` | skeleton หรือ overlay + `aria-busy="true"` บนตาราง |
| `sortable` | ไอคอนทิศใน `<th>` + `aria-sort` |

## Tokens used
| Token | บทบาท |
|-------|--------|
| `color-table-header-bg` | พื้นหัวตาราง Cool Slate |
| `color-table-header-text` | ตัวอักษรหัวตาราง |
| `color-table-cell-border` | เส้นใต้เซลล์ |
| `color-text` | ข้อความเซลล์ |
| `color-text-muted` | หัวตาราง dark / badge muted / disabled |
| `color-text-empty` | แถวว่าง |
| `color-surface` | พื้นการ์ด / zebra |
| `color-bg` | แคนวาสรอบตาราง |
| `glass-hairline` (`color-border`) | เส้นบางของ wrap เมื่อไม่อยู่ใน section |
| `grad-table-row-hover` | hover / selected แถว |
| `color-success` / `color-warning` / `color-danger` / `color-gold` | badge สถานะ |
| `color-primary` / `--i24-primary` | pagination หน้าปัจจุบัน + วง focus |
| `color-on-primary` | ตัวอักษรบน pagination ปัจจุบัน |
| `radius-table` / `radius-card` / `radius-pill` | มุม wrap / การ์ด / ปุ่มหน้า |

สูตรพื้นการ์ด: `surface-white-glass` — อ้าง [`../brand/effects.md`](../brand/effects.md) ห้ามคิด blur เอง

## Accessibility
- ใช้ `<table>` จริง: `<thead>` / `<tbody>`, `<th scope="col|row">`
- `caption` หรือ `aria-label` อธิบายตาราง
- sortable: ปุ่มใน `<th>` (ไม่ใช่ `<th>` คลิกเอง), `aria-sort="none|ascending|descending"`; Tab → Enter/Space เรียง
- checkbox / ปุ่มแถว: วง focus ที่มองเห็น (`color-focus-ring` = `color-primary` / `#0F172A`); เป้าแตะ ≥ 40×40px; Tab / Space / Enter
- สถานะ: ข้อความ + จุดสี — ห้ามสื่อความหมายด้วยสีอย่างเดียว
- `loading`: `aria-busy="true"`; `empty`: ข้อความที่อ่านได้ ไม่ใช่ตารางว่างเงียบ
- หัวตาราง light: `color-table-header-text` (`#334155`) บน `color-table-header-bg` (`#E2E8F0`) ≈ 8.4:1 (AAA)

## Reference snippet
```html
<section class="mac-section">
  <div class="mac-table-wrap">
    <table class="mac-table" aria-label="รายการใบแจ้งหนี้">
      <thead>
        <tr>
          <th scope="col">เลขที่</th>
          <th scope="col">สถานะ</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>INV-001</td>
          <td>
            <span class="mac-badge mac-badge--success">
              <span class="mac-badge-dot" aria-hidden="true"></span>ส่งแล้ว
            </span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</section>
```
