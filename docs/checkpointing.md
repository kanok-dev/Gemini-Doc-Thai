# เช็คพอยต์

Gemini CLI มีฟีเจอร์เช็คพอยต์ที่บันทึกสแนปช็อตของสถานะโครงการของคุณโดยอัตโนมัติก่อนที่เครื่องมือที่ขับเคลื่อนด้วย AI จะทำการแก้ไขไฟล์ใดๆ ทำให้คุณสามารถทดลองและใช้การเปลี่ยนแปลงโค้ดได้อย่างปลอดภัย โดยรู้ว่าคุณสามารถกลับไปสู่สถานะก่อนการรันเครื่องมือได้ทันที

## วิธีการทำงาน

เมื่อคุณอนุมัติเครื่องมือที่แก้ไขระบบไฟล์ (เช่น `write_file` หรือ `replace`) CLI จะสร้าง "เช็คพอยต์" โดยอัตโนมัติ เช็คพอยต์นี้ประกอบด้วย:

1.  **Git Snapshot:** จะทำการ commit ใน Git repository พิเศษที่อยู่ในไดเร็กทอรีโฮมของคุณ (`~/.gemini/history/<project_hash>`) สแนปช็อตนี้จับภาพสถานะทั้งหมดของไฟล์โครงการของคุณในขณะนั้น และ**ไม่**รบกวน Git repository ของโครงการคุณเอง
2.  **ประวัติการสนทนา:** การสนทนาทั้งหมดที่คุณมีกับ agent จนถึงจุดนั้นจะถูกบันทึก
3.  **การเรียกใช้เครื่องมือ:** การเรียกใช้เครื่องมือเฉพาะที่กำลังจะถูกดำเนินการจะถูกเก็บไว้ด้วย

หากคุณต้องการยกเลิกการเปลี่ยนแปลงหรือเพียงแค่ย้อนกลับ คุณสามารถใช้คำสั่ง `/restore` การเรียกคืนเช็คพอยต์จะ:

- คืนไฟล์ทั้งหมดในโครงการของคุณไปสู่สถานะที่จับภาพไว้ในสแนปช็อต
- เรียกคืนประวัติการสนทนาใน CLI
- เสนอการเรียกใช้เครื่องมือเดิมอีกครั้ง ช่วยให้คุณสามารถรันอีกครั้ง แก้ไข หรือเพียงแค่เพิกเฉย

ข้อมูลเช็คพอยต์ทั้งหมด รวมถึง Git snapshot และประวัติการสนทนา จะถูกเก็บไว้ในเครื่องของคุณในเครื่อง Git snapshot จะถูกเก็บใน shadow repository ในขณะที่ประวัติการสนทนาและการเรียกใช้เครื่องมือจะถูกบันทึกในไฟล์ JSON ในไดเร็กทอรีชั่วคราวของโครงการของคุณ โดยทั่วไปจะอยู่ที่ `~/.gemini/tmp/<project_hash>/checkpoints`

## การเปิดใช้งานฟีเจอร์

ฟีเจอร์เช็คพอยต์จะถูกปิดใช้งานโดยดีฟอลต์ เพื่อเปิดใช้งาน คุณสามารถใช้แฟล็กบรรทัดคำสั่งหรือแก้ไขไฟล์ `settings.json` ของคุณ

### การใช้แฟล็กบรรทัดคำสั่ง

คุณสามารถเปิดใช้งานเช็คพอยต์สำหรับเซสชันปัจจุบันโดยใช้แฟล็ก `--checkpointing` เมื่อเริ่มต้น Gemini CLI:

```bash
gemini --checkpointing
```

### การใช้ไฟล์ `settings.json`

เพื่อเปิดใช้งานเช็คพอยต์โดยดีฟอลต์สำหรับเซสชันทั้งหมด คุณต้องแก้ไขไฟล์ `settings.json` ของคุณ

เพิ่ม key ต่อไปนี้ลงใน `settings.json` ของคุณ:

```json
{
  "checkpointing": {
    "enabled": true
  }
}
```

## การใช้คำสั่ง `/restore`

เมื่อเปิดใช้งานแล้ว เช็คพอยต์จะถูกสร้างโดยอัตโนมัติ เพื่อจัดการเช็คพอยต์ คุณใช้คำสั่ง `/restore`

### แสดงรายการเช็คพอยต์ที่มีอยู่

เพื่อดูรายการเช็คพอยต์ที่บันทึกไว้ทั้งหมดสำหรับโครงการปัจจุบัน เพียงรัน:

```
/restore
```

CLI จะแสดงรายการไฟล์เช็คพอยต์ที่มีอยู่ ชื่อไฟล์เหล่านี้โดยทั่วไปจะประกอบด้วยการประทับเวลา ชื่อของไฟล์ที่กำลังถูกแก้ไข และชื่อของเครื่องมือที่กำลังจะถูกรัน (เช่น `2025-06-22T10-00-00_000Z-my-file.txt-write_file`)

### เรียกคืนเช็คพอยต์เฉพาะ

เพื่อเรียกคืนโครงการของคุณไปยังเช็คพอยต์เฉพาะ ใช้ไฟล์เช็คพอยต์จากรายการ:

```
/restore <checkpoint_file>
```

ตัวอย่าง:

```
/restore 2025-06-22T10-00-00_000Z-my-file.txt-write_file
```

หลังจากรันคำสั่ง ไฟล์และการสนทนาของคุณจะถูกเรียกคืนทันทีไปสู่สถานะที่เป็นอยู่เมื่อเช็คพอยต์ถูกสร้าง และพรอมต์เครื่องมือเดิมจะปรากฏขึ้นอีกครั้ง
