# การรวมระบบและการทดสอบ

เอกสารนี้อธิบายกระบวนการทดสอบการรวมระบบสำหรับ Gemini CLI

## ภาพรวม

การทดสอบการรวมระบบของ Gemini CLI รับประกันว่าส่วนประกอบต่างๆ ทำงานร่วมกันอย่างถูกต้องและเครื่องมือทั้งหมดใช้งานได้ตามที่คาดหวัง

## การรันการทดสอบ

การทดสอบการรวมระบบสามารถรันได้โดยใช้:

```bash
npm run test:integration
```

## ชุดการทดสอบ

การทดสอบครอบคลุม:
- การทดสอบระบบไฟล์
- การทดสอบการค้นหาเว็บ Google
- การทดสอบรายการไดเร็กทอรี
- การทดสอบการอ่านไฟล์หลายไฟล์
- การทดสอบการแทนที่
- การทดสอบคำสั่งเชลล์
- การทดสอบหน่วยความจำ
- การทดสอบเซิร์ฟเวอร์ MCP แบบง่าย
- การทดสอบการเขียนไฟล์

## การกำหนดค่าการทดสอบ

การทดสอบต้องการตัวแปรสภาพแวดล้อมต่อไปนี้:
- `GEMINI_API_KEY`: API key สำหรับการเข้าถึง Gemini API
- การตั้งค่าอื่นๆ ที่จำเป็นสำหรับการทดสอบเฉพาะ

## การเขียนการทดสอบใหม่

เมื่อเพิ่มเครื่องมือหรือฟีเจอร์ใหม่ ควรเพิ่มการทดสอบการรวมระบบที่สอดคล้องกัน การทดสอบควร:
- ทดสอบการทำงานปกติ
- ทดสอบการจัดการข้อผิดพลาด
- ตรวจสอบการโต้ตอบกับส่วนประกอบอื่น
