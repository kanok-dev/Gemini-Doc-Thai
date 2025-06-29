# การกำหนดค่า Gemini CLI

Gemini CLI มีหลายวิธีในการกำหนดค่าพฤติกรรม รวมถึงตัวแปรสภาพแวดล้อม อาร์กิวเมนต์บรรทัดคำสั่ง และไฟล์การตั้งค่า เอกสารนี้อธิบายวิธีการกำหนดค่าที่แตกต่างกันและการตั้งค่าที่มีอยู่

## ชั้นการกำหนดค่า

การกำหนดค่าจะถูกนำไปใช้ตามลำดับความสำคัญต่อไปนี้ (หมายเลขที่ต่ำกว่าจะถูกแทนที่ด้วยหมายเลขที่สูงกว่า):

1.  **ค่าดีฟอลต์:** ค่าดีฟอลต์ที่ฮาร์ดโค้ดภายในแอปพลิเคชัน
2.  **ไฟล์การตั้งค่าผู้ใช้:** การตั้งค่าทั่วไปสำหรับผู้ใช้ปัจจุบัน
3.  **ไฟล์การตั้งค่าโครงการ:** การตั้งค่าเฉพาะโครงการ
4.  **ตัวแปรสภาพแวดล้อม:** ตัวแปรทั้งระบบหรือเฉพาะเซสชัน อาจโหลดจากไฟล์ `.env`
5.  **อาร์กิวเมนต์บรรทัดคำสั่ง:** ค่าที่ส่งผ่านเมื่อเปิด CLI

## ไฟล์การตั้งค่าผู้ใช้และไฟล์การตั้งค่าโครงการ

Gemini CLI ใช้ไฟล์ `settings.json` สำหรับการกำหนดค่าแบบถาวร มีสองตำแหน่งสำหรับไฟล์เหล่านี้:

- **ไฟล์การตั้งค่าผู้ใช้:**
  - **ตำแหน่ง:** `~/.gemini/settings.json` (โดยที่ `~` คือไดเร็กทอรีโฮมของคุณ)
  - **ขอบเขต:** ใช้กับเซสชัน Gemini CLI ทั้งหมดสำหรับผู้ใช้ปัจจุบัน
- **ไฟล์การตั้งค่าโครงการ:**
  - **ตำแหน่ง:** `.gemini/settings.json` ภายในไดเร็กทอรีรูทของโครงการ
  - **ขอบเขต:** ใช้เฉพาะเมื่อเรียกใช้ Gemini CLI จากโครงการเฉพาะนั้น การตั้งค่าโครงการจะแทนที่การตั้งค่าผู้ใช้

**หมายเหตุเกี่ยวกับตัวแปรสภาพแวดล้อมในการตั้งค่า:** ค่าสตริงภายในไฟล์ `settings.json` ของคุณสามารถอ้างอิงตัวแปรสภาพแวดล้อมโดยใช้ไวยากรณ์ `$VAR_NAME` หรือ `${VAR_NAME}` ตัวแปรเหล่านี้จะถูกแก้ไขโดยอัตโนมัติเมื่อโหลดการตั้งค่า ตัวอย่าง หากคุณมีตัวแปรสภาพแวดล้อม `MY_API_TOKEN` คุณสามารถใช้ใน `settings.json` แบบนี้: `"apiKey": "$MY_API_TOKEN"`

### ไดเร็กทอรี `.gemini` ในโครงการของคุณ

นอกจากไฟล์การตั้งค่าโครงการแล้ว ไดเร็กทอรี `.gemini` ของโครงการยังสามารถมีไฟล์เฉพาะโครงการอื่นๆ ที่เกี่ยวข้องกับการทำงานของ Gemini CLI เช่น:

- [โปรไฟล์ sandbox แบบกำหนดเอง](#sandboxing) (เช่น `.gemini/sandbox-macos-custom.sb`, `.gemini/sandbox.Dockerfile`)

### การตั้งค่าที่มีอยู่ใน `settings.json`:

- **`contextFileName`** (string หรือ array ของ strings):
  - **คำอธิบาย:** ระบุชื่อไฟล์สำหรับไฟล์บริบท (เช่น `GEMINI.md`, `AGENTS.md`) สามารถเป็นชื่อไฟล์เดียวหรือรายการชื่อไฟล์ที่ยอมรับ
  - **ดีฟอลต์:** `GEMINI.md`
  - **ตัวอย่าง:** `"contextFileName": "AGENTS.md"`

- **`bugCommand`** (object):
  - **คำอธิบาย:** แทนที่ URL ดีฟอลต์สำหรับคำสั่ง `/bug`
  - **ดีฟอลต์:** `"urlTemplate": "https://github.com/google-gemini/gemini-cli/issues/new?template=bug_report.yml&title={title}&info={info}"`
  - **คุณสมบัติ:**
    - **`urlTemplate`** (string): URL ที่สามารถมี placeholders `{title}` และ `{info}`
  - **ตัวอย่าง:**
    ```json
    "bugCommand": {
      "urlTemplate": "https://bug.example.com/new?title={title}&info={info}"
    }
    ```

- **`fileFiltering`** (object):
  - **คำอธิบาย:** ควบคุมพฤติกรรมการกรองไฟล์ที่รู้เกี่ยวกับ git สำหรับคำสั่ง @ และเครื่องมือค้นหาไฟล์
  - **ดีฟอลต์:** `"respectGitIgnore": true, "enableRecursiveFileSearch": true`
  - **คุณสมบัติ:**
    - **`respectGitIgnore`** (boolean): ว่าจะเคารพรูปแบบ .gitignore เมื่อค้นพบไฟล์หรือไม่ เมื่อตั้งเป็น `true` ไฟล์ที่ git ละเว้น (เช่น `node_modules/`, `dist/`, `.env`) จะถูกแยกออกจากคำสั่ง @ และการดำเนินการรายการไฟล์โดยอัตโนมัติ
    - **`enableRecursiveFileSearch`** (boolean): ว่าจะเปิดใช้งานการค้นหาแบบ recursive สำหรับชื่อไฟล์ภายใต้ tree ปัจจุบันเมื่อทำให้สมบูรณ์คำนำหน้า @ ในพรอมต์หรือไม่
  - **ตัวอย่าง:**
    ```json
    "fileFiltering": {
      "respectGitIgnore": true,
      "enableRecursiveFileSearch": false
    }
    ```

- **`coreTools`** (array ของ strings):
  - **คำอธิบาย:** ช่วยให้คุณระบุรายการชื่อเครื่องมือหลักที่ควรมีให้กับโมเดล สามารถใช้เพื่อจำกัดชุดเครื่องมือที่มีอยู่ในตัว ดู [เครื่องมือที่มีอยู่ในตัว](../core/tools-api.md#built-in-tools) สำหรับรายการเครื่องมือหลัก
  - **ดีฟอลต์:** เครื่องมือทั้งหมดที่มีอยู่สำหรับใช้โดยโมเดล Gemini
  - **ตัวอย่าง:** `"coreTools": ["ReadFileTool", "GlobTool", "SearchText"]`

- **`excludeTools`** (array ของ strings):
  - **คำอธิบาย:** ช่วยให้คุณระบุรายการชื่อเครื่องมือหลักที่ควรแยกออกจากโมเดล เครื่องมือที่ระบุทั้งใน `excludeTools` และ `coreTools` จะถูกแยกออก
  - **ดีฟอลต์**: ไม่มีเครื่องมือที่แยกออก
  - **ตัวอย่าง:** `"excludeTools": ["run_shell_command", "findFiles"]`

- **`autoAccept`** (boolean):
  - **คำอธิบาย:** ควบคุมว่า CLI จะยอมรับและดำเนินการเรียกใช้เครื่องมือที่ถือว่าปลอดภัย (เช่น การดำเนินการแบบอ่านอย่างเดียว) โดยไม่ต้องได้รับการยืนยันจากผู้ใช้อย่างชัดเจนหรือไม่ หากตั้งเป็น `true` CLI จะข้ามพรอมต์การยืนยันสำหรับเครื่องมือที่ถือว่าปลอดภัย
  - **ดีฟอลต์:** `false`
  - **ตัวอย่าง:** `"autoAccept": true`

- **`theme`** (string):
  - **คำอธิบาย:** ตั้งค่า[ธีม](./themes.md)ภาพสำหรับ Gemini CLI
  - **ดีฟอลต์:** `"Default"`
  - **ตัวอย่าง:** `"theme": "GitHub"`

- **`sandbox`** (boolean หรือ string):
  - **คำอธิบาย:** ควบคุมว่าจะใช้และใช้ sandbox อย่างไรสำหรับการดำเนินการเครื่องมือ หากตั้งเป็น `true` Gemini CLI จะใช้ Docker image `gemini-cli-sandbox` ที่สร้างไว้ล่วงหน้า สำหรับข้อมูลเพิ่มเติม ดู [Sandboxing](#sandboxing)
  - **ดีฟอลต์:** `false`
  - **ตัวอย่าง:** `"sandbox": "docker"`

- **`toolDiscoveryCommand`** (string):
  - **คำอธิบาย:** กำหนดคำสั่งเชลล์แบบกำหนดเองสำหรับค้นพบเครื่องมือจากโครงการของคุณ คำสั่งเชลล์ต้องส่งคืน JSON array ของ [function declarations](https://ai.google.dev/gemini-api/docs/function-calling#function-declarations) บน `stdout` Tool wrappers เป็นตัวเลือก
  - **ดีฟอลต์:** ว่าง
  - **ตัวอย่าง:** `"toolDiscoveryCommand": "bin/get_tools"`

- **`toolCallCommand`** (string):
  - **คำอธิบาย:** กำหนดคำสั่งเชลล์แบบกำหนดเองสำหรับเรียกใช้เครื่องมือเฉพาะที่ค้นพบโดยใช้ `toolDiscoveryCommand` คำสั่งเชลล์ต้องตรงตามเกณฑ์ต่อไปนี้:
    - ต้องรับ function `name` (เหมือนกับใน [function declaration](https://ai.google.dev/gemini-api/docs/function-calling#function-declarations)) เป็นอาร์กิวเมนต์บรรทัดคำสั่งแรก
    - ต้องอ่าน function arguments เป็น JSON บน `stdin` คล้ายกับ [`functionCall.args`](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#functioncall)
