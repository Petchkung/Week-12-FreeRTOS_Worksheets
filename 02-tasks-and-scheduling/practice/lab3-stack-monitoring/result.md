# Lab 3: Stack Monitoring และ Debugging
## คำถามสำหรับวิเคราะห์
1. Task ไหนใช้ stack มากที่สุด? เพราะอะไร?
- Heavy Task ใช้ Stack มากที่สุด
เพราะในฟังก์ชัน heavy_stack_task() มีการประกาศตัวแปรภายใน (Local Variable) ขนาดใหญ่
- ซึ่งตัวแปรลักษณะนี้จะถูกเก็บใน Stack ของ Task ทำให้พื้นที่ Stack ถูกใช้มาก
หาก Stack ไม่เพียงพออาจเกิด Warning หรือ Stack Overflow ได้
2. การใช้ heap แทน stack มีข้อดีอย่างไร?
- ป้องกัน Stack Overflow สำหรับข้อมูลขนาดใหญ่
- ใช้หน่วยความจำได้อย่าง ยืดหยุ่น และสามารถคืนพื้นที่ได้ด้วย free()
- เหมาะกับการเก็บข้อมูลที่ต้อง อยู่ข้ามการเรียกฟังก์ชัน (Function Call)
  โดยเฉพาะกรณีที่ข้อมูลมีขนาดใหญ่หรือไม่แน่นอน
3. Stack overflow เกิดขึ้นเมื่อไหร่และทำอย่างไรป้องกัน?
- เกิดขึ้นเมื่อ Task ใช้พื้นที่ Stack เกินขนาดที่กำหนดไว้
เช่น การใช้ Local Array ขนาดใหญ่ หรือมีการเรียก Recursion ลึกเกินไป

- วิธีป้องกัน Stack Overflow:
    - กำหนด Stack Size ให้เหมาะสม กับงานของแต่ละ Task
    - เปิดใช้ฟีเจอร์ตรวจสอบ Overflow ของ FreeRTOS (configCHECK_FOR_STACK_OVERFLOW)
    - หลีกเลี่ยงการใช้ตัวแปรขนาดใหญ่ในฟังก์ชัน
    - ใช้ Heap สำหรับข้อมูลขนาดใหญ่แทน
4. การตั้งค่า stack size ควรพิจารณาจากอะไร?
- จำนวนและขนาดของ local variables
- ความลึกของ function call หรือ recursion
- ฟังก์ชันที่ใช้ เช่น printf() ใช้ stack เยอะ
- ผลจากการทดลองจริงด้วย uxTaskGetStackHighWaterMark()
5. Recursion ส่งผลต่อ stack usage อย่างไร?
- การ Recursion จะทำให้ Stack ถูกใช้เพิ่มขึ้นทุกครั้งที่มีการเรียกฟังก์ชันซ้ำ
- เพราะทุกครั้งจะต้องสร้าง Stack Frame ใหม่ เพื่อเก็บตัวแปรภายในและตำแหน่ง return address
- หากความลึกของ Recursion มากเกินไป จะทำให้ Stack Usage เพิ่มขึ้นแบบทวีคูณ
และอาจเกิด Stack Overflow ได้ในที่สุด
