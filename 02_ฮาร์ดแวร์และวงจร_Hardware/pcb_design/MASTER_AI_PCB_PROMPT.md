# 🤖 MASTER AI PCB PROMPT: SMARTWATCH CARRIER BOARD v1.0
> **คำแนะนำ:** คุณสามารถคัดลอกข้อความด้านล่างนี้ทั้งหมด นำไปวางในช่องแชทของ AI (ChatGPT, Claude, Gemini, Antigravity) เพื่อให้ AI สร้างหรือปรับปรุงไฟล์ KiCad, Gerber, PDF และโค้ดวงจรนี้ใหม่ได้ทันที 100% โดยไม่มีข้อผิดพลาด

```markdown
คุณคือวิศวกรผู้เชี่ยวชาญด้านการออกแบบวงจรพิมพ์ (Hardware & PCB Design Engineer) ระดับสูง
โปรดช่วยฉันออกแบบและสร้างไฟล์ PCB สำหรับโปรเจกต์ "SmartWatch Carrier Board v1.0" บน KiCad โดยยึดตามข้อกำหนดทางวิศวกรรมและพิกัดเรขาคณิตขั้นสูงดังต่อไปนี้อย่างเคร่งครัด:

---

### 1. ข้อมูลภาพรวมและข้อกำหนดเชิงกล (Mechanical Constraints)
1. รูปร่างบอร์ด: แผ่น PCB ทรงกลม ขนาดเส้นผ่านศูนย์กลาง Ø 44.0 mm (รัศมี R = 22.0 mm) จุดกึ่งกลางบอร์ดอยู่ที่พิกัด (X = 100.0 mm, Y = 100.0 mm) บนเลเยอร์ Edge.Cuts
2. เลเยอร์บอร์ด: PCB 2 เลเยอร์ (Top Layer: F.Cu และ Bottom Layer: B.Cu), เนื้อแผ่น FR-4 หนา 1.0 mm (เพื่อความบางสำหรับใส่นาฬิกา), ทองแดงหนา 1 oz (35 µm)
3. กฎความปลอดภัยของขอบบอร์ด (Strict Keep-In DRC Rule):
   - ขาอุปกรณ์ (Pads), รูเจาะ (Drills), ลายเส้นทองแดง (Tracks) และรูเวีย (Vias) ทั้งหมดจะต้องอยู่ภายในรัศมีปลอดภัย:
     $$\sqrt{(X - 100.0)^2 + (Y - 100.0)^2} \le 19.2\text{ mm}$$
   - รับประกันว่าทุกชิ้นส่วนจะอยู่ห่างจากขอบวงกลมจริงอย่างน้อย 2.8 mm ห้ามมีส่วนใดยื่นหลุดขอบเด็ดขาด (Zero Edge Protrusion)
4. พื้นที่เว้นว่างเสาอากาศ (Antenna Keep-Out Zone):
   - สี่เหลี่ยมผืนผ้าด้านบนกึ่งกลาง (X = 93.5 ถึง 106.5 mm, Y = 81.5 ถึง 85.5 mm)
   - ห้ามวางชิ้นส่วน ห้ามลากลายเส้น และห้ามเททองแดง (No Copper Fill) ทั้ง 2 ด้าน เพื่อให้เสาอากาศ 2.4GHz Wi-Fi/BLE ของ ESP32 ทำงานได้เต็มประสิทธิภาพ
5. สถาปัตยกรรมแยก 2 หน้า (Dual-Sided Component Placement):
   - หน้าบน (Top Layer: F.Cu): ติดตั้งเฉพาะขั้วต่อหน้าจอ GC9A01 Round TFT 7 ขา (1x7 Header) ที่แนวแกน Y = 106.5 mm
   - หน้าหลัง (Bottom Layer: B.Cu): ติดตั้งบอร์ด MCU (XIAO ESP32-C3), เซนเซอร์ MPU6050, ขั้วต่อเซนเซอร์ชีพจร Pulse Express, วงจรขับบัซเซอร์, วงจรแบ่งแรงดันวัดแบตเตอรี่ และแถบควบคุมพลังงาน (สวิตช์/ฟิวส์/ขั้วแบต)

---

### 2. รายการอุปกรณ์ พิกัดตำแหน่ง และฟุตพริ้นท์ (Component Footprint Mapping)
จัดวางอุปกรณ์ทุกตัวบน Bottom Layer (B.Cu) ยกเว้น DISP1 ดังนี้:
1. U1 (Seeed Studio XIAO ESP32-C3):
   - ซ็อคเก็ตตัวเมีย 1x7 สองแถว ระยะห่างแถว 15.4 mm วางกึ่งกลางที่ (X = 100.0 mm, Y = 95.0 mm)
   - แถวซ้าย (X = 92.3 mm, Y = 87.38 ถึง 102.62 mm): ขา 1=D0, 2=D1, 3=D2, 4=D3, 5=D4, 6=D5, 7=D6
   - แถวขวา (X = 107.7 mm, Y = 87.38 ถึง 102.62 mm): ขา 14=5V, 13=GND, 12=3V3, 11=D10, 10=D9, 9=D8, 8=D7
2. DISP1 (GC9A01 240x240 Round TFT 7-Pin):
   - อยู่หน้าบน (F.Cu) ที่ตำแหน่ง (X = 100.0 mm, Y = 106.5 mm)
   - ขา 1=3V3, 2=GND, 3=SCK, 4=MOSI, 5=DC, 6=GND/CS, 7=RST (ระยะ Pitch 2.54 mm)
3. U3 (MPU6050 6-Axis Fall Detection Sensor):
   - ขั้วต่อตัวเมีย 1x8 (2.54mm Pitch) วางแนวตั้งทางฝั่งซ้ายที่ (X = 86.0 mm, Y = 96.0 mm)
   - ขา 1=3V3, 2=GND, 3=SCL, 4=SDA, 5=NC, 6=NC, 7=GND, 8=NC (ห่างจาก MCU 6.3 mm)
4. U2_CONN (SparkFun Pulse Express MAX32664D/MAX30102):
   - ขั้วต่อ JST-SH 1.0mm 6-Pin SMD แนวตั้ง วางทางฝั่งขวาที่ (X = 114.0 mm, Y = 96.0 mm)
   - ขา 1=5V_SYS, 2=GND, 3=I2C_SDA, 4=I2C_SCL, 5=HUB_MFIO, 6=HUB_RESET (ห่างจาก MCU 6.3 mm)
5. วงจรขับบัซเซอร์ (Buzzer Driver Zone - มุมบนซ้าย):
   - BZ1 (Active Buzzer 3.3V 9x5.5mm): วางที่ (X = 90.0 mm, Y = 85.5 mm) รูเจาะ Lead Pitch 3.6 mm
   - Q1 (S8050 NPN Transistor): ฟุตพริ้นท์ SOT-23 SMD วางที่ (X = 94.0 mm, Y = 86.0 mm)
   - R3 (ตัวต้านทาน 1kΩ 0805 SMD): วางที่ (X = 94.0 mm, Y = 89.5 mm)
   - R4 (ตัวต้านทาน 100kΩ 0805 SMD): วางที่ (X = 90.0 mm, Y = 90.0 mm)
6. วงจรแบ่งแรงดันวัดระดับแบตเตอรี่ (Battery Sense Zone - มุมบนขวา):
   - R1 (ตัวต้านทาน 200kΩ ±1% 0805 SMD): วางที่ (X = 106.0 mm, Y = 86.5 mm)
   - R2 (ตัวต้านทาน 200kΩ ±1% 0805 SMD): วางที่ (X = 106.0 mm, Y = 89.5 mm)
   - C1 (ตัวเก็บประจุ 100nF 0805 SMD): วางที่ (X = 106.0 mm, Y = 92.5 mm)
7. แถบควบคุมพลังงานขอบล่าง (Power Management Strip - แนวนอน Y = 112.5 ถึง 113.0 mm):
   - F1 (ฟิวส์ตัดตอนอัตโนมัติ PTC 0.5A 1206 SMD): วางที่ (X = 89.5 mm, Y = 112.5 mm)
   - SW1 (สวิตช์เลื่อนเปิด-ปิด SPDT PCM12 SMD): วางที่ (X = 95.0 mm, Y = 112.5 mm)
   - J1 (ขั้วต่อแบตเตอรี่ LiPo 3.7V JST-PH 2.0mm 2-Pin): วางที่ (X = 101.0 mm, Y = 113.0 mm)
   - D1 (ไดโอดช็อตต์กี SS14 1A 40V SMA SMD): วางที่ (X = 107.5 mm, Y = 112.5 mm)

---

### 3. ตารางการเชื่อมต่อสัญญาณและโครงข่ายไฟฟ้า (Complete Netlist 20 Nets)
1. 5V_SYS       : D1(Pin 2) -> U1(Pin 14: 5V In) -> U2_CONN(Pin 1: VCC)
2. 3V3_SYS      : U1(Pin 12: 3V3 Out) -> DISP1(Pin 1) -> U3(Pin 1) -> BZ1(Pin 1)
3. GND_SYS      : U1(Pin 13) -> DISP1(Pin 2, Pin 6) -> U3(Pin 2, Pin 7) -> U2_CONN(Pin 2) -> Q1(Pin 2) -> R4(Pin 2) -> R2(Pin 2) -> C1(Pin 2) -> J1(Pin 2)
4. BAT_RAW+     : J1(Pin 1) -> F1(Pin 1)
5. BAT_OUT+     : F1(Pin 2) -> SW1(Pin 1)
6. SW_IN        : Alias ของ BAT_OUT+
7. BAT_SW+      : SW1(Pin 2) -> R1(Pin 1) และต่อเข้าโมดูล TP4056/Boost Step-Up
8. 5V_BOOST     : D1(Pin 1: Anode จากไฟ 5V บูสต์)
9. ADC_BAT      : U1(Pin 3: GPIO2/A2) -> R1(Pin 2) -> R2(Pin 1) -> C1(Pin 1)
10. HUB_MFIO    : U1(Pin 1: GPIO0/D0) -> U2_CONN(Pin 5)
11. HUB_RESET   : U1(Pin 2: GPIO1/D1) -> U2_CONN(Pin 6)
12. I2C_SDA     : U1(Pin 5: GPIO4/D4) -> U3(Pin 4) -> U2_CONN(Pin 3)
13. I2C_SCL     : U1(Pin 6: GPIO5/D5) -> U3(Pin 3) -> U2_CONN(Pin 4)
14. TFT_DC      : U1(Pin 7: GPIO6/D6) -> DISP1(Pin 5)
15. TFT_RST     : U1(Pin 8: GPIO7/D7) -> DISP1(Pin 7)
16. TFT_SCK     : U1(Pin 9: GPIO8/D8) -> DISP1(Pin 3)
17. TFT_MOSI    : U1(Pin 11: GPIO10/D10) -> DISP1(Pin 4)
18. BUZZER_CTL  : U1(Pin 4: GPIO3/D3) -> R3(Pin 1)
19. Q1_BASE     : R3(Pin 2) -> R4(Pin 1) -> Q1(Pin 1: Base)
20. BUZZER_NEG  : Q1(Pin 3: Collector) -> BZ1(Pin 2: ขาลบ)

---

### 4. กฎการเดินลายเส้นแบบแยกชั้นสมบูรณ์ (Topological Zero-Overlap Routing)
- กฎเหล็ก: ห้ามมีลายเส้นต่างสัญญาณวิ่งตัดกันบนเลเยอร์เดียวกันเด็ดขาด (Zero Overlap on Same Plane)
- การแบ่งหน้าที่ของเลเยอร์:
  * Top Layer (F.Cu - สีแดง): เดินเฉพาะเส้นสัญญาณจอแนวตั้ง TFT_MOSI (X = 100.0 mm), TFT_RST (X = 107.62 mm) และบัส I2C ข้ามไปฝั่งขวา
  * Bottom Layer (B.Cu - สีน้ำเงิน): เดินเส้น TFT_DC (Y = 104.5 mm), TFT_SCK (Y = 100.08 mm), 3V3_SYS (Y = 92.46 mm), 5V_SYS, ADC_BAT, สัญญาณควบคุม MFIO/RESET, วงจรบัซเซอร์ และระบบไฟล่าง
  * สัญญาณที่จำเป็นต้องตัดข้ามกันในเชิง 2D ให้ข้ามผ่านคนละเลเยอร์โดยมีเนื้อฉนวน FR-4 หนา 1.0 mm คั่นกลาง
- ขนาดความกว้างลายเส้น (Track Widths):
  * สายไฟกำลัง 5V และ แบตเตอรี่ (5V_SYS, BAT_RAW+, SW_IN, BAT_SW+): กว้าง 0.75 mm (29.5 mil)
  * สายไฟเลี้ยงระบบตรรกะ (3V3_SYS, GND): กว้าง 0.45 - 0.55 mm (17.7 - 21.6 mil)
  * สายสัญญาณข้อมูลความเร็วสูง (SPI, I2C, ADC, Controls): กว้าง 0.35 mm (13.8 mil)
  * ระยะ Clearance ระหว่างทองแดง: ไม่น้อยกว่า 0.35 mm
- ขนาดรูเจาะเวีย (Vias): ขนาดเส้นผ่านศูนย์กลาง 0.80 mm, ขนาดรูเจาะ Drill 0.40 mm

---

### 5. รูปแบบไฟล์ผลลัพธ์ที่ต้องการ (Required Outputs)
1. ไฟล์ KiCad PCB (`.kicad_pcb`): พร้อมฟุตพริ้นท์และลายเส้นเชื่อมต่อครบ 100% ผ่านการตรวจสอบ DRC (0 Errors)
2. ชุดไฟล์ Gerber & Drill ZIP: มาตรฐาน RS-274X ครบทุกเลเยอร์ทองแดง หน้ากาก (Mask), ซิลค์สกรีน (Silk) และรูเจาะ Excellon (`.drl`)
3. ไฟล์ PDF ขนาด 1:1 แบบ 3 หน้าสำหรับงานสร้างจริง:
   - หน้า 1: Bottom Layer (B.Cu) พลิกกระจก (Mirrored) ขาว-ดำ คมชัด สำหรับรีดเตารีดด้านหลัง
   - หน้า 2: Top Layer (F.Cu) หน้าตรงปกติ (Normal) ขาว-ดำ คมชัด สำหรับรีดเตารีดด้านหน้า
   - หน้า 3: แผนผังบอกตำแหน่งบัดกรีอุปกรณ์ (Assembly Map) พร้อมแถบวัดขนาดจริง 50 mm Calibration Bar
```
