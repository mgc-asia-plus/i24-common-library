# Brand Palette — Luxury Clear Glass

> **SSOT ของสี** — sync จาก `prototype/index.html` (ธีม Luxury Clear Glass)
>
> ระบบสี: **primary = แดง (แบรนด์)** · **accent = navy** · **neutral = slate/charcoal** · **surface = clear glass** · **status text = gold**

## ที่มา / มติ
- **แดง** = สีแบรนด์จาก `i24_LOGO.svg` (`#EC2129` ✅)
- **navy / slate / gold** = สีของ design system (ไม่ได้มาจากโลโก้) เลือกเพื่อลุค luxury
- ⚠️ **coral จากโลโก้ (`#F48569`) ถูกถอดออกจาก palette ที่ใช้งาน** — เหลือเฉพาะในตัวโลโก้เอง (ไม่ใช้เป็น accent อีกต่อไป)

## Brand red (primary)
| Token | Hex | ที่มา | ใช้กับ |
|-------|-----|-------|--------|
| `red-500` | `#EC2129` | ✅ โลโก้ | สีหลักแบรนด์, primary |
| `red-600` | `#B0141B` | derived | hover/active |
| `red-700` | `#7E0E14` | derived | เข้มสุด |

## Navy (accent)
| Token | Hex | ใช้กับ |
|-------|-----|--------|
| `navy-400` | `#2E4EA6` | focus ring, accent อ่อน |
| `navy-500` | `#1E3A8A` | accent หลัก, info |
| `navy-600` | `#152C63` | accent เข้ม / gradient end |

## Neutrals (slate / charcoal)
| Token | Hex | ใช้กับ |
|-------|-----|--------|
| `ink-900` | `#1A1D24` | ข้อความหลัก (light) |
| `ink-700` | `#333A46` | หัวข้อรอง |
| `ink-500` | `#6B7482` | ข้อความรอง / muted |
| `ink-300` | `#D2D7DF` | border, divider |
| `black`   | `#0A0C11` | พื้น (dark), ink สุด |
| `white`   | `#FFFFFF` | ตัวอักษรบนสี, พื้น glass |
| `page-bg` | `#EEF0F4` (light) / `#0A0C11` (dark) | พื้นหลังหน้า |

## Gold (status accent)
| Token | Light | Dark | ใช้กับ |
|-------|-------|------|--------|
| `gold` | `#A8811C` | `#E7C873` | ตัวอักษร status ในตาราง / เน้นหรูหรา |

## Status colors
| Token | Light | Dark |
|-------|-------|------|
| `danger`  | `#C1121F` | `#F1616B` |
| `success` | `#137A47` | `#3BB273` |
| `warning` | `#B7791F` | `#D6A24A` |
| `info`    | `#1E3A8A` | `#7C93E0` |

## Gradients
| Token | ค่า | ใช้กับ |
|-------|-----|--------|
| `grad-brand` | `linear-gradient(135deg, #E11D27 0%, #A81319 100%)` | ปุ่ม primary, โลโก้, badge brand |
| `grad-accent` | `linear-gradient(135deg, #2A4AA0 0%, #152C63 100%)` | ปุ่ม accent, badge accent |
| `grad-brand-soft` | light: `rgba(225,29,39,.06) → rgba(30,58,138,.08)` · dark: `rgba(236,33,41,.12) → rgba(46,78,166,.16)` | hover เบา, chip |

> gradient ใช้กับ **element** เท่านั้น — ห้ามใช้กับพื้นหลังหน้า/ตัวหนังสือ. glass/effect ดู [`effects.md`](effects.md)

## Contrast (คำนวณจากค่าจริง)
| คู่สี | อัตราส่วน | ผ่าน |
|-------|-----------|------|
| `white` บน `red-500 #EC2129` | ≈ 4.4:1 | ✅ ปุ่ม/text ใหญ่ · ⚠️ borderline text เล็ก |
| `white` บน grad-brand start `#E11D27` | ≈ 4.8:1 | ✅ ผ่าน AA normal |
| `white` บน grad-brand end `#A81319` | ≈ 7.6:1 | ✅ |
| `white` บน `navy-500 #1E3A8A` | ≈ 10:1 | ✅ |
| `gold #A8811C` (light) บนพื้น glass สว่าง | ≈ 3.6:1 | ⚠️ **ต่ำกว่า AA 4.5 สำหรับ text เล็ก** |

> ⚠️ **gold บน light**: ใช้กับ text หนา/ใหญ่ หรือทำให้เข้มขึ้น (เช่น `#8A6A15`) เมื่อเป็น text เล็ก; การยืนยัน a11y เต็มต้องทดสอบด้วยเครื่องมือ + assistive tech
