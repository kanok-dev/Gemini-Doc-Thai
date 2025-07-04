# คำสั่ง CLI

Gemini CLI รองรับคำสั่งที่มีอยู่ในตัวหลายคำสั่งเพื่อช่วยคุณจัดการเซสชัน ปรับแต่งอินเทอร์เฟซ และควบคุมพฤติกรรม คำสั่งเหล่านี้มีคำนำหน้าด้วยเครื่องหมายทับไปข้างหน้า (`/`) สัญลักษณ์แอท (`@`) หรือเครื่องหมายอัศเจรีย์ (`!`)

## คำสั่ง Slash (`/`)

คำสั่ง Slash ให้การควบคุมระดับเมตาเหนือ CLI เอง

- **`/bug`**
  - **คำอธิบาย:** ยื่นปัญหาเกี่ยวกับ Gemini CLI โดยดีฟอลต์ ปัญหาจะถูกยื่นใน GitHub repository สำหรับ Gemini CLI สตริงที่คุณป้อนหลัง `/bug` จะกลายเป็นหัวข้อสำหรับบั๊กที่กำลังยื่น พฤติกรรมดีฟอลต์ `/bug` สามารถแก้ไขได้โดยใช้การตั้งค่า `bugCommand` ในไฟล์ `.gemini/settings.json` ของคุณ

- **`/chat`**
  - **คำอธิบาย:** บันทึกและกลับมาใช้ประวัติการสนทนาสำหรับการแยกสาขาสถานะการสนทนาแบบโต้ตอบ หรือกลับมาใช้สถานะก่อนหน้าจากเซสชันภายหลัง
  - **คำสั่งย่อย:**
    - **`save`**
      - **คำอธิบาย:** บันทึกประวัติการสนทนาปัจจุบัน คุณต้องเพิ่ม `<tag>` สำหรับระบุสถานะการสนทนา
      - **การใช้งาน:** `/chat save <tag>`
    - **`resume`**
      - **คำอธิบาย:** กลับมาใช้การสนทนาจากการบันทึกก่อนหน้า
      - **การใช้งาน:** `/chat resume <tag>`
    - **`list`**
      - **คำอธิบาย:** แสดงรายการแท็กที่มีอยู่สำหรับการกลับมาใช้สถานะแชท

- **`/clear`**
  - **คำอธิบาย:** ล้างหน้าจอเทอร์มินัล รวมถึงประวัติเซสชันที่มองเห็นได้และ scrollback ภายใน CLI ข้อมูลเซสชันพื้นฐาน (สำหรับการเรียกคืนประวัติ) อาจถูกรักษาไว้ขึ้นอยู่กับการใช้งานที่แน่นอน แต่การแสดงผลภาพจะถูกล้าง
  - **แป้นพิมพ์ลัด:** กด **Ctrl+L** ตลอดเวลาเพื่อทำการล้าง

- **`/compress`**
  - **คำอธิบาย:** แทนที่บริบทแชททั้งหมดด้วยสรุป ช่วยประหยัดโทเค็นที่ใช้สำหรับงานในอนาคตขณะรักษาสรุประดับสูงของสิ่งที่เกิดขึ้น

- **`/editor`**
  - **คำอธิบาย:** เปิดกล่องโต้ตอบสำหรับเลือกเอดิเตอร์ที่รองรับ

- **`/help`** (หรือ **`/?`**)
  - **คำอธิบาย:** แสดงข้อมูลช่วยเหลือเกี่ยวกับ Gemini CLI รวมถึงคำสั่งที่มีอยู่และการใช้งาน

- **`/mcp`**
  - **คำอธิบาย:** แสดงรายการเซิร์ฟเวอร์ Model Context Protocol (MCP) ที่กำหนดค่า สถานะการเชื่อมต่อ รายละเอียดเซิร์ฟเวอร์ และเครื่องมือที่มีอยู่
  - **คำสั่งย่อย:**
    - **`desc`** หรือ **`descriptions`**:
      - **คำอธิบาย:** แสดงคำอธิบายโดยละเอียดสำหรับเซิร์ฟเวอร์และเครื่องมือ MCP
    - **`nodesc`** หรือ **`nodescriptions`**:
      - **คำอธิบาย:** ซ่อนคำอธิบายเครื่องมือ แสดงเฉพาะชื่อเครื่องมือ
    - **`schema`**:
      - **คำอธิบาย:** แสดง JSON schema เต็มสำหรับพารามิเตอร์ที่กำหนดค่าของเครื่องมือ
  - **แป้นพิมพ์ลัด:** กด **Ctrl+T** ตลอดเวลาเพื่อสลับระหว่างการแสดงและซ่อนคำอธิบายเครื่องมือ

- **`/memory`**
  - **คำอธิบาย:** จัดการบริบทการสอนของ AI (หน่วยความจำแบบชั้นที่โหลดจากไฟล์ `GEMINI.md`)
  - **คำสั่งย่อย:**
