## การตั้งค่าการยืนยันตัวตน

Gemini CLI ต้องการให้คุณยืนยันตัวตนกับบริการ AI ของ Google เมื่อเริ่มต้นครั้งแรก คุณจะต้องกำหนดค่า **หนึ่ง** ในวิธีการยืนยันตัวตนต่อไปนี้:

1.  **เข้าสู่ระบบด้วย Google (Gemini Code Assist):**
    - ใช้ตัวเลือกนี้เพื่อเข้าสู่ระบบด้วยบัญชี Google ของคุณ
    - ระหว่างการเริ่มต้นครั้งแรก Gemini CLI จะนำคุณไปยังเว็บเพจสำหรับการยืนยันตัวตน เมื่อยืนยันตัวตนแล้ว ข้อมูลประจำตัวของคุณจะถูกแคชในเครื่องเพื่อให้สามารถข้ามการเข้าสู่ระบบผ่านเว็บในการรันครั้งต่อไป
    - โปรดทราบว่าการเข้าสู่ระบบผ่านเว็บต้องทำในเบราว์เซอร์ที่สามารถสื่อสารกับเครื่องที่รัน Gemini CLI (โดยเฉพาะ เบราว์เซอร์จะถูกเปลี่ยนเส้นทางไปยัง localhost url ที่ Gemini CLI จะรอฟัง)
    - <a id="workspace-gca">ผู้ใช้อาจต้องระบุ GOOGLE_CLOUD_PROJECT หาก:</a>
      1. คุณมีบัญชี Google Workspace Google Workspace เป็นบริการแบบชำระเงินสำหรับธุรกิจและองค์กรที่มีเครื่องมือการทำงานแบบครบครัน รวมถึงโดเมนอีเมลที่กำหนดเอง (เช่น your-name@your-company.com) ฟีเจอร์ความปลอดภัยที่เพิ่มขึ้น และการควบคุมการจัดการ บัญชีเหล่านี้มักจัดการโดยนายจ้างหรือโรงเรียน
      1. คุณได้รับใบอนุญาต Code Assist ฟรีผ่าน [Google Developer Program](https://developers.google.com/program/plans-and-pricing) (รวมถึง Google Developer Experts ที่มีคุณสมบัติ)
      1. คุณได้รับการมอบหมายใบอนุญาตให้กับการสมัครสมาชิก Gemini Code Assist standard หรือ enterprise ปัจจุบัน
      1. คุณใช้ผลิตภัณฑ์นอก[ภูมิภาคที่รองรับ](https://developers.google.com/gemini-code-assist/resources/available-locations) สำหรับการใช้งานส่วนบุคคลฟรี
      1. คุณเป็นผู้ถือบัญชี Google ที่อายุต่ำกว่า 18 ปี
      - หากคุณอยู่ในหมวดหมู่หนึ่งเหล่านี้ คุณต้องกำหนดค่า Google Cloud Project Id ที่จะใช้เสียก่อน [เปิดใช้งาน Gemini for Cloud API](https://cloud.google.com/gemini/docs/discover/set-up-gemini#enable-api) และ [กำหนดค่าการอนุญาตการเข้าถึง](https://cloud.google.com/gemini/docs/discover/set-up-gemini#grant-iam)

      คุณสามารถตั้งค่าตัวแปรสภาพแวดล้อมชั่วคราวในเซสชันเชลล์ปัจจุบันของคุณโดยใช้คำสั่งต่อไปนี้:

      ```bash
      export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"
      ```
      - สำหรับการใช้งานซ้ำ คุณสามารถเพิ่มตัวแปรสภาพแวดล้อมไปยังไฟล์ `.env` ของคุณ (อยู่ในไดเร็กทอรีโครงการหรือไดเร็กทอรีโฮมของผู้ใช้) หรือไฟล์การกำหนดค่าของเชลล์ (เช่น `~/.bashrc`, `~/.zshrc` หรือ `~/.profile`) ตัวอย่าง คำสั่งต่อไปนี้เพิ่มตัวแปรสภาพแวดล้อมไปยังไฟล์ `~/.bashrc`:

      ```bash
      echo 'export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"' >> ~/.bashrc
      source ~/.bashrc
      ```

2.  **<a id="gemini-api-key"></a>Gemini API key:**
    - รับ API key ของคุณจาก Google AI Studio: [https://aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
    - ตั้งค่าตัวแปรสภาพแวดล้อม `GEMINI_API_KEY` ในวิธีการต่อไปนี้ แทนที่ `YOUR_GEMINI_API_KEY` ด้วย API key ที่คุณได้รับจาก Google AI Studio:
      - คุณสามารถตั้งค่าตัวแปรสภาพแวดล้อมชั่วคราวในเซสชันเชลล์ปัจจุบันของคุณโดยใช้คำสั่งต่อไปนี้:
        ```bash
        export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
        ```
      - สำหรับการใช้งานซ้ำ คุณสามารถเพิ่มตัวแปรสภาพแวดล้อมไปยังไฟล์ `.env` ของคุณ (อยู่ในไดเร็กทอรีโครงการหรือไดเร็กทอรีโฮมของผู้ใช้) หรือไฟล์การกำหนดค่าของเชลล์ (เช่น `~/.bashrc`, `~/.zshrc` หรือ `~/.profile`) ตัวอย่าง คำสั่งต่อไปนี้เพิ่มตัวแปรสภาพแวดล้อมไปยังไฟล์ `~/.bashrc`:
        ```bash
        echo 'export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"' >> ~/.bashrc
        source ~/.bashrc
        ```

3.  **Vertex AI:**
    - หากไม่ใช้โหมด express:
      - ตรวจสอบว่าคุณมีโครงการ Google Cloud และได้เปิดใช้งาน Vertex AI API แล้ว
      - ตั้งค่า Application Default Credentials (ADC) โดยใช้คำสั่งต่อไปนี้:
        ```bash
        gcloud auth application-default login
        ```
        สำหรับข้อมูลเพิ่มเติม ดูที่ [ตั้งค่า Application Default Credentials สำหรับ Google Cloud](https://cloud.google.com/docs/authentication/provide-credentials-adc)
      - ตั้งค่าตัวแปรสภาพแวดล้อม `GOOGLE_CLOUD_PROJECT`, `GOOGLE_CLOUD_LOCATION` และ `GOOGLE_GENAI_USE_VERTEXAI` ในวิธีการต่อไปนี้ แทนที่ `YOUR_PROJECT_ID` และ `YOUR_PROJECT_LOCATION` ด้วยค่าที่เกี่ยวข้องสำหรับโครงการของคุณ:
        - คุณสามารถตั้งค่าตัวแปรสภาพแวดล้อมเหล่านี้ชั่วคราวในเซสชันเชลล์ปัจจุบันของคุณโดยใช้คำสั่งต่อไปนี้:
          ```bash
          export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"
          export GOOGLE_CLOUD_LOCATION="YOUR_PROJECT_LOCATION" # เช่น us-central1
          export GOOGLE_GENAI_USE_VERTEXAI=true
          ```
        - สำหรับการใช้งานซ้ำ คุณสามารถเพิ่มตัวแปรสภาพแวดล้อมไปยังไฟล์ `.env` ของคุณ (อยู่ในไดเร็กทอรีโครงการหรือไดเร็กทอรีโฮมของผู้ใช้) หรือไฟล์การกำหนดค่าของเชลล์ (เช่น `~/.bashrc`, `~/.zshrc` หรือ `~/.profile`) ตัวอย่าง คำสั่งต่อไปนี้เพิ่มตัวแปรสภาพแวดล้อมไปยังไฟล์ `~/.bashrc`:
          ```bash
          echo 'export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"' >> ~/.bashrc
          echo 'export GOOGLE_CLOUD_LOCATION="YOUR_PROJECT_LOCATION"' >> ~/.bashrc
          echo 'export GOOGLE_GENAI_USE_VERTEXAI=true' >> ~/.bashrc
          source ~/.bashrc
          ```
    - หากใช้โหมด express:
      - ตั้งค่าตัวแปรสภาพแวดล้อม `GOOGLE_API_KEY` ในวิธีการต่อไปนี้ แทนที่ `YOUR_GOOGLE_API_KEY` ด้วย Vertex AI API key ที่ให้มาโดยโหมด express:
        - คุณสามารถตั้งค่าตัวแปรสภาพแวดล้อมเหล่านี้ชั่วคราวในเซสชันเชลล์ปัจจุบันของคุณโดยใช้คำสั่งต่อไปนี้:
          ```bash
          export GOOGLE_API_KEY="YOUR_GOOGLE_API_KEY"
          export GOOGLE_GENAI_USE_VERTEXAI=true
          ```
        - สำหรับการใช้งานซ้ำ คุณสามารถเพิ่มตัวแปรสภาพแวดล้อมไปยังไฟล์ `.env` ของคุณ (อยู่ในไดเร็กทอรีโครงการหรือไดเร็กทอรีโฮมของผู้ใช้) หรือไฟล์การกำหนดค่าของเชลล์ (เช่น `~/.bashrc`, `~/.zshrc` หรือ `~/.profile`) ตัวอย่าง คำสั่งต่อไปนี้เพิ่มตัวแปรสภาพแวดล้อมไปยังไฟล์ `~/.bashrc`:
          ```bash
          echo 'export GOOGLE_API_KEY="YOUR_GOOGLE_API_KEY"' >> ~/.bashrc
          echo 'export GOOGLE_GENAI_USE_VERTEXAI=true' >> ~/.bashrc
          source ~/.bashrc
          ```
