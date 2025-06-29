# Gemini CLI

[![Gemini CLI CI](https://github.com/google-gemini/gemini-cli/actions/workflows/ci.yml/badge.svg)](https://github.com/google-gemini/gemini-cli/actions/workflows/ci.yml)

![Gemini CLI Screenshot](./docs/assets/gemini-screenshot.png)

Repository นี้ประกอบด้วย Gemini CLI ซึ่งเป็นเครื่องมือ AI workflow บรรทัดคำสั่งที่เชื่อมต่อกับเครื่องมือของคุณ เข้าใจโค้ดของคุณ และเร่งขั้นตอนการทำงานของคุณ

ด้วย Gemini CLI คุณสามารถ:

- สืบค้นและแก้ไข codebase ขนาดใหญ่ในและเกินหน้าต่างบริบท 1M token ของ Gemini
- สร้างแอปใหม่จาก PDF หรือ sketches โดยใช้ความสามารถ multimodal ของ Gemini
- ทำงานปฏิบัติการอัตโนมัติ เช่น การสืบค้น pull requests หรือการจัดการ rebase ที่ซับซ้อน
- ใช้เครื่องมือและ MCP servers เพื่อเชื่อมต่อความสามารถใหม่ รวมถึง [การสร้างสื่อด้วย Imagen, Veo หรือ Lyria](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)
- ยึดคำค้นของคุณด้วยเครื่องมือ [Google Search](https://ai.google.dev/gemini-api/docs/grounding) ที่มีอยู่ใน Gemini

## เริ่มต้นใช้งานอย่างรวดเร็ว

1. **ข้อกำหนดเบื้องต้น:** ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง [Node.js เวอร์ชัน 18](https://nodejs.org/en/download) หรือสูงกว่าแล้ว
2. **เรียกใช้ CLI:** รันคำสั่งต่อไปนี้ในเทอร์มินัลของคุณ:

   ```bash
   npx https://github.com/google-gemini/gemini-cli
   ```

   หรือติดตั้งด้วย:

   ```bash
   npm install -g @google/gemini-cli
   gemini
   ```

3. **เลือกธีมสี**
4. **ยืนยันตัวตน:** เมื่อได้รับพรอมต์ ให้เข้าสู่ระบบด้วยบัญชี Google ส่วนตัวของคุณ ซึ่งจะให้คุณสามารถใช้งานได้สูงสุด 60 คำขอโมเดลต่อนาทีและ 1,000 คำขอโมเดลต่อวันโดยใช้ Gemini

ตอนนี้คุณพร้อมที่จะใช้ Gemini CLI แล้ว!

### สำหรับการใช้งานขั้นสูงหรือขีดจำกัดที่เพิ่มขึ้น:

หากคุณต้องการใช้โมเดลเฉพาะหรือต้องการความจุคำขอที่สูงขึ้น คุณสามารถใช้ API key:

1. สร้าง key จาก [Google AI Studio](https://aistudio.google.com/apikey)
2. ตั้งค่าเป็นตัวแปรสภาพแวดล้อมในเทอร์มินัลของคุณ แทนที่ `YOUR_API_KEY` ด้วย key ที่คุณสร้างขึ้น

   ```bash
   export GEMINI_API_KEY="YOUR_API_KEY"
   ```

สำหรับวิธีการยืนยันตัวตนอื่นๆ รวมถึงบัญชี Google Workspace ดูที่คู่มือ [การยืนยันตัวตน](./docs_thai/cli/authentication.md)

## ตัวอย่าง

เมื่อ CLI ทำงานแล้ว คุณสามารถเริ่มโต้ตอบกับ Gemini จากเชลล์ของคุณ

คุณสามารถเริ่มโครงการจากไดเร็กทอรีใหม่:

```sh
cd new-project/
gemini
> เขียน Gemini Discord bot ที่ตอบคำถามโดยใช้ไฟล์ FAQ.md ที่ฉันจะให้
```

หรือทำงานกับโครงการที่มีอยู่:

```sh
git clone https://github.com/google-gemini/gemini-cli
cd gemini-cli
gemini
> ให้สรุปการเปลี่ยนแปลงทั้งหมดที่เกิดขึ้นเมื่อวาน
```

### ขั้นตอนต่อไป

- เรียนรู้วิธี [มีส่วนร่วมหรือสร้างจากซอร์ส](./CONTRIBUTING.md)
- สำรวจ **[คำสั่ง CLI](./docs_thai/cli/commands.md)** ที่มีอยู่
- หากพบปัญหาใดๆ ให้ดู **[คู่มือแก้ไขปัญหา](./docs_thai/troubleshooting.md)**
- สำหรับเอกสารที่ครอบคลุม ดู [เอกสารฉบับเต็ม](./docs_thai/index.md)
- ดู [งานยอดนิยม](#งานยอดนิยม) เพื่อแรงบันดาลใจเพิ่มเติม

### การแก้ไขปัญหา

ไปที่คู่มือ [การแก้ไขปัญหา](docs_thai/troubleshooting.md) หากคุณ
กำลังประสบปัญหา

## งานยอดนิยม

### สำรวจ codebase ใหม่

เริ่มต้นด้วยการ `cd` เข้าไปใน repository ที่มีอยู่หรือ clone ใหม่ และรัน `gemini`

```text
> อธิบายส่วนหลักของสถาปัตยกรรมระบบนี้
```

```text
> มีกลไกความปลอดภัยใดบ้างที่มีอยู่?
```

### ทำงานกับโค้ดที่มีอยู่

```text
> ทำ first draft สำหรับ GitHub issue #123
```

```text
> ช่วยฉัน migrate codebase นี้ไปยัง Java เวอร์ชันล่าสุด เริ่มด้วยแผน
```

### ทำงานอัตโนมัติ

ใช้ MCP servers เพื่อรวมเครื่องมือระบบในเครื่องของคุณเข้ากับชุดการทำงานร่วมกันขององค์กร

```text
> ทำสไลด์แสดงประวัติ git จาก 7 วันที่ผ่านมา จัดกลุ่มตามฟีเจอร์และสมาชิกทีม
```

```text
> ทำเว็บแอปเต็มหน้าจอสำหรับการแสดงผลบนผนัง เพื่อแสดง GitHub issues ที่มีการโต้ตอบมากที่สุด
```

### โต้ตอบกับระบบของคุณ

```text
> แปลงรูปภาพทั้งหมดในไดเร็กทอรีนี้เป็น png และเปลี่ยนชื่อให้ใช้วันที่จากข้อมูล exif
```

```text
> จัดระเบียบใบแจ้งหนี้ PDF ของฉันตามเดือนของการใช้จ่าย
```

## ข้อกำหนดการใช้บริการและประกาศความเป็นส่วนตัว

สำหรับรายละเอียดเกี่ยวกับข้อกำหนดการใช้บริการและประกาศความเป็นส่วนตัวที่ใช้กับการใช้งาน Gemini CLI ของคุณ ดูที่ [ข้อกำหนดการใช้บริการและประกาศความเป็นส่วนตัว](./docs_thai/tos-privacy.md)
