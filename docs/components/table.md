# Table

## Purpose
แสดงข้อมูลเชิงแถว/คอลัมน์ พร้อมหัวตาราง, สถานะว่าง, และ footer (pagination/summary)

## Anatomy
```
┌ Toolbar (search / filter / action) ┐  ← optional
├ Head: คอลัมน์ (sortable?)          ┤
│ Rows: ข้อมูล (zebra?)              │
├ Footer: pagination / นับรวม        ┤
└ Empty / Loading state              ┘
```

## Variants
- `default` เส้น divider แนวนอน
- `zebra` สลับสีแถว (`color-surface`)
- `compact` padding แถวลด (`sm`)

## States
- **row hover**: พื้น `color-surface`
- **selected row**: พื้น `brand-red-50` + checkbox
- **sortable header**: มีไอคอนทิศ + `aria-sort`
- **loading**: skeleton หรือ overlay + `aria-busy`
- **empty**: ข้อความ + (optional) ปุ่ม action ให้เริ่ม
- **error**: ข้อความ error + ปุ่มลองใหม่

## Tokens used
`color-bg`, `color-surface`, `color-border`, `color-text`, `color-text-muted`, `brand-red-50`, `space-3/4`, `text-sm`, `radius-md`

## Accessibility
- ใช้ `<table>` semantics จริง: `<thead>/<tbody>`, `<th scope="col|row">`
- sortable: ปุ่มใน `<th>` + `aria-sort="ascending|descending|none"`
- caption/`aria-label` อธิบายตาราง
- อย่าใช้ table เพื่อ layout

## Pattern: server-side table (Go + HTMX)
- แถว/หน้าถูก render เป็น partial; ปุ่มเปลี่ยนหน้า/sort ยิง `hx-get` มาที่ `/{resource}/table` แล้ว swap `<tbody>` หรือทั้งบล็อก
- footer นับรวม + ปุ่ม prev/next เป็น partial เดียวกัน

## Reference snippet
```html
<table class="w-full text-sm text-[--color-text]">
  <thead class="text-[--color-text-muted] border-b border-[--color-border]">
    <tr><th scope="col" class="text-left py-3">เลขที่</th><th scope="col" class="text-left">สถานะ</th></tr>
  </thead>
  <tbody hx-target="this">
    <tr class="border-b border-[--color-border] hover:bg-[--color-surface]">
      <td class="py-3">INV-001</td><td>...</td>
    </tr>
  </tbody>
</table>
```
