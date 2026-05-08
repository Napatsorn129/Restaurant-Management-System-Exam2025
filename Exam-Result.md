# Restaurant Management System (RMS)

> **ข้อสอบปฏิบัติการทดสอบและติดตั้งระบบซอฟต์แวร์เชิงธุรกิจ**  
> รายวิชา: การออกแบบและพัฒนาซอฟต์แวร์ 1  
> ชื่อ-นามสกุล: นางสาวนภัสสร คำปัน 
> รหัสนักศึกษา: 68030129 
> วันที่สอบ: วันที่8 พ.ค 2569

---

## Project Overview

> ระบบจัดการร้านอาหาร (Restaurant Management System: RMS) เป็นระบบสำหรับจัดการเมนู การรับออเดอร์ การชำระเงิน และรายงานยอดขาย

**Source Repository:** `https://github.com/surachai-p/Restaurant-Management-System-Exam-2025.git`  
**Student Fork / Repo:** `https://github.com/[รหัสนักศึกษา]/Restaurant-Management-System-Exam-2025.git`

---

## Tech Stack

| Layer      | Technology                                      |
|------------|-------------------------------------------------|
| Frontend   | React 18 + Vite + TypeScript + Tailwind CSS     |
| Backend    | Node.js 22 LTS + Express + TypeScript           |
| Database   | PostgreSQL 16 (Neon.tech)                       |
| ORM        | Prisma                                          |
| Testing    | Vitest (Unit) + Newman (E2E)                    |
| Container  | Docker / Docker Compose                         |
| CI/CD      | GitHub Actions                                  |

---

## Production URLs

| Service            | URL                                      | Status |
|--------------------|------------------------------------------|--------|
| Frontend (Vercel)  | `https://[your-app].vercel.app`          | ⬜     |
| Backend (Render)   | `https://[your-api].onrender.com`        | ⬜     |
| API Health Check   | `https://[your-api].onrender.com/api/health` | ⬜ |
| Database (Neon)    | `postgresql://...@...neon.tech/...`      | ⬜     |

---

## Test Plan

> **ส่วนที่ 1 — แผนการทดสอบ (4 คะแนน)**

### 1.1 ขอบเขตการทดสอบ (Test Scope)

#### In Scope
| Feature   | เหตุผลที่ทดสอบ |
|-----------|----------------|
| Auth      | ระบบ Login/Logout และ Role-based Access |
| Menu      | CRUD เมนูและการจัดการสต็อก |
| Order     | เปิดโต๊ะ รับออเดอร์ แก้ไข ยืนยัน |
| Payment   | ชำระเงิน คำนวณทอน พิมพ์ใบเสร็จ |
| Report    | ยอดขายรายวัน/รายเดือน เมนูขายดี |
| Security  | JWT, RBAC, SQL Injection, XSS |

#### Out of Scope
| Feature                                 | เหตุผลที่ไม่ทดสอบ |
|-----------------------------------------|--------------------|
| Performance / Load Testing (JMeter, k6) | ไม่อยู่ในขอบเขตของข้อสอบและต้องการสภาพแวดล้อมพิเศษ |
| UI/UX Usability Testing                 | ต้องใช้ผู้ทดสอบจริง ไม่สามารถทำอัตโนมัติในเวลาที่กำหนด |
| Third-party Payment Gateway             | ระบบนี้ไม่มีการเชื่อมต่อ Payment Gateway ภายนอก |
| Mobile Responsive Testing               | ไม่ได้กำหนดเป็น Requirement หลักของระบบในข้อสอบนี้ |


---

### 1.2 แนวทางการทดสอบ (Test Approach)

| ประเภทการทดสอบ           | เครื่องมือ       | รายละเอียด |
|--------------------------|-----------------|------------|
| Unit Testing             | Vitest          | ทดสอบฟังก์ชันใน Backend |
| API Testing (E2E)        | Postman / Newman | ทดสอบ REST API endpoint ทั้งหมด |
| Security Testing         | npm audit, Manual | ตรวจสอบช่องโหว่ Dependency และ API |
| Smoke Testing            | Manual / Newman | ทดสอบ Feature หลัก 4 รายการบน Production |
| Staging Deployment Test  | Docker Compose  | ทดสอบก่อน Deploy บน Cloud |

---

### 1.3 สภาพแวดล้อมทดสอบ (Test Environment)

| รายการ         | เวอร์ชัน / ค่า                     |
|----------------|------------------------------------|
| OS             | Windows 11 / macOS / Ubuntu (ระบุของจริง) |
| Node.js        | 22 LTS |
| npm            | (รัน `npm -v` แล้วใส่) |
| Docker         | (รัน `docker -v` แล้วใส่) |
| PostgreSQL     | 16 (Neon.tech) |
| Browser        | Chrome 124+ |
| Newman         | (รัน `newman --version` แล้วใส่) |
---

### 1.4 เงื่อนไขการผ่าน/ไม่ผ่านการทดสอบ (Entry / Exit Criteria)

#### Entry Criteria (เงื่อนไขเริ่มทดสอบ)
| เงื่อนไข                    | รายละเอียด |
|---------------------------|------------|
| ระบบ Build ได้ไม่มี Error    | `npm run build` ของ backend และ frontend ต้องสำเร็จ |
| Database เชื่อมต่อได้         | `DATABASE_URL` ถูกต้องและ Prisma seed รันผ่าน |
| API Health Check ผ่าน      | `GET /api/health` ตอบ `{"status":"ok"}` |
| Postman Collection พร้อม   | Environment Variables ตั้งค่าครบ |


#### Exit Criteria (เงื่อนไขผ่านการทดสอบ)
| เกณฑ์                       | ค่าที่กำหนด |
|----------------------------|-----------|
| Newman Pass Rate           | ≥ 80% |
| Unit Test Pass Rate        | 100% |
| Critical/High Bug ที่ยังเปิดอยู่ | = 0 |
| Security Scan ระดับ High+   | = 0 หรือมี Mitigation Plan |
| Smoke Test บน Staging      | ผ่านทั้ง 4 Feature |

---

### 1.5 ความเสี่ยงเชิงธุรกิจ (Business Risk)

| # | Feature | ความเสี่ยง | ผลกระทบ | ระดับ |
|---|---------|-----------|---------|-------|
| 1 | Payment | คำนวณเงินทอนผิด เช่น จ่าย 500 บิล 350 ทอน 50 แทน 150 | ร้านขาดทุนทุกธุรกรรม สูญเสียความน่าเชื่อถือ | 🔴 Critical |
| 2 | Auth    | JWT ไม่หมดอายุหรือใช้ซ้ำหลัง Logout ได้ | ข้อมูลการเงินรั่วไหล อาจละเมิด PDPA | 🔴 Critical |
| 3 | Order   | ออเดอร์หายหลัง Confirm ไม่ถูก Save ลง Database | ครัวไม่ได้รับออเดอร์ ลูกค้ารอนาน เสียรายได้ | 🟠 High |
| 4 | Report  | ยอดขายแสดงผิด คำนวณนับซ้ำหรือขาดรายการ | ตัดสินใจทางธุรกิจบนข้อมูลผิด สั่งวัตถุดิบผิดปริมาณ | 🟠 High |
---

## Test Cases & Results

> **ส่วนที่ 2 — กรณีทดสอบ (8 คะแนน)**

### กรณีทดสอบทั้งหมด (≥ 10 กรณี)

## Test Cases & Results

| TC-ID | Feature | Scenario | Input | Expected | Actual | Pass/Fail |
|-------|---------|----------|-------|----------|--------|-----------|
| TC-001 | Auth | **[Positive]** Login ด้วย admin ถูกต้อง | `{username:"admin", password:"Admin@123"}` | HTTP 200 + JWT token | | |
| TC-002 | Menu | **[Positive]** เพิ่มเมนูใหม่สำเร็จ | `{name:"ข้าวผัด", price:60, category:"main"}` | HTTP 201 + object ที่สร้าง | | |
| TC-003 | Payment | **[Positive]** ชำระเงินและได้ทอนถูกต้อง | orderId ที่ confirm แล้ว, amount:200, total:150 | HTTP 200, change:50 | | |
| TC-004 | Auth | **[Negative]** Login password ผิด | `{username:"admin", password:"wrong"}` | HTTP 401 | | |
| TC-005 | Order | **[Negative]** เพิ่ม item ใน order ที่ปิดแล้ว | closedOrderId + itemId | HTTP 400 หรือ 403 | | |
| TC-006 | Menu | **[Negative]** สร้างเมนูราคาติดลบ | `{name:"test", price:-1}` | HTTP 400 + error message | | |
| TC-007 | Security | **[Security]** เรียก API โดยไม่มี Token | `GET /api/orders` (ไม่มี Authorization header) | HTTP 401 Unauthorized | | |
| TC-008 | Security | **[Security]** Waiter เข้าถึง Admin endpoint | Waiter token + `DELETE /api/menu/:id` | HTTP 403 Forbidden | | |
| TC-009 | Security | **[Security]** SQL Injection ใน login | `{username:"admin'--", password:"x"}` | HTTP 401, ไม่ bypass auth | | |
| TC-010 | Order | **[Edge]** Confirm order ที่ไม่มี item เลย | POST /api/orders/confirm, items:[] | HTTP 400 + error message | | |
| TC-011 | Payment | **[Edge]** ชำระเงินพอดี (change = 0) | amount = totalPrice | HTTP 200, change:0 | | |

**สรุปผล:** ผ่าน ___ / ___ กรณี (___%)

---

## Test Reports

> **ส่วนที่ 3 (ต่อ) — ผลการรัน Newman**

### Newman Run Result
- Total assertions: 13
- Passed: 10
- Failed: 3
- **Pass Rate: 77%**

### Failures (ล้วนเป็น Bug ในระบบ)
| # | TC | Expected | Actual | สาเหตุ |
|---|----|----|----|----|
| 1 | TC-006 Negative Price | 400 | 201 | BUG-001: ระบบรับราคาติดลบ |
| 2 | TC-008 Role Forbidden | 403 | 200 | token เป็น admin ในรอบนี้ |
| 3 | TC-010 Empty Order | 400 | 201 | BUG-002: ระบบรับ order ว่าง |

### Newman E2E Test Summary

```
Collection: RMS-[รหัสนักศึกษา]-TestSuite
Run Date:   YYYY-MM-DD HH:MM

┌─────────────────────────┬──────────────────┐
│                         │         executed │
├─────────────────────────┼──────────────────┤
│              iterations │                1 │
│                requests │               ?? │
│            test-scripts │               ?? │
│      prerequest-scripts │               ?? │
│              assertions │               ?? │
├─────────────────────────┴──────────────────┤
│ total run duration:     ???ms              │
│ total data received:    ???B               │
│ average response time:  ???ms              │
└────────────────────────────────────────────┘
```

**Pass Rate:** _____ / _____ (____%)  
**Newman Report (HTML):** `./tests/reports/newman-report.html`

> 📸 วางภาพหน้าจอผลการรัน Newman ที่นี่

---

## Security Scan Report

> **ส่วนที่ 3.4 — npm audit Security Scan**

### Backend Security Scan

```bash
# คำสั่งที่รัน:
cd backend && npm audit --audit-level=moderate
```

| Severity | จำนวน |
|----------|--------|
| Critical | 0      |
| High     | 0      |
| Medium   | 0      |
| Low      | 0      |
| **รวม**  | **0**  |

#### รายละเอียด Dependency ที่มีช่องโหว่ระดับ High ขึ้นไป

| Package | CVE ID | Severity | เวอร์ชันที่มีปัญหา | เวอร์ชันที่ปลอดภัย | สถานะ |
|---------|--------|----------|--------------------|---------------------|-------|
| <!-- ระบุรายละเอียด --> | | | | | |

**แก้ไขด้วย:**
```bash
npm audit fix
```

---

### Frontend Security Scan

```bash
# คำสั่งที่รัน:
cd frontend && npm audit --audit-level=moderate
```

| Severity | จำนวน |
|----------|--------|
| Critical | 0      |
| High     | 0      |
| Medium   | 0      |
| Low      | 0      |
| **รวม**  | **0**  |

---

## Bug Reports

> **ส่วนที่ 3 — รายงานข้อบกพร่อง (≥ 2 Bug)**

---

### BUG-001: [ชื่อ Bug สั้น ๆ]
## BUG-001: ระบบยอมรับราคาติดลบในเมนู
**Severity:** High
**Priority:** P2
**Feature:** Menu
**Status:** Open / Fixed

#### Steps to Reproduce
1. Login ด้วย admin token
2. POST /api/menu พร้อม body {"name":"ทดสอบ","price":-1,"category":"food"}
3. ดูผลลัพธ์

#### Expected Result
> HTTP 400 Bad Request — ราคาต้องมากกว่า 0

#### Actual Result
> HTTP 201 Created — ระบบสร้างเมนูราคา -1 บาทสำเร็จ (id: 12)

#### Evidence
> 📸 วางภาพหน้าจอที่นี่  
> `![alt text](bug-001.png)`

#### Business Impact
> เมนูที่มีราคาติดลบทำให้คำนวณยอดขายผิดพลาด ร้านอาหารสูญเสียรายได้
---

### BUG-002: [ชื่อ Bug สั้น ๆ]
## BUG-002: ระบบยอมรับ Order ที่ไม่มีสินค้าเลย
**Severity:** High
**Priority:** P2
**Feature:** Order 
**Status:** Open / Fixed

#### Steps to Reproduce
1. Login ด้วย waiter token
2. POST /api/orders พร้อม body {"tableId":1,"items":[]}
3. ดูผลลัพธ์

#### Expected Result
> HTTP 400 Bad Request — ต้องมีสินค้าอย่างน้อย 1 รายการ

#### Actual Result
> HTTP 201 Created — ระบบสร้าง order ว่างสำเร็จ (id:1, totalAmount:"0")

#### Evidence
> 📸 วางภาพหน้าจอที่นี่  
> `![alt text](bug-002.png)`

#### Business Impact
> ครัวได้รับออเดอร์ว่าง ทำให้สับสนและเสียเวลา อาจทำให้โต๊ะถูก occupy โดยไม่มีออเดอร์จริง

---

### ## BUG-003: [ชื่อ Bug สั้น ๆ]
## BUG-003: ระบบยอมรับการชำระเงินที่น้อยกว่ายอดรวม และคำนวณเงินทอนติดลบ
**Severity:** Critical
**Priority:** P1
**Feature:** Payment

### Steps to Reproduce
1. สร้าง order และ confirm (totalAmount = 160)
2. POST /api/payments ด้วย {"orderId":1, "amountPaid":100}
3. ดูผลลัพธ์

### Expected Result
> HTTP 400 Bad Request — จำนวนเงินที่จ่ายน้อยกว่ายอดรวม ไม่สามารถชำระได้

### Actual Result
> HTTP 201 Created — ระบบประมวลผลสำเร็จ และคืน change: -60 (ติดลบ)

#### Evidence
> 📸 วางภาพหน้าจอที่นี่  
> `![alt text](bug-003.png)`

### Business Impact
> ร้านอาหารสูญเสียรายได้ทุกครั้งที่ลูกค้าจ่ายเงินไม่ครบ เนื่องจากระบบไม่ตรวจสอบ

---

## Deployment Guide

> **ส่วนที่ 4 & 5 — คู่มือการติดตั้ง**

### Prerequisites

| รายการ       | เวอร์ชันที่ต้องการ | ลิงก์ดาวน์โหลด |
|--------------|-------------------|----------------|
| Node.js      | 22 LTS            | https://nodejs.org |
| Git          | ล่าสุด            | https://git-scm.com |
| Docker       | ล่าสุด            | https://docker.com |
| Docker Compose | v2+             | (รวมกับ Docker Desktop) |

---

### On-Premises Setup

> **ส่วนที่ 4.1 — การติดตั้งบนเครื่องตนเองในรูปแบบ On-Premises Server (8 คะแนน)**

#### ขั้นตอนการติดตั้ง

```bash
# 1. Clone Repository
git clone https://github.com/[รหัสนักศึกษา]/Restaurant-Management-System-Exam-2025.git
cd Restaurant-Management-System-Exam-2025

# 2. ตั้งค่า Environment Variables (Backend)
cp backend/.env.example backend/.env
# แก้ไข backend/.env ให้มีค่า:
#   DATABASE_URL=postgresql://...
#   JWT_SECRET=your-secret
#   CORS_ORIGIN=http://localhost:5173
#   NODE_ENV=development

# 3. รัน Backend (Port 3001)
cd backend
npm install
npm run dev

# 4. รัน Frontend (Port 5173) — เปิด terminal ใหม่
cd frontend
npm install
npm run dev
```

#### ผลการทดสอบ (Smoke Test — On-Premises)

| ทดสอบ | URL | ผลลัพธ์ที่คาดหวัง | ผ่าน/ไม่ผ่าน |
|-------|-----|-------------------|--------------|
| Backend Health | `http://localhost:3001/api/health` | `{"status":"ok"}` | ⬜ |
| Frontend Login | `http://localhost:5173` | หน้า Login แสดงผลสำเร็จ | ⬜ |

#### หลักฐาน (On-Premises)

> 📸 **ภาพหน้าจอ Backend Health Check** (`http://localhost:3001/api/health`)
> 
> (วางภาพที่นี่)

> 📸 **ภาพหน้าจอ Frontend Login สำเร็จ** (`http://localhost:5173`)
>
> (วางภาพที่นี่)

---

### Staging Environment (Docker Compose)

> **ส่วนที่ 4.2 — การติดตั้งด้วย Docker Compose (8 คะแนน)**

#### สิ่งที่แก้ไขใน `docker-compose.yml`

- [x] เพิ่ม Environment Variables ครบถ้วน (`DATABASE_URL`, `JWT_SECRET`, `CORS_ORIGIN`, `VITE_API_URL`)
- [x] กำหนด Port Mapping: backend → 3001, frontend → 80
- [x] เพิ่ม Health Check สำหรับ backend service
- [x] กำหนด `depends_on` ให้ frontend รอ backend พร้อมก่อน

#### คำสั่งรัน Staging

```bash
docker compose up --build
```

#### ผลการทดสอบ (Smoke Test — Staging)

| ทดสอบ | URL | ผลลัพธ์ที่คาดหวัง | ผ่าน/ไม่ผ่าน |
|-------|-----|-------------------|--------------|
| Backend Health | `http://localhost:3001/api/health` | `{"status":"ok"}` | ⬜ |
| Frontend       | `http://localhost:80` | หน้า Login แสดงผลสำเร็จ | ⬜ |

#### หลักฐาน (Staging)

> 📸 **ภาพหน้าจอ `docker compose ps`** (ทุก Container สถานะ running)
>
> (วางภาพที่นี่)

---

### Neon.tech Database Setup

> **ส่วนที่ 5.1**

#### ขั้นตอน
1. ไปที่ https://console.neon.tech → Create Project → เลือก PostgreSQL 16
2. คัดลอก Connection String (format: `postgresql://user:pass@ep-xxx.neon.tech/db?sslmode=require`)
3. ใช้เป็นค่า `DATABASE_URL` ใน Backend

**Connection String:** `postgresql://[user]:[pass]@[host].neon.tech/[db]?sslmode=require`

---

### Render + Vercel Deployment Steps

> **ส่วนที่ 5.2 & 5.3**

#### Backend บน Render.com

```
Build Command:  npm install && npx prisma generate && npm run build
Start Command:  npx prisma db push && npx tsx prisma/seed.ts && npm start
```

#### Frontend บน Vercel

```
Root Directory: frontend
Framework:      Vite
Build Command:  npm run build
```

---

### Environment Variables Table

| Variable      | Service   | ค่าตัวอย่าง / คำอธิบาย                         |
|---------------|-----------|------------------------------------------------|
| `DATABASE_URL` | Backend  | `postgresql://user:pass@host.neon.tech/db?sslmode=require` |
| `JWT_SECRET`   | Backend  | random string ที่ปลอดภัย (≥ 32 ตัวอักษร)       |
| `CORS_ORIGIN`  | Backend  | URL ของ Frontend เช่น `https://[app].vercel.app` |
| `NODE_ENV`     | Backend  | `production`                                    |
| `VITE_API_URL` | Frontend | URL ของ Backend เช่น `https://[api].onrender.com` |

---

### Smoke Test Results

> **ส่วนที่ 5.4 — ทดสอบ 4 Feature หลักบน Production**

| # | Feature          | คำสั่ง / ขั้นตอน                              | Expected               | หลักฐาน | ผ่าน/ไม่ผ่าน |
|---|------------------|-----------------------------------------------|------------------------|---------|--------------|
| 1 | Health Check     | `GET /api/health`                             | `{"status":"ok"}`      | 📸      | ⬜           |
| 2 | Login            | Login ด้วย admin บน Frontend URL              | เข้าระบบสำเร็จ        | 📸      | ⬜           |
| 3 | Open Order & Add | เปิดโต๊ะ → เพิ่มสินค้า → Confirm             | ออเดอร์ถูกบันทึก      | 📸      | ⬜           |
| 4 | Payment          | ชำระเงิน → ตรวจสอบ change                    | คำนวณเงินทอนถูกต้อง   | 📸      | ⬜           |

**Production Smoke Test ผ่าน: ___ / 4 รายการ**

> 📸 (วางภาพหน้าจอหลักฐานแต่ละ Feature)

---

## CI/CD Pipeline + Newman Pass Rate

> **ส่วนที่ 5.5**

### สิ่งที่แก้ไขใน `.github/workflows/cicd.yml`

- [x] เพิ่ม trigger เมื่อมีการ push ไปที่สาขาหลัก (`main` / `master`)
- [x] เพิ่ม `actions/setup-node` สำหรับ Node.js version 22
- [x] เพิ่ม step รัน Unit Test ของ Backend (`npm test`)
- [x] เพิ่ม step ติดตั้งและรัน Newman
- [x] เพิ่ม step `npm audit --audit-level=high` ทุกครั้งที่ push

### Newman Pass Rate (จาก CI/CD Pipeline)

| Metric          | ค่า    |
|-----------------|--------|
| Total Tests     | ??     |
| Tests Passed    | ??     |
| Tests Failed    | ??     |
| **Pass Rate**   | **??%** |

> 📸 **ภาพหน้าจอ GitHub Actions Pipeline สำเร็จ**
>
> (วางภาพที่นี่)

---

*Template สร้างจากข้อสอบปฏิบัติการทดสอบและติดตั้งระบบซอฟต์แวร์เชิงธุรกิจ — PRIME-BSD Model*




