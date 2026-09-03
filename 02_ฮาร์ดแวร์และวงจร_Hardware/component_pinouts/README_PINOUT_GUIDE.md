# 📌 คู่มือแผนผังขา (Pinout) และรูปภาพอุปกรณ์ทุกตัว ทุกค่า (Complete Hardware Pinout Guide)
## โครงการ SmartWatch Carrier Board v1.0 (อุปกรณ์สวมใส่ติดตามสุขภาพและระบบคิวผู้ป่วยนอก)

โฟลเดอร์นี้รวบรวม **รูปภาพแผนผังขา (Pinout Diagrams)** ความละเอียดสูงระดับโปสเตอร์วิศวกรรม, มาร์คกิ้งบนตัวถัง SMD, ขั้วต่อ (Polarity), และตารางจับคู่ขาสัญญาณทั้งหมด 17 ชิ้นส่วนของวงจร

---

### 📂 ไฟล์ภาพทั้งหมดในโฟลเดอร์นี้:
1. **[00_MASTER_PINOUT_CHEATSHEET.png](./00_MASTER_PINOUT_CHEATSHEET.png)** - โปสเตอร์รวมผังขาทุกอุปกรณ์ความละเอียดสูงพิเศษ 2260x3380 px
2. **[01_Official_Seeed_XIAO_Wiki_Pinout.png](./01_Official_Seeed_XIAO_Wiki_Pinout.png)** - ผังขาทางการจาก Seeed Studio Wiki
3. **[01_XIAO_ESP32C3_Pinout.png](./01_xiao_esp32c3_pinout.png)** - ผังขา Seeed Studio XIAO ESP32-C3 พร้อมจุดต่อ SmartWatch
4. **[02_Pulse_Express_MAX32664_MAX30102_Pinout.png](./02_Pulse_Express_MAX32664_MAX30102_Pinout.png)** - ขั้วต่อ JST-SH 6P เซนเซอร์ชีพจรและ SpO2
5. **[03_MPU6050_GY521_Pinout.png](./03_MPU6050_GY521_Pinout.png)** - ผังขา 8 พิน โมดูลตรวจจับการหกล้ม MPU-6050
6. **[04_GC9A01_Round_TFT_7Pin_Pinout.png](./04_GC9A01_Round_TFT_7Pin_Pinout.png)** - ผังขา 7 พิน SPI หน้าจอแสดงผลทรงกลม GC9A01
7. **[05_TP4056_LiPo_Charger_Module.png](./05_TP4056_LiPo_Charger_Module.png)** - โมดูลชาร์จ LiPo TP4056 พร้อมวงจรป้องกัน DW01A
8. **[06_MT3608_5V_Boost_Converter.png](./06_MT3608_5V_Boost_Converter.png)** - โมดูลบูสต์สเต็ปอัป 3.7V เป็น 5.0V MT3608
9. **[07_S8050_NPN_Transistor_SOT23.png](./07_S8050_NPN_Transistor_SOT23.png)** - ทรานซิสเตอร์ S8050 (มาร์คกิ้ง J3Y บนตัวถัง SOT-23)
10. **[08_Active_Buzzer_3.3V.png](./08_Active_Buzzer_3.3V.png)** - บัซเซอร์ 3.3V พร้อมบอกขั้วบวก (+) และขั้วลบ (-)
11. **[09_SS14_Schottky_Diode_SMA.png](./09_SS14_Schottky_Diode_SMA.png)** - ไดโอด SS14 พร้อมตำแหน่งแถบสีขาวขั้วลบ Cathode
12. **[10_PTC_Resettable_Fuse_0.5A_1206.png](./10_PTC_Resettable_Fuse_0.5A_1206.png)** - ฟิวส์คืนสภาพ 0.5A ขนาด 1206 SMD
13. **[11_PCM12_SPDT_Slide_Switch.png](./11_PCM12_SPDT_Slide_Switch.png)** - สวิตช์เลื่อนเปิด-ปิด SPDT PCM12 SMD
14. **[12_JST_PH_2Pin_Battery_Connector.png](./12_JST_PH_2Pin_Battery_Connector.png)** - ขั้วต่อสายไฟแบตเตอรี่ LiPo แดง (+)/ดำ (-)
15. **[13_Resistor_R1_200k_0805.png](./13_Resistor_R1_200k_0805.png)** - ตัวต้านทาน R1: 200kΩ ±1% (รหัส 2003 / 204)
16. **[14_Resistor_R2_200k_0805.png](./14_Resistor_R2_200k_0805.png)** - ตัวต้านทาน R2: 200kΩ ±1% (รหัส 2003 / 204)
17. **[15_Resistor_R3_1k_0805.png](./15_Resistor_R3_1k_0805.png)** - ตัวต้านทาน R3: 1kΩ ±5% (รหัส 102)
18. **[16_Resistor_R4_100k_0805.png](./16_Resistor_R4_100k_0805.png)** - ตัวต้านทาน R4: 100kΩ ±5% (รหัส 104)
19. **[17_Capacitor_C1_100nF_0805.png](./17_Capacitor_C1_100nF_0805.png)** - ตัวเก็บประจุ C1: 100nF 50V (MLCC 0805 สีน้ำตาล)
20. **[index.html](./index.html)** - โปรแกรมเปิดดูผังขาแบบโต้ตอบ (Interactive Pinout Viewer) ในเบราว์เซอร์
