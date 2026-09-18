# Badge

## Purpose
ป้ายเล็กแสดงสถานะ หมวด หรือจำนวน (เช่น "ใหม่", "รอดำเนินการ", จำนวนแจ้งเตือน) — ทรง **Pill** ตามแคตตาล็อก

## Anatomy
```
[ (dot?)  label  (dismiss ×?) ]
```
- บังคับ: ข้อความสั้น
- ทางเลือก: จุดสีนำหน้า (`mac-badge-dot`); ปุ่มปิดเมื่อลบได้

## Variants

| Variant | เมื่อไหร่ที่ใช้ | Visual |
|---------|----------------|--------|
| `success` | สำเร็จในตาราง (`ready` / `submitted`) | พื้นโปร่ง; ข้อความ `color-success` (`#137A47` / dark `#3BB273`) + จุดสี |
| `warning` | รอ / เตือนในตาราง | พื้นโปร่ง; ข้อความ `color-warning` (`#B7791F` / dark `#D6A24A`) + จุดสี |
| `danger` | ล้มเหลวในตาราง | พื้นโปร่ง; ข้อความ `color-danger` (`#B0141B`) + จุดสี |
| `muted` | ว่าง / ไม่ทราบ / history | พื้นโปร่ง; ข้อความ `color-text-muted` |
| `status` | ป้าย luxury **ทางเลือก** — **ไม่ใช้เป็นคอลัมน์สถานะตาราง** | พื้นโปร่งหรือ `color-surface`; ข้อความ `color-gold` |
| `brand` | เน้นแบรนด์นอกตาราง | พื้น `color-danger` / `brand-red` (`#B0141B`); ข้อความ `color-on-primary` (`#FFFFFF`) |
| `accent` | tag / หมวดเด่น | พื้น `color-primary` / `--i24-primary` (`#0F172A`); ข้อความ `color-on-primary` |

ทุก variant มน `radius-badge` / `radius-pill` (9999px)

> **ตาราง (SSOT จาก i24-etax-service `.mac-badge`)**: คอลัมน์สถานะใช้ `success` / `warning` / `danger` / `muted` + จุดสี (`mac-badge-dot`) พื้นโปร่ง — ดู [`table.md`](table.md) และ [`../brand/palette.md`](../brand/palette.md) §6  
> สื่อสถานะด้วยข้อความ + จุด ไม่พึ่งสีอย่างเดียว

## Sizes

| Size | สูง | ตัวอักษร |
|------|-----|----------|
| `sm` | 18px | เล็ก (`text-xs`) |
| `md` (default) | 22px | ปกติ (`text-sm`) |

Badge เองเป็นป้าย static — ถ้ามีปุ่มปิด พื้นที่แตะของปุ่มนั้น ≥ **40×40px**

## States

| State | พฤติกรรม |
|-------|----------|
| **default** | static — ไม่โต้ตอบ |
| **focus** | ใช้เมื่อ badge คลิกได้หรือมีปุ่ม × — วงแหวน `color-focus-ring` (ค่า = `color-primary` / `--i24-primary` `#0F172A`) |
| **disabled** | ใช้เมื่อปุ่ม × / badge ที่คลิกได้ถูกปิด — ไม่รับคลิก; `aria-disabled` |

- จุดสีนำหน้าบังคับในคอลัมน์สถานะตาราง
- ปุ่ม × ต้องมี `aria-label`

## Tokens used
- `color-success` (`#137A47` / `#3BB273`)
- `color-warning` (`#B7791F` / `#D6A24A`)
- `color-danger` / `brand-red` (`#B0141B`)
- `color-text-muted` (`#6B7280` / `#9CA3AF`)
- `color-gold` (`#A8811C` / `#E7C873`)
- `color-primary` / `--i24-primary` (`#0F172A`) — accent
- `color-on-primary` (`#FFFFFF`)
- `color-surface` — พื้นทางเลือกของ `status`
- `radius-badge` / `radius-pill` (9999px)
- `color-focus-ring` — focus ของปุ่มปิด / badge ที่คลิกได้ (กฎร่วม SpecIndex); ค่าวงแหวน = `color-primary`

ชื่อ token จาก [`../brand/design-tokens.md`](../brand/design-tokens.md)

## Accessibility
- อย่าสื่อความหมายด้วยสีอย่างเดียว — ใส่ข้อความ / ไอคอน / `mac-badge-dot`
- จำนวนแจ้งเตือนบนปุ่ม: ผูก `aria-label` ที่ปุ่ม เช่น "การแจ้งเตือน 3 รายการ"
- ปุ่ม ×: คีย์บอร์ด (`Tab` + `Enter` / `Space`), `aria-label`, focus `color-focus-ring`, พื้นที่แตะ ≥ **40×40px**
- Badge static ไม่ต้องโฟกัส

## Reference snippet
```html
<!-- คอลัมน์สถานะในตาราง -->
<span class="mac-badge mac-badge--success"><span class="mac-badge-dot" aria-hidden="true"></span>ส่งแล้ว</span>
<span class="mac-badge mac-badge--warning"><span class="mac-badge-dot" aria-hidden="true"></span>รอดำเนินการ</span>
<span class="mac-badge mac-badge--danger"><span class="mac-badge-dot" aria-hidden="true"></span>ล้มเหลว</span>

<!-- ลบได้ -->
<span class="mac-badge">ใหม่
  <button type="button" class="mac-badge-dismiss" aria-label="ลบป้ายใหม่"
          style="min-width:40px;min-height:40px"></button>
</span>
```
