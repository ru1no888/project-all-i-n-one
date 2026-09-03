# 🏭 JLCPCB & PCBWAY ORDERING SPECIFICATION & PROMPT GUIDE
> **คำแนะนำ:** เอกสารนี้รวบรวมพารามิเตอร์และขั้นตอนสำหรับนำไฟล์ `SmartWatch_Carrier_v1_Gerber.zip` ไปสั่งผลิตที่โรงงาน **JLCPCB**, **PCBWay** หรือโรงงานรับทำ PCB ชั้นนำ

---

## 1. 📋 ตารางพารามิเตอร์สำหรับกรอกหน้าเว็บสั่งผลิต (Parameters Checklist)

เมื่อคุณเข้าสู่หน้าสั่งซื้อของ [JLCPCB.com](https://jlcpcb.com) หรือ [PCBWay.com](https://pcbway.com) แล้วอัปโหลดไฟล์ **`SmartWatch_Carrier_v1_Gerber.zip`** ให้เลือกตั้งค่าพารามิเตอร์ตามตารางนี้:

| หัวข้อตั้งค่า (Option Name) | ค่าที่ต้องเลือก (Selected Value) | เหตุผลทางวิศวกรรม (Engineering Rationale) |
| :--- | :---: | :--- |
| **Base Material** | **FR-4** | วัสดุมาตรฐานฉนวนใยแก้ว แข็งแรง ทนความร้อนสูง |
| **Layers** | **2 Layers** | วงจร 2 หน้า (หน้าบนขับจอ, หน้าหลัง MCU & เซนเซอร์) |
| **Dimensions** | **44 mm × 44 mm** | ขนาดทรงกลม Ø 44.0 mm (ระบบจะตรวจจับจากไฟล์ Edge_Cuts อัตโนมัติ) |
| **PCB Qty** | **5 pcs** (หรือตามต้องการ) | จำนวนเริ่มต้นขั้นต่ำที่คุ้มราคาที่สุด |
| **Different Design** | **1 Design** | มี 1 แบบวงจร |
| **Delivery Format** | **Single PCB** | ส่งมอบเป็นชิ้นเดี่ยวตัดขอบกลม |
| **PCB Thickness** | **1.0 mm** (หรือ 1.2 mm) | **แนะนำ 1.0 mm** เพื่อให้ตัวเรือนนาฬิกาบางและเบาที่สุด |
| **PCB Color (Solder Mask)** | **Matte Black** (สีดำด้าน) หรือ **Green** (สีเขียว) | สีดำด้านจะดูหรูหราเข้ากับเคสสมาร์ทวอทช์ |
| **Silkscreen Color** | **White** (สีขาว) | ตัวหนังสือสีขาวตัดกับพื้นบอร์ดสีดำ อ่านขาง่าย คมชัด |
| **Surface Finish** | **HASL Lead-Free** (หรือ **ENIG**) | • **HASL Lead-Free**: บัดกรีง่าย ไร้สารตะกั่ว ปลอดภัยต่อการสวมใส่<br>• **ENIG (ชุบทองแท้)**: ผิวเรียบเนียนระดับพรีเมียม สวยงาม ทนทานต่อเหงื่อ |
| **Outer Lead Weight** | **1 oz** (35 µm) | ความหนาทองแดงมาตรฐาน รองรับกระแสไฟได้สูงถึง 2.0A สบายๆ |
| **Via Process** | **Tenting Vias** (หรือ Untented) | เคลือบหน้ากากปิดรูเวีย ป้องกันการลัดวงจร |
| **Min Hole Size / Drill** | **0.4 mm** | รูเจาะเวียขนาด 0.40 mm และรูขาอุปกรณ์ 0.85–0.90 mm |
| **Min Track / Spacing** | **6/6 mil (0.15 mm)** | ลายเส้นของเราออกแบบไว้ที่ 0.35 mm (13.8 mil) ซึ่งผ่านเกณฑ์โรงงานแบบเหลือเฟือ |
| **Edge Connector / Gold Fingers** | **No** | ไม่มีขั้วสล็อตเสียบการ์ด |
| **Castellated Holes** | **No** | ไม่มีรูกัดขอบ |
| **Confirm Production File** | **Yes** (แนะนำ) | ให้วิศวกรโรงงานส่งภาพตรวจก่อนเริ่มตัดแผ่น |

---

## 2. 📦 รายการไฟล์ภายในชุด Gerber ZIP (`SmartWatch_Carrier_v1_Gerber.zip`)

ภายในไฟล์ ZIP ประกอบด้วยไฟล์มาตรฐาน RS-274X และ Excellon ครบถ้วน 100%:

```
SmartWatch_Carrier_v1_Gerber.zip
 ├── SmartWatch_Carrier_v1-F_Cu.gtl         [เลเยอร์ทองแดงหน้าบน - Top Copper]
 ├── SmartWatch_Carrier_v1-B_Cu.gbl         [เลเยอร์ทองแดงหน้าหลัง - Bottom Copper]
 ├── SmartWatch_Carrier_v1-F_Mask.gts       [หน้ากากโซลเดอร์มาร์กหน้าบน - Top Solder Mask]
 ├── SmartWatch_Carrier_v1-B_Mask.gbs       [หน้ากากโซลเดอร์มาร์กหน้าหลัง - Bottom Solder Mask]
 ├── SmartWatch_Carrier_v1-F_SilkS.gto      [ลายสกรีนตัวหนังสือหน้าบน - Top Silkscreen]
 ├── SmartWatch_Carrier_v1-B_SilkS.gbo      [ลายสกรีนตัวหนังสือหน้าหลัง - Bottom Silkscreen]
 ├── SmartWatch_Carrier_v1-F_Paste.gtp      [เลเยอร์แผ่นสเตนซิลหน้าบน - Top Solder Paste]
 ├── SmartWatch_Carrier_v1-B_Paste.gbp      [เลเยอร์แผ่นสเตนซิลหน้าหลัง - Bottom Solder Paste]
 ├── SmartWatch_Carrier_v1-Edge_Cuts.gm1    [เส้นขอบตัดบอร์ดวงกลม Ø 44mm - Board Outline]
 └── SmartWatch_Carrier_v1.drl              [ไฟล์พิกัดและขนาดรูเจาะสว่าน - Excellon Drill File]
```

---

## 3. 📝 ข้อความสั่งผลิตแบบข้อกำหนดภาษาอังกฤษ (English Production Note)
หากโรงงานหรือระบบขอ **"Order Remark / Production Notes"** คุณสามารถคัดลอกข้อความนี้ไปใส่ได้ทันที:

```text
Dear Engineer,
Please manufacture this 2-layer round PCB according to the following specifications:
1. Board Outline: Circular shape Ø 44.0 mm, defined on Edge.Cuts layer.
2. Thickness: 1.0 mm FR-4 (Tg 130-140°C).
3. Surface Finish: HASL Lead-Free (or ENIG if selected).
4. Copper Weight: 1 oz (35 µm) outer layers.
5. Solder Mask: Matte Black. Silkscreen: White.
6. Minimum drill size: 0.40 mm (Vias), Component lead holes: 0.85 mm - 0.90 mm.
7. Clean all drill holes and ensure accurate circular routing along Edge.Cuts.
Thank you!
```
