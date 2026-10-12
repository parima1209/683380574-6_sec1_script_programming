\# Week 8: Automating with CSV and JSON Data



\*\*จัดทำโดย:\*\* จันทรณภา จอมทอง 683380574-6 



โปรเจกต์นี้ฝึกการอ่าน เขียน และประมวลผลไฟล์ CSV และ JSON ด้วยโมดูล `csv` และ `json` ของ Python



\## ความสามารถ

\* \*\*อ่าน CSV (DictReader)\*\*: อ่านไฟล์ CSV โดยใช้แถวแรกเป็นหัวตาราง

\* \*\*เขียน CSV (DictWriter)\*\*: เขียนข้อมูลแบบ dictionary กลับเป็นไฟล์ CSV

\* \*\*ประมวลผล CSV\*\*: คำนวณยอดขายรวม ราคาเฉลี่ย และกรองรายการตามเงื่อนไข

\* \*\*อ่าน/เขียน JSON\*\*: ใช้ `json.load` และ `json.dump` (จัดรูปแบบให้อ่านง่าย)

\* \*\*แก้ไขข้อมูล JSON\*\*: อัปเดตสต็อกสินค้าและเพิ่มสินค้าใหม่

\* \*\*แยกโมดูล\*\*: `csv\_handler.py`, `json\_handler.py`, `utils.py`



\## วิธีรัน

&#x20;   python main.py



\## ผลลัพธ์

\* `data/output\_filtered\_sales.csv` — รายการขายที่ผ่านการกรอง พร้อมแถวสรุป

\* `data/output\_updated\_inventory.json` — ข้อมูลสินค้าคงคลังที่อัปเดตแล้ว



\## โครงสร้างโปรเจกต์

&#x20;   data-processor/

&#x20;   ├── src/

&#x20;   │   ├── \_\_init\_\_.py

&#x20;   │   ├── csv\_handler.py

&#x20;   │   ├── json\_handler.py

&#x20;   │   └── utils.py

&#x20;   ├── data/

&#x20;   │   ├── input\_sales.csv

&#x20;   │   └── input\_inventory.json

&#x20;   ├── main.py

&#x20;   ├── .gitignore

&#x20;   └── README.md

