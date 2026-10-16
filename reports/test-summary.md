# สรุปผลการทดสอบ (Test Summary)

> **ต้องกรอกหลังรัน `npx playwright test` จริงบนเครื่องของคุณเท่านั้น** ห้ามกรอกผลที่ไม่ได้มาจากการรันจริง
> ไฟล์นี้ถูกสร้างเป็นแม่แบบ ยังไม่มีผลการรันใด ๆ

- วันที่รัน: 16 ตุลาคม 2026 เวลา 15:03
- เวอร์ชัน Playwright (`npx playwright --version`):1.64.1
- เบราว์เซอร์: Chromium (Desktop Chrome)

| รหัส | ชื่อ Test | ผล (Passed/Failed) | หมายเหตุ / ข้อผิดพลาดที่พบ |
|---|---|---|---|
| UT-01.1 | empty username and password | Passed  | ____ |
| UT-01.2 | missing password | Passed  | ____ |
| UT-01.3 | invalid login details | Passed  | ____ |
| UT-02 | product button state Add to cart -> Remove -> Add to cart |Passed  | ____ |
| IT-01 | top-down REAL Login -> browser-level Inventory STUB |Passed  | ____ |
| IT-02 | DRIVER login state -> REAL Inventory and Cart |Passed  | ____ |
| ST-01 | complete purchase of two products | Passed  | ____ |
| ST-02 | checkout validation and recovery | Passed  | ____ |

รวม: Passed 8 / 8 test cases (6 ข้อสอบ)
