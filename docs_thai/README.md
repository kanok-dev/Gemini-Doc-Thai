# README - เอกสารไทย Gemini CLI

เอกสารนี้ให้ภาพรวมของเอกสารภาษาไทยสำหรับ Gemini CLI

## ภาพรวม

โฟลเดอร์ `docs_thai` มีเอกสารประกอบ Gemini CLI ที่แปลเป็นภาษาไทย เพื่อให้ผู้ใช้ชาวไทยสามารถเข้าใจและใช้งาน Gemini CLI ได้อย่างมีประสิทธิภาพ

## 📖 README หลัก
- **[README_MAIN.md](./README_MAIN.md)** - README หลักที่แปลเป็นภาษาไทย (แปลจาก README.md ในรูท)

## โครงสร้างเอกสาร

### เอกสารหลัก
- **[index.md](./index.md)** - หน้าหลักและภาพรวมของเอกสาร
- **[architecture.md](./architecture.md)** - สถาปัตยกรรมของ Gemini CLI
- **[deployment.md](./deployment.md)** - คู่มือการติดตั้งและการปรับใช้
- **[checkpointing.md](./checkpointing.md)** - ระบบ checkpoint สำหรับการกู้คืน
- **[extension.md](./extension.md)** - การพัฒนาและใช้งานส่วนขยาย
- **[integration-tests.md](./integration-tests.md)** - การทดสอบการรวมระบบ
- **[sandbox.md](./sandbox.md)** - ระบบ sandbox เพื่อความปลอดภัย
- **[telemetry.md](./telemetry.md)** - การรวบรวมข้อมูลเทเลเมทรี
- **[tos-privacy.md](./tos-privacy.md)** - ข้อกำหนดและนโยบายความเป็นส่วนตัว
- **[troubleshooting.md](./troubleshooting.md)** - คู่มือแก้ไขปัญหา

### เอกสาร CLI
- **[cli/index.md](./cli/index.md)** - ภาพรวมของ CLI
- **[cli/authentication.md](./cli/authentication.md)** - การตั้งค่าการยืนยันตัวตน
- **[cli/commands.md](./cli/commands.md)** - คำสั่งที่มีอยู่ใน CLI
- **[cli/configuration.md](./cli/configuration.md)** - การกำหนดค่า CLI
- **[cli/themes.md](./cli/themes.md)** - การปรับแต่งธีม
- **[cli/token-caching.md](./cli/token-caching.md)** - การแคชโทเค็น
- **[cli/tutorials.md](./cli/tutorials.md)** - บทช่วยสอนการใช้งาน

### เอกสาร Core
- **[core/index.md](./core/index.md)** - ภาพรวมของแพ็คเกจ Core
- **[core/tools-api.md](./core/tools-api.md)** - API สำหรับเครื่องมือ

### เอกสารเครื่องมือ
- **[tools/index.md](./tools/index.md)** - ภาพรวมเครื่องมือทั้งหมด
- **[tools/file-system.md](./tools/file-system.md)** - เครื่องมือระบบไฟล์
- **[tools/multi-file.md](./tools/multi-file.md)** - เครื่องมืออ่านหลายไฟล์
- **[tools/shell.md](./tools/shell.md)** - เครื่องมือเชลล์
- **[tools/memory.md](./tools/memory.md)** - เครื่องมือหน่วยความจำ

### ไฟล์สื่อ
- **[assets/](./assets/)** - รูปภาพและไฟล์สื่ออื่นๆ (คัดลอกจากเอกสารต้นฉบับ)

## วิธีการใช้งานเอกสาร

### การเริ่มต้น
1. เริ่มต้นที่ [index.md](./index.md) เพื่อดูภาพรวม
2. อ่าน [deployment.md](./deployment.md) สำหรับการติดตั้ง
3. ดู [cli/authentication.md](./cli/authentication.md) สำหรับการตั้งค่าเริ่มต้น

### การเรียนรู้เพิ่มเติม
- อ่าน [cli/tutorials.md](./cli/tutorials.md) สำหรับตัวอย่างการใช้งาน
- ศึกษา [tools/index.md](./tools/index.md) เพื่อเข้าใจเครื่องมือต่างๆ
- ดู [cli/commands.md](./cli/commands.md) สำหรับคำสั่งที่มีอยู่

### การแก้ไขปัญหา
- ใช้ [troubleshooting.md](./troubleshooting.md) เมื่อพบปัญหา
- ตรวจสอบ [cli/configuration.md](./cli/configuration.md) สำหรับการตั้งค่า

## การปรับปรุงเอกสาร

### การมีส่วนร่วม
เอกสารนี้เป็นการแปลจากเอกสารต้นฉบับภาษาอังกฤษ หากพบข้อผิดพลาดหรือต้องการปรับปรุง สามารถ:
- สร้าง issue ใน GitHub repository
- ส่ง pull request สำหรับการแก้ไข
- แนะนำการปรับปรุงผ่านชุมชน

### การอัปเดต
เอกสารจะได้รับการอัปเดตเมื่อมีการเปลี่ยนแปลงในเอกสารต้นฉบับ

## การสนับสนุน

### ช่องทางการช่วยเหลือ
- GitHub Repository: https://github.com/google-gemini/gemini-cli
- เอกสารต้นฉบับ: [../docs/](../docs/)
- ชุมชนผู้ใช้งาน Gemini CLI

### ภาษาอื่นๆ
- เอกสารภาษาอังกฤษ: [../docs/](../docs/)

---

**หมายเหตุ**: เอกสารนี้เป็นการแปลจากเอกสารต้นฉบับภาษาอังกฤษ หากมีข้อสงสัยหรือต้องการข้อมูลล่าสุด กรุณาอ้างอิงเอกสารต้นฉบับ
