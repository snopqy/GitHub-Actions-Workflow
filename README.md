1. การใช้ `on: push` และ `on: pull_request` ช่วยให้ Workflow ทำงานโดยอัตโนมัติเมื่อมีการเปลี่ยนแปลงใน branch `main` ซึ่งเป็น branch หลักของโปรเจกต์

- `on: push` จะทำให้ workflow ทำงานเมื่อมีการ push โค้ดใหม่เข้าสู่ branch main โดยตรง เช่น การแก้ไขไฟล์แล้ว push ขึ้น GitHub
- `on: pull_request` จะทำให้ workflow ทำงานเมื่อนักพัฒนาสร้าง Pull Request ที่เปลี่ยนแปลงไปยัง branch main เพื่อให้สามารถตรวจสอบ (CI) ได้ก่อนที่จะรวมโค้ดเข้ามา
การใช้ทั้งสองอย่างช่วยครอบคลุมทั้งการ push โดยตรง และการ merge ผ่าน pull request ซึ่งเป็นกระบวนการพัฒนาที่ปลอดภัย

2. ใน GitHub Actions:

- `jobs` คือ กลุ่มของงานที่สามารถทำงานแยกกัน หรือเรียงลำดับกันได้ โดยระบุได้ว่าแต่ละ job ต้องรอ job อื่นก่อนหรือไม่ (`needs:`)
- `steps` คือ คำสั่งย่อยภายในแต่ละ `job` ซึ่งจะทำงานตามลำดับจากบนลงล่าง โดยสามารถเรียกใช้งาน action ที่มีอยู่ หรือสั่งรันคำสั่ง shell ได้

ใน workflow นี้:
- job `checkout` ทำหน้าที่ดึง source code มาจาก repository
- job `lint-yaml` ตรวจสอบว่าไฟล์ YAML ไม่มี syntax error
- job `build` จำลองการ build แอปพลิเคชัน
- job `notify` แสดงข้อความแจ้งว่า workflow เสร็จแล้ว
