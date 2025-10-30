# Lab 1: ESP-IDF Setup และโปรเจกต์แรก
## คำถามทบทวหน

1. ไฟล์ใดบ้างที่จำเป็นสำหรับโปรเจกต์ ESP-IDF ขั้นต่ำ?
- CMakeLists.txt — ต้องมีทั้งในโฟลเดอร์หลัก (root) และในโฟลเดอร์ main/
- main/main.c — ไฟล์โค้ดหลักของโปรเจกต์ (หรืออาจเป็น C/C++ อื่นๆ ตามที่ใช้)
- sdkconfig — ไฟล์เก็บค่าการตั้งค่าโปรเจกต์ทั้งหมด
2. ความแตกต่างระหว่าง `hello_esp32.bin` และ `hello_esp32.elf` คืออะไร?
- .elf → เป็น Executable File ที่ใช้สำหรับ Debug มีข้อมูล Symbol ใช้ใน IDE/Debugger
- .bin → เป็น Binary File ที่ใช้สำหรับ แฟลชลงบอร์ด ESP32 โดย ไม่มีข้อมูล Symbol
3. คำสั่ง `idf.py set-target` ทำอะไร?
- ใช้ ตั้งค่า Target Chip ให้ตรงกับรุ่นของ ESP32 ที่ใช้งานจริง เพื่อให้ระบบคอมไพล์โค้ดได้ถูกต้อง
4. โฟลเดอร์ `build/` มีไฟล์อะไรบ้าง?
- ไฟล์ Binary และ ELF เช่น .bin, .elf
- ไฟล์ Object (.o)
- ไฟล์ Linker Script (.ld)
- ไฟล์ Map, Log Build, CMake Cache
- ไฟล์ Library ของแต่ละ Component
5. การใช้ `vTaskDelay()` แทน `delay()` มีความสำคัญอย่างไร?
- vTaskDelay() → เป็นฟังก์ชันที่ รู้จักระบบ FreeRTOS
  ให้ Task อื่นสามารถทำงานต่อได้
  ป้องกันการ Block CPU ทั้งระบบ
- delay() → เป็นฟังก์ชันแบบ Blocking
  หยุดการทำงานของ CPU ทั้งหมด
  ไม่เหมาะกับระบบ Multitasking
