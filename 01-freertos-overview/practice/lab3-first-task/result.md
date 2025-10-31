# Lab 3: สร้าง Task แรกด้วย FreeRTOS

## คำถามทบทวน
1. เหตุใด Task function ต้องมี infinite loop?
- เพราะในระบบ FreeRTOS ถ้า Task ทำงานจน return ออกจากฟังก์ชัน
ตัว Scheduler จะไม่จัดการปิดหรือคืนทรัพยากรของ Task ให้อัตโนมัติ

- ดังนั้น Task ควรอยู่ใน ลูปไม่รู้จบ (infinite loop) เพื่อให้ทำงานต่อเนื่องตลอดอายุของระบบ
และป้องกันไม่ให้ Task จบการทำงานโดยไม่ได้ตั้งใจ

2. ความหมายของ stack size ใน xTaskCreate() คืออะไร?
- คือ ขนาดหน่วยความจำ (Stack Memory) ที่จัดสรรให้ Task นั้นโดยเฉพาะ
- ใช้เก็บตัวแปรภายใน ฟังก์ชันที่เรียกซ้อน (function call) และข้อมูลภายในของ Task
- หากกำหนดขนาด เล็กเกินไป อาจเกิด Stack Overflow ทำให้ระบบทำงานผิดพลาดได้
3. ความแตกต่างระหว่าง vTaskDelay() และ vTaskDelayUntil()?
   - vTaskDelay() บอกให้ task บล็อกไปเป็นเวลาที่กำหนด จากเวลาปัจจุบัน 
   - vTaskDelayUntil() บอกให้ task บล็อกจนถึง เวลาที่กำหนดแบบ absolute เพื่อให้ task ทำงานแบบ period ที่คงที่
4. การใช้ vTaskDelete(NULL) vs vTaskDelete(handle) ต่างกันอย่างไร?
- vTaskDelete(NULL) → ลบ Task ตัวเอง (คือ Task ที่เรียกคำสั่งนี้อยู่)
- vTaskDelete(handle) → ลบ Task อื่นๆ โดยอ้างอิงจากตัวแปร handle ของ Task ที่ต้องการลบ
5. Priority 0 กับ Priority 24 อันไหนสูงกว่า?
  - ใน FreeRTOS ตัวเลข Priority ยิ่งมาก ยิ่งมีความสำคัญสูงกว่า
  ดังนั้น
  Priority 24 สูงกว่า Priority 0
