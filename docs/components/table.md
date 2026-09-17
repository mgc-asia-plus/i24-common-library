# Table

## Purpose
แสดงข้อมูลเชิงแถว/คอลัมน์ พร้อมหัวตาราง, สถานะว่าง, และ footer (pagination/summary)

## Anatomy
```
┌ Toolbar (search / filter / action) ┐  ← optional
├ Head: คอลัมน์ (sortable?)          ┤  ← Cool Slate header เท่านั้น
│ Rows: ข้อมูล (zebra?)              │
├ Footer: pagination / นับรวม        ┤
└ Empty / Loading state              ┘
```

## Variants
- `default` เส้น divider แนวนอน
- `zebra` สลับสีแถว (`color-surface`)
- `compact` padding แถวลด (`sm`)

## Header (Cool Slate)
ใช้กับ `<thead>` เท่านั้น — ไม่ทาสีนี้ที่แถวข้อมูล, sidebar, ปุ่ม, หรือ badge สถานะ

| Token | Light | Dark |
| :--- | :--- | :--- |
| `color-table-header-bg` | `#E2E8F0` | `rgba(255, 255, 255, 0.06)` |
| `color-table-header-text` | `#334155` | `color-text-muted` (`#9CA3AF`) |

ค่า hex SSOT ที่ [`../brand/palette.md`](../brand/palette.md) · semantic ที่ [`../brand/design-tokens.md`](../brand/design-tokens.md)  
Dark **ห้าม** ใช้ Cool Slate ทึบ (`#E2E8F0` / `#334155`)

## Status column (จาก i24-etax-service)
ใช้ badge **ข้อความ + จุด** พื้นโปร่ง — map ตามความหมาย ไม่ใช้ `status` (gold) ทั้งคอลัมน์

| Variant | Light | Dark | ตัวอย่างค่า |
| :--- | :--- | :--- | :--- |
| `success` | `#137A47` | `#3BB273` | `ready`, `submitted`, `success`, `imported` |
| `warning` | `#B7791F` | `#D6A24A` | `pending`, `prepare`, `new`, `failed_retry`, `[transient]` |
| `danger` | `#B0141B` | `#B0141B` | `failed`, `error`, `invalid`, `[permanent]` |
| `muted` | `#6B7280` | `#9CA3AF` | ว่าง, ไม่ทราบ, `history` |

อ้างอิง implementation: `i24-etax-service/internal/helpers/admintable/cell.go` · สเปก badge [`badge.md`](badge.md)

## States
- **row hover**: พื้น `grad-brand-soft` (tint จาง) หรือ `color-surface`
- **selected row**: พื้น `grad-brand-soft` + checkbox
- **status column**: `success` / `warning` / `danger` / `muted` ตามตารางด้านบน
- **sortable header**: มีไอคอนทิศ + `aria-sort`
- **loading**: skeleton หรือ overlay + `aria-busy`
- **empty**: ข้อความ + (optional) ปุ่ม action ให้เริ่ม
- **error**: ข้อความ error + ปุ่มลองใหม่

## Tokens used
`color-table-header-bg`, `color-table-header-text`, `color-success`, `color-warning`, `color-danger`, `color-text-muted`, `color-bg`, `color-surface`, `color-border`, `color-text`, `grad-brand-soft`, `glass-hairline`, `space-3/4`, `text-sm`, `radius-md`

## Accessibility
- ใช้ `<table>` semantics จริง: `<thead>/<tbody>`, `<th scope="col|row">`
- sortable: ปุ่มใน `<th>` + `aria-sort="ascending|descending|none"`
- caption/`aria-label` อธิบายตาราง
- อย่าใช้ table เพื่อ layout
- หัวตาราง light: `#334155` บน `#E2E8F0` ≈ 8.4:1 (AAA)
- สถานะ: ใส่ข้อความ + จุดสี — ห้ามสื่อความหมายด้วยสีอย่างเดียว

## Pattern: server-side table (Go + HTMX)
- แถว/หน้าถูก render เป็น partial; ปุ่มเปลี่ยนหน้า/sort ยิง `hx-get` มาที่ `/{resource}/table` แล้ว swap `<tbody>` หรือทั้งบล็อก
- footer นับรวม + ปุ่ม prev/next เป็น partial เดียวกัน

## Reference snippet
```html
<table class="w-full text-sm text-[--color-text]">
  <thead class="bg-[--color-table-header-bg] text-[--color-table-header-text]">
    <tr><th scope="col" class="text-left py-3">เลขที่</th><th scope="col" class="text-left">สถานะ</th></tr>
  </thead>
  <tbody hx-target="this">
    <tr class="border-b border-[--color-border] hover:bg-[--color-surface]">
      <td class="py-3">INV-001</td>
      <td><span class="mac-badge mac-badge--success"><span class="mac-badge-dot" aria-hidden="true"></span>ส่งแล้ว</span></td>
    </tr>
  </tbody>
</table>
```
