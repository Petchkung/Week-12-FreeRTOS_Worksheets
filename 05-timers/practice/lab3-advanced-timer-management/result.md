# Lab 3: Advanced Timer Management & Performance 
## 📋 Advanced Analysis Questions
1. **Service Task Priority**: ผลกระทบของ Priority ต่อ Timer Accuracy?
- การตั้ง Priority สูง จะช่วยให้ Timer Callback ถูกเรียกได้ตรงเวลา และลดอาการ Jitter (ความคลาดเคลื่อนของเวลา)
- อย่างไรก็ตาม หากตั้ง Priority สูงเกินไป อาจทำให้ Task อื่น ๆ ขาดทรัพยากร CPU
- ควรเลือก Priority ให้เหมาะสมกับลักษณะของระบบ เช่น
    - ใช้ Priority = 15 สำหรับงานที่ต้องการความแม่นยำแบบ Real-time
    - หลีกเลี่ยงการตั้งสูงเกินความจำเป็น เพื่อให้ระบบคงความสมดุลระหว่าง Task
2. **Callback Performance**: วิธีการเพิ่มประสิทธิภาพ Callback Functions?
- ลดระยะเวลาการทำงานภายใน Callback เพื่อไม่ให้รบกวน Timer อื่น ๆ
- ภายใน Callback ไม่ควรทำงานหนักหรือประมวลผลซับซ้อน แต่ควรใช้วิธี ส่งสัญญาณต่อไปยัง Task อื่น ผ่าน
    - Queue,
    - Event Group, หรือ
    - Task Notification
- ตัวอย่างแนวทางที่ดี:
```
void vTimerCallback(TimerHandle_t xTimer) {
    xQueueSend(timer_event_queue, &event, 0);
}
```
- แนวคิดคือ “Callback ทำงานเบา ส่งต่อข้อมูลให้ Task ประมวลผลภายหลัง” เพื่อรักษาความเร็วและความแม่นยำของระบบ Timer
3. **Memory Management**: กลยุทธ์การจัดการ Memory สำหรับ Dynamic Timers?
- ใช้ Static Allocation สำหรับ Timer ที่ต้องมีอยู่ตลอดเวลา เช่น System Watchdog หรือ Heartbeat
- ใช้ Dynamic Allocation สำหรับ Timer ชั่วคราวที่สร้าง–ลบระหว่างการทำงาน
- ควรมีระบบเฝ้าระวังหน่วยความจำ เช่น
    - ตรวจสอบค่า Free Heap เป็นระยะ
    - ใช้ฟังก์ชัน cleanup_dynamic_timers() เพื่อลบ Timer ที่ไม่ได้ใช้งาน
➡️ กลยุทธ์นี้ช่วยให้ระบบมีเสถียรภาพและป้องกันการรั่วของหน่วยความจำ (Memory Leak)
4. **Error Recovery**: วิธีการ Handle Timer System Failures?
- หากคำสั่ง xTimerStart() หรือ xTimerStop() ทำงานไม่สำเร็จ ให้ใช้ การ Retry แบบปลอดภัย
เช่น ใช้ฟังก์ชัน safe_timer_start() เพื่อเรียกซ้ำ
- บันทึกความผิดพลาดลงในตัวแปร Health Data เพื่อใช้ตรวจสอบย้อนหลัง เช่น
```
health_data.command_failures++;
```
- แนวทางนี้ช่วยให้ระบบสามารถตรวจจับและวิเคราะห์ความผิดปกติได้อย่างเป็นระบบ และไม่หยุดทำงานทันทีเมื่อเกิดข้อผิดพลาด
5. **Production Deployment**: การปรับแต่งสำหรับ Production Environment?
- เพื่อให้ระบบ เสถียร ประหยัดพลังงาน และพร้อมใช้งานจริง, ควรดำเนินการดังนี้:

     - ใช้ Static Timer สำหรับฟังก์ชันหลักเพื่อลด Overhead
     - เปิดใช้ Health Monitoring System เพื่อติดตามความผิดปกติ
     - ตรวจสอบ Stack/Heap Usage อย่างสม่ำเสมอ
     - ตั้งค่า Service Task Priority ให้สมดุลระหว่างความแม่นยำและการตอบสนอง
     - ปิด Debug Logs ใน Production เพื่อลดการใช้ CPU และ Flash I/O
- การปรับแต่งเหล่านี้ช่วยให้ระบบ Timer ทำงานได้ อย่างแม่นยำ เสถียร และมีประสิทธิภาพสูงสุด ในสภาพแวดล้อมจริง
