# หลัก Gemini CLI

เอกสารนี้ให้ภาพรวมของแพ็คเกจ `packages/core` ซึ่งทำหน้าที่เป็นแบ็กเอนด์สำหรับ Gemini CLI

## ภาพรวม

แพ็คเกจ Core ทำหน้าที่เป็นแบ็กเอนด์สำหรับ Gemini CLI จัดการ:
- การสื่อสารกับ Gemini API
- การดำเนินการเครื่องมือ
- การจัดการเซสชันและสถานะ
- การสร้างและการจัดการพรอมต์

## ส่วนประกอบหลัก

### API Client
จัดการการสื่อสารกับ Google Gemini API รวมถึง:
- การยืนยันตัวตน
- การส่งคำขอ
- การจัดการการตอบสนอง
- การจัดการข้อผิดพลาด

### Tool Manager
จัดการระบบเครื่องมือ:
- การลงทะเบียนเครื่องมือ
- การดำเนินการเครื่องมือ
- การตรวจสอบความปลอดภัย
- การจัดการอนุญาต

### Session Manager
จัดการสถานะเซสชัน:
- ประวัติการสนทนา
- บริบทการสนทนา
- การบันทึกและเรียกคืนสถานะ

### Prompt Manager
จัดการการสร้างและการจัดการพรอมต์:
- การสร้างพรอมต์จากอินพุตผู้ใช้
- การรวมบริบท
- การจัดการประวัติ

## การกำหนดค่า

แพ็คเกจ Core สามารถกำหนดค่าผ่าน:
- ไฟล์ `settings.json`
- ตัวแปรสภาพแวดล้อม
- การตั้งค่าโปรแกรม

## การพัฒนาและการขยาย

สำหรับการพัฒนาขั้นสูง:
- การสร้างเครื่องมือแบบกำหนดเอง
- การขยายฟังก์ชันการทำงาน
- การรวมระบบกับระบบภายนอก
