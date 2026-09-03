# ระบบอุปกรณ์สวมใส่ติดตามสัญญาณชีพสุขภาพและเว็บแอปพลิเคชันบริหารจัดการคิวผู้ป่วยนอก
### (Hospital Queue Patient Portal & Smartwatch Health Monitoring)

---

## 📌 บทนำและภาพรวมโครงงาน (Overview)
โครงงานนี้เป็นการวิจัยและพัฒนานวัตกรรมระบบอุปกรณ์สวมใส่อัจฉริยะ (Smartwatch) ร่วมกับเว็บแอปพลิเคชันบริหารจัดการคิวผู้ป่วยนอกของโรงพยาบาล เพื่อยกระดับความปลอดภัยของผู้ป่วยในระหว่างรอรับการตรวจรักษา โดยระบบสามารถ:
1. **ติดตามสัญญาณชีพแบบเรียลไทม์ (Continuous Vital Signs Monitoring):** วัดอัตราการเต้นของหัวใจ (Heart Rate) และระดับความอิ่มตัวของออกซิเจนในเลือด ($SpO_2$) พร้อมคำนวณดัชนีช็อก (Shock Index: $SI = \frac{HR}{SBP}$) เพื่อประเมินภาวะวิกฤตของผู้ป่วย
2. **ตรวจจับอุบัติเหตุการหกล้ม (Multi-Stage Fall Detection):** ตรวจจับสภาวะการตกอิสระ (Free-fall), แรงกระแทก (Impact $SVM > 2.5g$) และสภาวะแน่นิ่งผิดปกติ (Inactivity) ด้วยเซนเซอร์ IMU 6 แกน
3. **จัดลำดับความเร่งด่วนของคิวอัตโนมัติ (Dynamic Queue Prioritization):** คัดกรองและปรับลำดับคิวผู้ป่วยตามหลักเกณฑ์ฉุกเฉิน ESI Version 4 ผ่านระบบ AI Triage เมื่อพบสัญญาณชีพวิกฤต
4. **แจ้งเตือนและส่งข้อมูลแบบทันที (Realtime Communication):** ส่งสัญญาณเตือนไปยังห้องพยาบาลและบุคลากรทางการแพทย์ผ่าน WebSockets ทันทีที่มีเหตุฉุกเฉิน

---

## 📁 โครงสร้างโฟลเดอร์ภายในโปรเจกต์ (Repository Structure)

```text
├── 01_เล่มรายงานโครงงาน_Thesis/
│   ├── เล่มรายงานโครงงาน_ฉบับสมบูรณ์_FINAL_v3_IEEE.docx    # เล่มรายงานโครงงานฉบับสมบูรณ์ (ฟอร์แมต IEEE มทร.อีสาน ขอนแก่น)
│   ├── เล่มรายงานโครงงาน_ฉบับสมบูรณ์_FINAL_v3_IEEE.pdf     # ไฟล์ PDF เล่มสมบูรณ์ (103 หน้า พร้อมตรวจ/พิมพ์)
│   ├── ECP-P01_แบบร่างโครงงานวิศวกรรมคอมพิวเตอร์_ฉบับปรับปรุงสมบูรณ์_v14.docx # แบบร่างข้อเสนอโครงงาน (Proposal v14)
│   ├── ECP-P01_แบบร่างโครงงานวิศวกรรมคอมพิวเตอร์_ฉบับปรับปรุงสมบูรณ์_v14.pdf  # ไฟล์ PDF แบบร่างโครงงาน (20 หน้าเต็ม)
│   └── ร่างเดิมและไฟล์สำรอง_Archive/                     # โฟลเดอร์สำรองไฟล์ดราฟต์เดิมทั้งหมดอย่างปลอดภัย
│
├── 02_ฮาร์ดแวร์และวงจร_Hardware/
│   ├── smartwatch_component_pinouts.html                 # ผังการต่อสาย Pinout และวงจรเซนเซอร์แบบ Interactive Web
│   ├── component_pinouts/                                # แผนภาพ Pinout รายชิ้นส่วน
│   ├── pcb_design/                                       # ไฟล์ออกแบบแผ่นวงจรพิมพ์ PCB (KiCad / EasyEDA)
│   └── pcb_design.zip                                    # ไฟล์บีบอัดสำหรับส่งโรงงานผลิต PCB (Gerber Files)
│
├── 03_ซอร์สโค้ดและเว็บแอป_SourceCode/
│   ├── repo_README.md                                    # เอกสารคู่มือการติดตั้งและการรัน Frontend Web App
│   ├── repo_ARCHITECTURE.md                              # สถาปัตยกรรมระบบ Frontend & Backend API Spec
│   ├── repo_package.json                                 # รายการ Dependencies (Next.js 14, React, Tailwind CSS)
│   ├── repo_patient-api.ts                               # API Client Module สำหรับเชื่อมต่อระบบโรงพยาบาล
│   ├── repo_types.ts                                     # TypeScript Interface สำหรับ Patient, Queue, Vital Signs
│   └── repo_mock_backend.py                              # สคริปต์จำลองเซิร์ฟเวอร์ Mock API สำหรับการทดสอบระบบ
│
├── 04_ไฟล์ข้อมูลและเครื่องมือเสริม_Assets_Tools/
│   ├── extracted_assets/                                 # รูปภาพและกราฟิกประกอบที่ใช้ในเอกสาร
│   ├── extracted_ch4_images/                             # ภาพผลการทดลองและการทดสอบระบบในบทที่ 4
│   ├── logo/                                             # ตราสัญลักษณ์มหาวิทยาลัยเทคโนโลยีราชมงคลอีสาน
│   └── build_full_thesis.py                              # สคริปต์สำหรับบิวด์และจัดรูปแบบรูปเล่มอัตโนมัติ
│
├── AGENTS.md                                             # ข้อกำหนดและแนวทางสำหรับ AI Assistant
├── GEMINI.md                                             # กฎระเบียบข้อบังคับและ Memory Protocol ประจำโปรเจกต์
├── PROJECT_MEMORY.md                                     # บันทึกความจำระยะยาว ประวัติการพัฒนา และข้อสรุปงาน
└── README.md                                             # เอกสารภาพรวมโปรเจกต์ (ไฟล์นี้)
```

---

## 🛠️ รายละเอียดสเปกฮาร์ดแวร์และเซนเซอร์ (Hardware Specifications)

| ส่วนประกอบ (Component) | รายละเอียด (Specification) | ฟังก์ชันการทำงาน |
|---|---|---|
| **MCU Controller** | Seeed Studio XIAO ESP32-C3 | หน่วยประมวลผลหลัก รองรับ Wi-Fi 2.4GHz และ BLE 5.0 |
| **Biometric Sensor** | MAX32664 Biometric Hub + MAX30102 PPG | ตรวจวัด Pulse Rate และ $SpO_2$ ด้วยความแม่นยำสูง |
| **Motion Sensor** | MPU-6050 (6-Axis Accel + Gyro) | ตรวจจับการเคลื่อนไหวและการหกล้ม 3 ขั้นตอน (SVM Analysis) |
| **Power Management** | TP4056 + แบตเตอรี่ LiPo 3.7V (500mAh) | วงจรชาร์จแบตเตอรี่ พร้อมวงจรแบ่งแรงดันวัดระดับแบตเตอรี่ |
| **Display** | จอแสดงผล OLED 0.96 นิ้ว (I2C) | แสดงผลอัตราเต้นหัวใจ, ออกซิเจนในเลือด และสถานะคิว |

---

## 💻 เทคโนโลยีฝั่งเว็บแอปพลิเคชัน (Software Stack)
- **Frontend Framework:** Next.js (App Router), React 18, TypeScript
- **Styling & UI:** Tailwind CSS, Lucide Icons, Headless UI
- **Database & Realtime:** Google Cloud Firestore, WebSockets
- **Deployment:** Vercel / Docker Container

---

## 👥 ผู้จัดทำโครงงาน (Contributors)
- **นายปรเมศว์ เดนนิส โฮค อาร์ริงตัน** (Mr. Porramet Dennis Hoke Arrington)
- **นายธนกร สุภาวรรณชัย** (Mr. Thanakorn Suphawanchai)

**สาขาวิชาวิศวกรรมคอมพิวเตอร์ คณะวิศวกรรมศาสตร์**  
**มหาวิทยาลัยเทคโนโลยีราชมงคลอีสาน วิทยาเขตขอนแก่น**  
**อาจารย์ที่ปรึกษาโครงงาน:** อาจารย์อรินธร เจษฎาเมธาขจร  
**ปีการศึกษา:** 2568 (Academic Year 2025)
