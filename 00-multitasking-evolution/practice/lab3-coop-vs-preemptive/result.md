# Lab 3: Cooperative vs Preemptive Comparison

## การทดสอบและเปรียบเทียบ

### การทดสอบ Cooperative System
1. Build และ flash โปรแกรมโดย uncomment `test_cooperative_multitasking()`
2. กดปุ่มหลายครั้งและสังเกตเวลาตอบสนอง
  - เวลาตอนสนองมีทั้ง 0 , 10 , 20 ms ตามเวลาที่กดปุ่ม
3. บันทึกเวลาตอบสนองสูงสุด
  - สูงสุดที่ 20 ms

### การทดสอบ Preemptive System
1. แก้ไขโค้ดโดย uncomment `test_preemptive_multitasking()`
2. Build และ flash ใหม่
3. กดปุ่มหลายครั้งและเปรียบเทียบเวลาตอบสนอง
  - เวลาตอนสนองที่เร็วกว่า Cooperative System
## คำถามสำหรับวิเคราะห์

1. ระบบไหนมีเวลาตอบสนองดีกว่า? เพราะอะไร?
  - Preemptive ดีกว่า เพราะสลับ task ทันที ไม่ต้องรอ task ปัจจุบันเสร็จ
2. ข้อดีของ Cooperative Multitasking คืออะไร?
  - ง่ายต่อออกแบบ
  - ประหยัด CPU/หน่วยความจำ
  - เหมาะกับงานลำดับชัดเจน
3. ข้อเสียของ Cooperative Multitasking คืออะไร?
  - ตอบสนองช้า
  - ยากคาดการณ์
  - เสี่ยงถ้า task ไม่ยอมสลับ
4. ในสถานการณ์ใดที่ Cooperative จะดีกว่า Preemptive?
  - งานไม่ต้องตอบสนองทันที
  - ลำดับชัดเจน
  - ลด overhead
5. เหตุใด Preemptive จึงเหมาะสำหรับ Real-time systems?
  -ตอบสนองทันที
  จัด priority ได้
