# การดำเนินการและการปรับใช้ Gemini CLI

เอกสารนี้อธิบายวิธีการเรียกใช้ Gemini CLI และอธิบายสถาปัตยกรรมการปรับใช้ที่ Gemini CLI ใช้

## การเรียกใช้ Gemini CLI

มีหลายวิธีในการเรียกใช้ Gemini CLI ตัวเลือกที่คุณเลือกขึ้นอยู่กับวิธีที่คุณตั้งใจจะใช้ Gemini CLI

---

### 1. การติดตั้งมาตรฐาน (แนะนำสำหรับผู้ใช้ทั่วไป)

นี่เป็นวิธีที่แนะนำสำหรับผู้ใช้ปลายทางในการติดตั้ง Gemini CLI ซึ่งเกี่ยวข้องกับการดาวน์โหลดแพ็คเกจ Gemini CLI จาก NPM registry

- **การติดตั้งแบบ Global:**

  ```bash
  # ติดตั้ง CLI แบบ global
  npm install -g @google/gemini-cli

  # ตอนนี้คุณสามารถเรียกใช้ CLI จากทุกที่
  gemini
  ```

- **การดำเนินการ NPX:**
  ```bash
  # ดำเนินการเวอร์ชันล่าสุดจาก NPM โดยไม่ต้องติดตั้งแบบ global
  npx @google/gemini-cli
  ```

---

### 2. การเรียกใช้ใน sandbox (Docker/Podman)

เพื่อความปลอดภัยและการแยกออก Gemini CLI สามารถเรียกใช้ภายในคอนเทนเนอร์ได้ นี่เป็นวิธีเริ่มต้นที่ CLI ดำเนินการเครื่องมือที่อาจมีผลข้างเคียง

- **โดยตรงจาก Registry:**
  คุณสามารถเรียกใช้ sandbox image ที่เผยแพร่โดยตรง นี่มีประโยชน์สำหรับสภาพแวดล้อมที่คุณมีเพียง Docker และต้องการเรียกใช้ CLI
  ```bash
  # เรียกใช้ sandbox image ที่เผยแพร่
  docker run --rm -it us-docker.pkg.dev/gemini-code-dev/gemini-cli/sandbox:0.1.1
  ```
- **การใช้แฟล็ก `--sandbox`:**
  หากคุณมี Gemini CLI ติดตั้งในเครื่อง (โดยใช้การติดตั้งมาตรฐานที่อธิบายข้างต้น) คุณสามารถสั่งให้เรียกใช้ภายในคอนเทนเนอร์ sandbox
  ```bash
  gemini --sandbox "your prompt here"
  ```

---

### 3. การเรียกใช้จากซอร์ส (แนะนำสำหรับผู้มีส่วนร่วม Gemini CLI)

ผู้มีส่วนร่วมในโครงการจะต้องการเรียกใช้ CLI โดยตรงจากซอร์สโค้ด

- **โหมดการพัฒนา:**
  วิธีนี้ให้การ hot-reloading และมีประโยชน์สำหรับการพัฒนาที่ใช้งานอยู่
  ```bash
  # จากรูทของ repository
  npm run start
  ```
- **โหมดที่คล้ายกับ Production (Linked package):**
  วิธีนี้จำลองการติดตั้งแบบ global โดยการลิงค์แพ็คเกจในเครื่องของคุณ มีประโยชน์สำหรับการทดสอบ local build ในเวิร์กโฟลว์ production

  ```bash
  # ลิงค์แพ็คเกจ cli ในเครื่องไปยัง global node_modules ของคุณ
  npm link packages/cli

  # ตอนนี้คุณสามารถเรียกใช้เวอร์ชันในเครื่องของคุณโดยใช้คำสั่ง `gemini`
  gemini
  ```

---

### 4. การเรียกใช้ commit ล่าสุดของ Gemini CLI จาก GitHub

คุณสามารถเรียกใช้เวอร์ชันที่ commit ล่าสุดของ Gemini CLI โดยตรงจาก GitHub repository นี่มีประโยชน์สำหรับการทดสอบฟีเจอร์ที่ยังอยู่ในการพัฒนา

```bash
# ดำเนินการ CLI โดยตรงจาก main branch บน GitHub
npx https://github.com/google-gemini/gemini-cli
```

## สถาปัตยกรรมการปรับใช้

วิธีการดำเนินการที่อธิบายข้างต้นเป็นไปได้ด้วยองค์ประกอบและกระบวนการทางสถาปัตยกรรมต่อไปนี้:

**แพ็คเกจ NPM**

โครงการ Gemini CLI เป็น monorepo ที่เผยแพร่แพ็คเกจหลักสองตัวไปยัง NPM registry:

- `@google/gemini-cli-core`: แบ็กเอนด์ จัดการตรรกะและการดำเนินการเครื่องมือ
- `@google/gemini-cli`: ฟรอนต์เอนด์สำหรับผู้ใช้

แพ็คเกจเหล่านี้ใช้เมื่อทำการติดตั้งมาตรฐานและเมื่อเรียกใช้ Gemini CLI จากซอร์ส

**กระบวนการสร้างและแพ็คเกจ**

มีกระบวนการสร้างที่แตกต่างกันสองแบบที่ใช้ ขึ้นอยู่กับช่องทางการจัดจำหน่าย:

- **การเผยแพร่ NPM:** สำหรับการเผยแพร่ไปยัง NPM registry ซอร์สโค้ด TypeScript ใน `@google/gemini-cli-core` และ `@google/gemini-cli` จะถูก transpile เป็น JavaScript มาตรฐานโดยใช้ TypeScript Compiler (`tsc`) ไดเร็กทอรี `dist/` ที่เป็นผลลัพธ์คือสิ่งที่ได้รับการเผยแพร่ในแพ็คเกจ NPM นี่เป็นแนวทางมาตรฐานสำหรับไลบรารี TypeScript

- **การดำเนินการ GitHub `npx`:** เมื่อเรียกใช้เวอร์ชันล่าสุดของ Gemini CLI โดยตรงจาก GitHub กระบวนการที่แตกต่างจะถูกเรียกใช้โดยสคริปต์ `prepare` ใน `package.json` สคริปต์นี้ใช้ `esbuild` เพื่อรวมแอปพลิเคชันทั้งหมดและ dependencies เป็นไฟล์ JavaScript เดียวที่ครบถ้วนในตัวเอง bundle นี้จะถูกสร้างขึ้นทันทีบนเครื่องของผู้ใช้และไม่ได้ถูก check เข้าสู่ repository

**Docker sandbox image**

วิธีการดำเนินการที่ใช้ Docker ได้รับการสนับสนุนโดย container image `gemini-cli-sandbox` image นี้ถูกเผยแพร่ไปยัง container registry และมี Gemini CLI เวอร์ชันที่ติดตั้งแบบ global ไว้ล่วงหน้า สคริปต์ `scripts/prepare-cli-packagejson.js` จะฉีด URI ของ image นี้เข้าไปใน `package.json` ของ CLI แบบไดนามิกก่อนการเผยแพร่ เพื่อให้ CLI ทราบว่าควรดึง image ใดเมื่อใช้แฟล็ก `--sandbox`

## กระบวนการ Release

สคริปต์แบบรวม `npm run publish:release` จัดระเบียบกระบวนการ release สคริปต์ดำเนินการต่อไปนี้:

1.  สร้างแพ็คเกจ NPM โดยใช้ `tsc`
2.  อัปเดต `package.json` ของ CLI ด้วย Docker image URI
3.  สร้างและแท็ก Docker image `gemini-cli-sandbox`
4.  Push Docker image ไปยัง container registry
5.  เผยแพร่แพ็คเกจ NPM ไปยัง artifact registry
