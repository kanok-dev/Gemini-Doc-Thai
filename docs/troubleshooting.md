# คู่มือการแก้ไขปัญหา

คู่มือนี้ให้การแก้ไขปัญหาทั่วไปและเคล็ดลับการดีบัก

## การยืนยันตัวตน

- **ข้อผิดพลาด: `Failed to login. Message: Request contains an invalid argument`**
  - ผู้ใช้ที่มีบัญชี Google Workspace หรือผู้ใช้ที่มีบัญชี Google Cloud ที่เชื่อมโยงกับบัญชี Gmail อาจไม่สามารถเปิดใช้งานฟรีทิชิมของแผน Google Code Assist
  - สำหรับบัญชี Google Cloud คุณสามารถแก้ไขได้โดยตั้งค่า `GOOGLE_CLOUD_PROJECT` เป็น project ID ของคุณ
  - คุณยังสามารถหา API key จาก [AI Studio](http://aistudio.google.com/app/apikey) ซึ่งรวมถึงฟรีทิชิมแยกต่างหาก

## คำถามที่พบบ่อย (FAQs)

- **Q: ฉันจะอัปเดต Gemini CLI เป็นเวอร์ชันล่าสุดได้อย่างไร?**
  - A: หากติดตั้งแบบ global ผ่าน npm อัปเดต Gemini CLI โดยใช้คำสั่ง `npm install -g @google/gemini-cli@latest` หากรันจากซอร์ส ดึงการเปลี่ยนแปลงล่าสุดจาก repository และสร้างใหม่โดยใช้ `npm run build`

- **Q: ไฟล์การกำหนดค่า Gemini CLI เก็บไว้ที่ไหน?**
  - A: การกำหนดค่า CLI เก็บไว้ในไฟล์ `settings.json` สองไฟล์: หนึ่งในไดเร็กทอรีโฮมของคุณและหนึ่งในไดเร็กทอรีรูทของโครงการ ในทั้งสองตำแหน่ง `settings.json` อยู่ในโฟลเดอร์ `.gemini/` ดูที่ [การกำหนดค่า CLI](./cli/configuration.md) สำหรับรายละเอียดเพิ่มเติม

- **Q: ทำไมฉันไม่เห็นจำนวนโทเค็นที่แคชในผลลัพธ์สถิติ?**
  - A: ข้อมูลโทเค็นที่แคชจะแสดงเฉพาะเมื่อมีการใช้โทเค็นที่แคช ฟีเจอร์นี้ใช้ได้สำหรับผู้ใช้ API key (Gemini API key หรือ Vertex AI) แต่ไม่ใช่สำหรับผู้ใช้ OAuth (บัญชี Google Personal/Enterprise) ในขณะนี้ เนื่องจาก Code Assist API ไม่รองรับการสร้างเนื้อหาแคช คุณยังคงสามารถดูการใช้โทเค็นทั้งหมดด้วยคำสั่ง `/stats`

## ข้อความข้อผิดพลาดทั่วไปและการแก้ไข

- **ข้อผิดพลาด: `EADDRINUSE` (Address already in use) เมื่อเริ่มต้นเซิร์ฟเวอร์ MCP**
  - **สาเหตุ:** กระบวนการอื่นกำลังใช้พอร์ตที่เซิร์ฟเวอร์ MCP พยายามผูกไว้อยู่แล้ว
  - **การแก้ไข:**
    หยุดกระบวนการอื่นที่ใช้พอร์ตหรือกำหนดค่าเซิร์ฟเวอร์ MCP ให้ใช้พอร์ตอื่น

- **ข้อผิดพลาด: Command not found (เมื่อพยายามรัน Gemini CLI)**
  - **สาเหตุ:** Gemini CLI ไม่ได้ติดตั้งอย่างถูกต้องหรือไม่อยู่ใน PATH ของระบบ
  - **การแก้ไข:**
    1.  ตรวจสอบว่าการติดตั้ง Gemini CLI สำเร็จ
    2.  หากติดตั้งแบบ global ตรวจสอบว่าไดเร็กทอรี npm global binary อยู่ใน PATH ของคุณ
    3.  หากรันจากซอร์ส ตรวจสอบว่าคุณใช้คำสั่งที่ถูกต้องในการเรียกใช้ (เช่น `node packages/cli/dist/index.js ...`)

- **ข้อผิดพลาด: `MODULE_NOT_FOUND` หรือข้อผิดพลาด import**
  - **สาเหตุ:** Dependencies ไม่ได้ติดตั้งอย่างถูกต้อง หรือโครงการยังไม่ได้ถูกสร้าง
  - **การแก้ไข:**
    1.  รัน `npm install` เพื่อให้แน่ใจว่า dependencies ทั้งหมดมีอยู่
    2.  รัน `npm run build` เพื่อคอมไพล์โครงการ

- **ข้อผิดพลาด: "Operation not permitted", "Permission denied" หรือคล้ายกัน**
  - **สาเหตุ:** หากเปิดใช้งาน sandboxing แอปพลิเคชันอาจพยายามทำการดำเนินการที่ถูกจำกัดโดย sandbox ของคุณ เช่น การเขียนนอกไดเร็กทอรีโครงการหรือไดเร็กทอรี temp ของระบบ
  - **การแก้ไข:** ดู [Sandboxing](./cli/configuration.md#sandboxing) สำหรับข้อมูลเพิ่มเติม รวมถึงวิธีปรับแต่งการกำหนดค่า sandbox ของคุณ
