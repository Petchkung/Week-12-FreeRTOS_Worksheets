# Lab 1: Task Priority และ Scheduling
## คำถามสำหรับวิเคราะห์
1. Priority ไหนทำงานมากที่สุด? เพราะอะไร?
- Task ที่มี Priority สูงสุด (High Priority Task) จะทำงานมากที่สุด
เนื่องจากในระบบ FreeRTOS Scheduler จะเลือก Task ที่อยู่ในสถานะ “Ready” และมี Priority สูงสุด มาทำงานก่อนเสมอ
ดังนั้น Task ที่มีตัวเลข Priority มากกว่าจะได้รับ CPU ก่อน
2. เกิด Priority Inversion หรือไม่? จะแก้ไขได้อย่างไร?
- เกิด Priority Inversion ได้ในบางกรณี
เช่น Task ที่มี Priority ต่ำถือครองทรัพยากร (Resource) อยู่ แล้ว Task ที่มี Priority สูงต้องรอ

- วิธีแก้ไข:
ใช้ Mutex ที่รองรับ Priority Inheritance → Task ที่ถือ Resource จะถูก ยก Priority ชั่วคราว จนกว่าจะปล่อย Resource
3. Tasks ที่มี priority เดียวกันทำงานอย่างไร?
- Task ที่มี Priority เท่ากันจะ ไม่แย่ง CPU กันโดยตรง
- Scheduler จะใช้วิธี Time-sharing (Round Robin Scheduling)
แต่ละ Task จะได้เวลาทำงานตามรอบ (Time Slice) อย่างเท่าเทียมกัน
4. การเปลี่ยน Priority แบบ dynamic ส่งผลอย่างไร?
- การเปลี่ยน Priority แบบ Dynamic จะทำให้ลำดับการทำงานของ Task เปลี่ยนทันที
- Scheduler จะ จัดลำดับใหม่ทันที ตาม Priority ปัจจุบัน
ซึ่งสามารถใช้ควบคุมลำดับความสำคัญของ Task ในช่วงเวลาต่าง ๆ ของระบบได้อย่างยืดหยุ่น
5. CPU utilization ของแต่ละ priority เป็นอย่างไร?
- Task ที่มี Priority สูง จะได้รับ CPU มากกว่า เพราะ Scheduler ให้รันก่อนเสมอ
- ส่วน Task ที่มี Priority ต่ำกว่า จะได้ทำงานน้อยลง หรืออาจต้อง รอจนกว่า Task ที่สูงกว่าจะว่าง
