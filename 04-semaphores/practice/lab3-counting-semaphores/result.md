# Lab 3: Counting Semaphores
### คำถามสำหรับการทดลอง
1. เมื่อ Producers มากกว่า Resources จะเกิดอะไรขึ้น?
- เมื่อจำนวน Producers มากกว่า Resource ที่มีอยู่ในระบบ, จะเกิดการ รอคิว (Blocked State)
เพราะทุก Producer ต้องขอใช้ Resource ผ่าน xSemaphoreTake()
- ผลที่เกิดขึ้นคือ:
     - บาง Producer ที่ขอใช้ทันจะได้ Resource ไปทำงานทันที
     - ส่วน Producer ที่เหลือจะต้อง รอจนกว่าทรัพยากรถูกคืนด้วย xSemaphoreGive()
     - ทำให้เกิด การหน่วงเวลา (Wait Time) และบาง Task อาจ Timeout หากรอนานเกิน 8 วินาที (ตามโค้ดที่กำหนดไว้)
     - ส่งผลให้ Success Rate ลดลง เพราะบาง Producer ไม่สามารถขอใช้ Resource ได้ทันเวลา
2. Load Generator มีผลต่อ Success Rate อย่างไร?
  - ทำให้ resource pool ถูกใช้จนหมด (Resource pool exhausted)
  - Producers ที่กำลังรอจะยิ่งรอคิวนานขึ้น และบางรายอาจ timeout
  - หลัง load burst จบ Success Rate จะลดลงชั่วคราว แล้วค่อยกลับมาสูงขึ้นเมื่อ resource ถูกคืน
3. Counting Semaphore จัดการ Resource Pool อย่างไร?
- Counting Semaphore จะถูกสร้างด้วย
  ```
  xSemaphoreCreateCounting(MAX_RESOURCES, MAX_RESOURCES);
  ```
  ซึ่งระบุทั้งจำนวน สูงสุดของ Resource และ ค่าปัจจุบันเริ่มต้น

- การทำงาน:
     - เมื่อ Task ต้องการใช้ Resource → เรียก xSemaphoreTake() → ค่าลดลง 1
     - เมื่อ Task ใช้งานเสร็จ → เรียก xSemaphoreGive() → ค่านับเพิ่มกลับ 1
- หากค่าของ Semaphore ลดลงถึง 0 หมายถึง Resource ทั้งหมดถูกใช้งานอยู่
→ Task ใหม่ที่เข้ามาจะต้อง รอ (Blocked) หรือ Timeout หากรอนานเกินกำหนด
