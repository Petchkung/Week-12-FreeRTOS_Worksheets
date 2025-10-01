1. การวัด CPU Utilization

สังเกตการแสดงสถิติทุก 20 context switches

<img width="518" height="155" alt="image" src="https://github.com/user-attachments/assets/932fe9d5-69dc-4ef2-8091-fbae2a5c9ba8" />

บันทึกค่า CPU utilization และ overhead

<img width="539" height="43" alt="image" src="https://github.com/user-attachments/assets/f2a884d1-fa6a-4afa-a551-6a750668e18d" />

2. การทดสอบ Time Slice ต่างๆ

ทดสอบ time slice: 10ms, 25ms, 50ms, 100ms, 200ms
เปรียบเทียบประสิทธิภาพ

<img width="878" height="256" alt="image" src="https://github.com/user-attachments/assets/3a28c157-05aa-4a0d-bff4-7f82ed4e24db" />


คำถามสำหรับวิเคราะห์
1. Time slice ขนาดไหนให้ประสิทธิภาพดีที่สุด? เพราะอะไร?

Time slice ขนาด 50 ms ให้ประสิทธิภาพดีที่สุด
เหตุผล
มี ความสมดุลระหว่างการตอบสนอง (responsiveness) และ ประสิทธิภาพของ CPU (CPU utilization)
ไม่สั้นเกินไปจนเสียเวลาสลับ task บ่อย
ไม่ยาวเกินไปจน task เบาต้องรอคิวนาน
ลด context switching overhead ได้มากกว่าช่วงเวลาอื่น

2. ปัญหาอะไรที่เกิดขึ้นเมื่อ time slice สั้นเกินไป?

เกิด context switching บ่อยเกินไป
ทำให้ CPU เสียเวลาสลับ task มากกว่าทำงานจริง
ส่งผลให้ CPU utilization ต่ำ และ overhead สูง
บาง task อาจทำงานไม่เสร็จภายใน slice เดียว → ทำซ้ำหลายรอบ เสียประสิทธิภาพ

3. ปัญหาอะไรที่เกิดขึ้นเมื่อ time slice ยาวเกินไป?

งานที่ใช้เวลาน้อย (เช่น Display, Sensor) ต้อง รอนานกว่าจะได้ทำงาน → ตอบสนองช้า
ถ้า task หนึ่งกินเวลานานเกินไป จะ บล็อก task อื่น
ลดความสามารถของระบบในการตอบสนองแบบ real-time
เสี่ยงต่อ starvation (task บางตัวไม่ได้ทำงานเลย)

4. Context switching overhead คิดเป็นกี่เปอร์เซ็นต์ของเวลาทั้งหมด?

<img width="600" height="279" alt="image" src="https://github.com/user-attachments/assets/073c4b8a-65fb-4a91-a69a-3f917d221f71" />

5. งานไหนที่ได้รับผลกระทบมากที่สุดจากการ time-sharing?

งานที่ใช้เวลาประมวลผลนาน 
เหตุผล
Task นี้ใช้ CPU หนัก (loop มาก) → มัก ไม่เสร็จภายใน time slice เดียว
ถ้า time slice สั้น → ต้อง ถูกตัดหลายรอบ → ทำให้ไม่มีความต่อเนื่อง
อาจต้องใช้เวลาหลายรอบถึงจะทำงานเสร็จ → ประสิทธิภาพต่ำลง
