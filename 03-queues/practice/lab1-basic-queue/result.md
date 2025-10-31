# Lab 1: Basic Queue Operations
### คำถามสำหรับการทดลอง
1. เมื่อ Queue เต็ม การเรียก `xQueueSend` จะเกิดอะไรขึ้น?
- หาก Queue เต็ม, Task ที่เรียก xQueueSend() จะ เข้าสู่สถานะรอ (Blocked)
จนกว่า Queue จะมีที่ว่างให้ส่งข้อมูลได้
- ถ้ากำหนด Timeout ไว้ และเวลาหมดก่อนที่จะมีที่ว่าง
การส่งจะ ไม่สำเร็จ และฟังก์ชันจะคืนค่า pdFAIL
2. เมื่อ Queue ว่าง การเรียก `xQueueReceive` จะเกิดอะไรขึ้น?
- หาก Queue ว่าง, Task ที่เรียก xQueueReceive() จะ รอ (Blocked) จนกว่าจะมีข้อมูลใหม่ถูกส่งเข้ามาใน Queue
- หากเกินเวลาที่กำหนดใน Timeout, การรับจะ ไม่สำเร็จ และฟังก์ชันจะคืนค่า pdFAIL
3. ทำไม LED จึงกะพริบตามการส่งและรับข้อความ?
- เนื่องจากในโค้ดมีการสั่งให้ LED ติด–ดับทุกครั้งที่มีการส่งหรือรับข้อมูลสำเร็จผ่าน Queue
เพื่อใช้เป็น ตัวบ่งชี้สถานะการทำงานของ Task (Sender/Receiver) แบบมองเห็นได้ง่าย

- ตัวอย่างโค้ดแสดงพฤติกรรมของ LED เมื่อส่งข้อมูลสำเร็จ:
    ```
    if (xStatus == pdPASS) {
    ESP_LOGI(TAG, "Sent: ID=%d, MSG=%s, Time=%lu", 
             message.id, message.message, message.timestamp);
    
    // 🔸 ทำให้ LED กะพริบเมื่อส่งข้อมูลสำเร็จ
    gpio_set_level(LED_SENDER, 1);      // เปิดไฟ LED
    vTaskDelay(pdMS_TO_TICKS(100));     // หน่วงเวลา 100 ms
    gpio_set_level(LED_SENDER, 0);      // ปิดไฟ LED
    }
    ```
