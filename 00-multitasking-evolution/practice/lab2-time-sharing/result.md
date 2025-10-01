1. การวัด CPU Utilization

สังเกตการแสดงสถิติทุก 20 context switches

บันทึกค่า CPU utilization และ overhead

<img width="539" height="43" alt="image" src="https://github.com/user-attachments/assets/f2a884d1-fa6a-4afa-a551-6a750668e18d" />

2. การทดสอบ Time Slice ต่างๆ

ทดสอบ time slice: 10ms, 25ms, 50ms, 100ms, 200ms

เปรียบเทียบประสิทธิภาพ

คำถามสำหรับวิเคราะห์
Time slice ขนาดไหนให้ประสิทธิภาพดีที่สุด? เพราะอะไร?

ปัญหาอะไรที่เกิดขึ้นเมื่อ time slice สั้นเกินไป?

ปัญหาอะไรที่เกิดขึ้นเมื่อ time slice ยาวเกินไป?

Context switching overhead คิดเป็นกี่เปอร์เซ็นต์ของเวลาทั้งหมด?

งานไหนที่ได้รับผลกระทบมากที่สุดจากการ time-sharing?
