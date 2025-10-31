# Lab 2: Task States Demonstration
## คำถามสำหรับวิเคราะห์
1. Task อยู่ใน Running state เมื่อไหร่บ้าง?
  - Task จะอยู่ใน Running State เมื่อได้รับ CPU จาก Scheduler และกำลังประมวลผลจริง
เช่น ในฟังก์ชัน state_demo_task ตอนที่ LED (GPIO2) สว่างอยู่
2. ความแตกต่างระหว่าง Ready และ Blocked state คืออะไร?
  - Ready: task พร้อมทำงาน แต่ยังไม่ได้รับ CPU (รอคิว)
  - Blocked: task รอ event หรือ resource เช่น semaphore หรือ delay
3. การใช้ vTaskDelay() ทำให้ task อยู่ใน state ใด?
  - คำสั่ง vTaskDelay() จะทำให้ Task เข้าสู่ Blocked State ชั่วคราว
เมื่อเวลาที่กำหนดหมดลง Task จะ กลับเข้าสู่ Ready State เพื่อรอการรันต่อ
4. การ Suspend task ต่างจาก Block อย่างไร?
  - Suspend: หยุด task ด้วยคำสั่งจากภายนอก (vTaskSuspend() / Resume) จะไม่กลับมาทำงานจนกว่าจะ vTaskResume()
  - Block: task หยุดเองเพราะรอ event/time แล้วกลับมาอัตโนมัติเมื่อเงื่อนไขครบ
5. Task ที่ถูก Delete จะกลับมาได้หรือไม่?
  - ไม่ได้ 
เมื่อ Task ถูกลบด้วย vTaskDelete() แล้ว จะถูก นำออกจากระบบโดยสมบูรณ์
หากต้องการให้ Task กลับมาทำงานอีก ต้อง สร้างใหม่ ด้วย xTaskCreate() เท่านั้น
