# Toast Notification

## Purpose
การ์ดแจ้งผลลัพธ์สั้น ๆ หลังทำรายการ (สำเร็จ / ล้มเหลว / เตือน / ข้อมูล) ลอยมุมจอ หายเอง (auto-dismiss) ไม่ขวางงานหลัก  
พื้นผิวใช้สูตร `surface-white-glass` จาก [`../brand/effects.md`](../brand/effects.md) — ห้ามคิด blur / opacity เอง

## Anatomy
```
viewport ──────────────────────┐
│                    ┌─ toast ┐│
│                    │ ● text ✕││  ← bottom-right
│                    └────────┘│
└──────────────────────────────┘
```
1. **Container** — `position: fixed`; มุมขวาล่าง; live region
2. **Toast item** — การ์ด `surface-white-glass`
3. **Status indicator** — จุดสีตาม variant (ใช้ semantic token ไม่ใช้ hex อิสระ)
4. **Message** — ข้อความกระชับ
5. **Close** — ปุ่มปิดก่อนเวลา (ถ้ามี)

## Variants
| Variant | เมื่อไหร่ที่ใช้ | สีจุดสถานะ |
|---------|----------------|-------------|
| `success` | บันทึก/ส่งสำเร็จ | `color-success` (`#137A47` light / `#3BB273` dark) |
| `danger` / `error` | ล้มเหลว หรือต้องแก้ทันที | `color-danger` (`#B0141B`) |
| `warning` | เตือนแต่ไปต่อได้ | `color-warning` (`#B7791F` light / `#D6A24A` dark) |
| `info` (default) | สถานะทั่วไป | `color-primary` / `--i24-primary` (`#0F172A`) |

ห้ามใช้เขียว/amber จาก utility อื่น — จุดสถานะต้องเป็น `color-success` / `color-warning` / `color-danger` / `color-primary` ใน [`../brand/design-tokens.md`](../brand/design-tokens.md) เท่านั้น.

## Sizes
| Size | การ์ด | ปุ่มปิด | ใช้เมื่อ |
|------|-------|---------|---------|
| `md` (default) | กว้าง `320px–400px`; ข้อความบรรทัดเดียว/สองบรรทัด | **40×40px** | ทั่วไป |
| `compact` | กว้างขั้นต่ำพอข้อความ; ยังสูงพอแตะปิด | **40×40px** | ซ้อนหลายใบ |

ทรงแคปซูล `radius-pill` **9999px** (หรือ `radius-card` **20px** ถ้าข้อความหลายบรรทัด). Auto-dismiss แนะนำ **4000ms** (พฤติกรรม ไม่ใช่ token).

## States
| State | พฤติกรรม |
|-------|----------|
| `default` | มองเห็นใน live region; นับถอยหลัง dismiss |
| `hover` | ชะลอ/พักตัวจับเวลาเมื่อชี้การ์ด; ปุ่มปิดเปลี่ยนสี `color-text` |
| `focus` / `focus-visible` | วงแหวนบนปุ่มปิด (`color-focus-ring` = `color-primary` / `--i24-primary` `#0F172A`) |
| `active` | กดปุ่มปิด — เริ่ม exit |
| `disabled` | ไม่ใช้กับการ์ดทั้งใบ; ปุ่มปิดที่กดไม่ได้ต้อง `disabled` ถ้ากำลังลบออกจาก DOM |
| `exiting` | ออกจากจอแล้วถอดโหนด; อย่าประกาศซ้ำใน live region |

## Tokens used
- `color-surface` — พื้นการ์ด สูตร `surface-white-glass` (blur **24px**)
- `color-success` (`#137A47` / `#3BB273`) — จุด success
- `color-danger` (`#B0141B`) — จุด error
- `color-warning` (`#B7791F` / `#D6A24A`) — จุด warning
- `color-primary` / `--i24-primary` (`#0F172A`) — จุด info + focus ring
- `color-on-primary` (`#FFFFFF`) — ไม่ใช้ตัวหนังสือบนจุด; ใช้บนปุ่มถ้ามีแอ็กชัน Navy
- `color-text` (`#1A1A1A` / `#F3F4F6`) · `color-text-muted` (`#6B7280` / `#9CA3AF`)
- `color-focus-ring` — ใช้ค่า `color-primary` / `--i24-primary` (`#0F172A`)
- `radius-pill` **9999px** · `radius-card` **20px**
- `font-sans`

อ้างสูตร `surface-white-glass` ใน [`../brand/effects.md`](../brand/effects.md).  
`prefers-reduced-transparency` / fallback ทึบ — ตาม effects.

## Accessibility
- **Live region**: container มี `aria-live="polite"` และ `aria-atomic="true"` สำหรับ success / info / warning
- **Error สำคัญ**: ใช้ `role="alert"` หรือ `aria-live="assertive"` — ไม่ใช้ polite อย่างเดียวถ้าผู้ใช้ต้องรู้ทันที
- **Role**: การ์ดไม่ใช้ `role="dialog"` (ไม่ดึงโฟกัส); โฟกัสคงอยู่ที่งานหลัก
- **Keyboard**: ปุ่มปิดโฟกัสได้ด้วย `Tab`; `Enter` / `Space` ปิด
- **Touch**: ปุ่มปิด ≥ **40×40px**
- **Focus ที่มองเห็น**: `focus-visible` บนปุ่มปิด
- Auto-dismiss ต้องมีปุ่มปิดด้วย — อย่าพึ่งเวลาอย่างเดียว (WCAG 2.2.1)

## Reference snippet
```html
<div id="i24-toasts" class="i24-toast-container" aria-live="polite" aria-atomic="true">
  <div class="surface-white-glass i24-toast" data-variant="info">
    <span class="i24-toast-dot" aria-hidden="true"></span>
    <p>บันทึกข้อมูลเรียบร้อย</p>
    <button type="button" class="i24-toast-close" aria-label="ปิดการแจ้งเตือน">✕</button>
  </div>
</div>
```
HTML สั้น — ไม่ใส่ JS manager / template ครบชุดต่อ stack. Error ใช้ `role="alert"` บนใบนั้นแทน polite.
