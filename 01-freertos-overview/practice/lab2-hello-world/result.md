# Lab 2: Hello World และ Serial Communication

## คำถามทบทวน
1. ความแตกต่างระหว่าง `printf()` และ `ESP_LOGI()` คืออะไร?   
- printf() → ใช้แสดงข้อความแบบพื้นฐาน
ไม่มี tag, ไม่มี log level, และไม่มี เวลา (timestamp)

- ESP_LOGI() → เป็นระบบ logging ของ ESP-IDF
มี tag, ระดับ log (log level), และ timestamp
ทำให้จัดการ log ได้ง่ายกว่า และสามารถ กรองข้อความตามระดับความสำคัญ ได้
2. Log level ไหนที่จะแสดงใน default configuration?
- ค่าเริ่มต้นคือ Info (ESP_LOGI)
- และจะแสดงระดับที่ สูงกว่า ด้วย เช่น Warning และ Error
3. การใช้ `ESP_ERROR_CHECK()` มีประโยชน์อย่างไร?
- ใช้ตรวจสอบ ค่าผลลัพธ์ (return value) ของฟังก์ชันที่ส่งกลับมาในรูปแบบ esp_err_t
- หากเกิด Error จะ:
แสดงข้อความ log ที่ระบุชนิดของ error
และ หยุดการทำงานของโปรแกรมทันที
ช่วยให้ตรวจจับและแก้ไขข้อผิดพลาดได้ง่ายระหว่างพัฒนา
4. คำสั่งใดในการออกจาก Monitor mode?
  - Ctrl + ]
5. การตั้งค่า Log level สำหรับ tag เฉพาะทำอย่างไร?
  - ใช้ `esp_log_level_set("TAG_NAME", ESP_LOG_LEVEL_INFO);`
  - สามารถตั้งได้เป็น `NONE`, `ERROR`, `WARN`, `INFO`, `DEBUG`, `VERBOSE`
