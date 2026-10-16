# Final Exam: Playwright Testing บน SauceDemo

ระบบเป้าหมาย: https://www.saucedemo.com/
เครื่องมือ: Playwright Test (TypeScript)

## วิธีรัน

```bash
npm install
npx playwright install chromium
npx playwright test
npx playwright show-report
```

หลังรันจะได้ `playwright-report/index.html` และ `reports/results.json`

## โครงสร้างข้อสอบ

| รหัส | ไฟล์ | หัวข้อ |
|---|---|---|
| UT-01 | `tests/unit/UT-01.spec.ts` | Login Form Validation (3 test cases) |
| UT-02 | `tests/unit/UT-02.spec.ts` | Product Button State Validation |
| IT-01 | `tests/integration/IT-01.spec.ts` | Top-Down Integration ด้วย Stub |
| IT-02 | `tests/integration/IT-02.spec.ts` | Bottom-Up Integration ด้วย Driver |
| ST-01 | `tests/system/ST-01.spec.ts` | Complete Purchase Flow |
| ST-02 | `tests/system/ST-02.spec.ts` | Checkout Validation and Recovery |

บทที่ 1 เป็น UI Component/Functional Testing แบบ Black-box ผ่านเบราว์เซอร์ เพราะเข้าถึง Source Code ภายในของ SauceDemo ไม่ได้

## IT-01: Top-Down Integration Testing ด้วย Stub

แนวคิด Top-Down คือทดสอบจากโมดูลระดับบนลงล่าง โดยใช้ Stub แทนโมดูลระดับล่างที่ยังไม่พร้อมหรือไม่ต้องการใช้ของจริง

| ส่วน | สถานะ | รายละเอียด |
|---|---|---|
| หน้า Login ของ SauceDemo | **Real** | เปิดเว็บจริง กรอก `standard_user` / `secret_sauce` และกด Login จริง |
| การเปลี่ยนไปหน้า `inventory.html` | **Real** | ตรวจ URL จริงหลัง Login สำเร็จ |
| หน้า Inventory | **Stub** | สร้างด้วย `page.setContent()` แสดง `Mock Inventory Ready` และสินค้า `Mock Backpack`, `Mock Bike Light` |

Stub นี้จำลอง DOM ระดับเบราว์เซอร์หลัง Login จริง ไม่ได้แทน Internal Module ของ SauceDemo โดยตรง ส่วนที่ Assertions ตรวจหลังสร้าง Stub จึงเป็นการยืนยันว่าชั้นบน (Login) ส่งต่อไปยังชั้นล่างที่ถูกจำลองได้ตามที่ออกแบบ

## IT-02: Bottom-Up Integration Testing ด้วย Driver

แนวคิด Bottom-Up คือทดสอบจากโมดูลระดับล่างขึ้นบน โดยใช้ Driver ทำหน้าที่เรียกใช้และเตรียมสภาพแวดล้อมแทนโมดูลระดับบนที่ยังไม่ได้ผสานเข้ามา

**บทบาทของ Driver:** ฟังก์ชัน `driverOpenInventory()` ทำหน้าที่แทนขั้นตอน Login โดยสร้าง `BrowserContext`, ตั้ง Cookie `session-username=standard_user` บนโดเมน `www.saucedemo.com` ด้วย `addCookies()` แล้วเปิด `https://www.saucedemo.com/inventory.html` ตรง ๆ ไม่ผ่านฟอร์ม Login

| ส่วน | สถานะ | รายละเอียด |
|---|---|---|
| `driverOpenInventory()` และ Cookie | **Driver** | เตรียมสถานะ Login |
| หน้า Inventory (สินค้า 6 รายการ) | **Real** | ใช้หน้าจริงของ SauceDemo |
| การเพิ่มสินค้าและ Cart Badge | **Real** | คลิกปุ่มจริง |
| หน้า Shopping Cart | **Real** | ตรวจสินค้าสองรายการในหน้าจริง |

Test ปิด `BrowserContext` ที่สร้างเองในบล็อก `finally`

## ผลการทดสอบ

ดูสรุปผลจากการรันจริงใน `reports/test-summary.md` และรายงานฉบับเต็มใน `playwright-report/` กับ `reports/results.json`
