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
| Frontend (Vercel)  | `https://restaurant-management-system-exam20.vercel.app` | ✅ |
| Backend (Render)   | `https://rms-backend-l5a0.onrender.com`  | ✅ |
| API Health Check   | `https://rms-backend-l5a0.onrender.com/api/health` | ✅ |
| Database (Neon)    | `postgresql://neondb_owner:***@ep-jolly-hat-aqznmse6-pooler.c-8.us-east-1.aws.neon.tech/neondb` | ✅ |

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
| OS             | macOS |
| Node.js        | 22 LTS |
| npm            | 10.9.7 |
| Docker         | 29.2.1 |
| PostgreSQL     | 16 (Neon.tech) |
| Browser        | Chrome |
| Newman         | 6.2.2 |
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
| TC-ID | Feature | Scenario | Input | Expected | Actual | Pass/Fail |
|-------|---------|----------|-------|----------|--------|-----------|
| TC-001 | Auth | **[Positive]** Login ด้วย admin ถูกต้อง | `{username:"admin", password:"Admin@123"}` | HTTP 200 + JWT token | HTTP 200 + token | ✅ Pass |
| TC-002 | Menu | **[Positive]** เพิ่มเมนูใหม่สำเร็จ | `{name:"ข้าวผัด", price:60, category:"main"}` | HTTP 201 + object ที่สร้าง | HTTP 201 | ✅ Pass |
| TC-003 | Payment | **[Positive]** ชำระเงินและได้ทอนถูกต้อง | orderId ที่ confirm แล้ว, amount:100, total:75 | HTTP 200, change:25 | HTTP 200, change:25 | ✅ Pass |
| TC-004 | Auth | **[Negative]** Login password ผิด | `{username:"admin", password:"wrong"}` | HTTP 401 | HTTP 401 | ✅ Pass |
| TC-005 | Order | **[Negative]** เพิ่ม item ใน order ที่ปิดแล้ว | closedOrderId + itemId | HTTP 400 หรือ 403 | HTTP 400 | ✅ Pass |
| TC-006 | Menu | **[Negative]** สร้างเมนูราคาติดลบ | `{name:"test", price:-1}` | HTTP 400 + error message | HTTP 201 (BUG-001) | ❌ Fail |
| TC-007 | Security | **[Security]** เรียก API โดยไม่มี Token | `GET /api/orders` (ไม่มี Authorization header) | HTTP 401 Unauthorized | HTTP 401 | ✅ Pass |
| TC-008 | Security | **[Security]** Waiter เข้าถึง Admin endpoint | Waiter token + `DELETE /api/menu/:id` | HTTP 403 Forbidden | HTTP 200 (BUG-002) | ❌ Fail |
| TC-009 | Security | **[Security]** SQL Injection ใน login | `{username:"admin'--", password:"x"}` | HTTP 401, ไม่ bypass auth | HTTP 401 | ✅ Pass |
| TC-010 | Order | **[Edge]** สร้าง order ที่ไม่มี item เลย | POST /api/orders, items:[] | HTTP 400 + error message | HTTP 201 (BUG-003) | ❌ Fail |
| TC-011 | Payment | **[Edge]** ชำระเงินพอดี (change = 0) | amount = totalPrice (75) | HTTP 200, change:0 | HTTP 200, change:0 | ✅ Pass |

**สรุปผล:** ผ่าน 8 / 11 กรณี (72.7%)

---

## Test Reports

> **ส่วนที่ 3 (ต่อ) — ผลการรัน Newman**

### Newman Run Result
```
Collection: RMS-68030129-TestSuite
Run Date:   2026-05-15
┌─────────────────────────┬────────────────────┬────────────────────┐
│                         │           executed │             failed │
├─────────────────────────┼────────────────────┼────────────────────┤
│              iterations │                  1 │                  0 │
│                requests │                 12 │                  0 │
│            test-scripts │                  9 │                  0 │
│      prerequest-scripts │                  0 │                  0 │
│              assertions │                 13 │                  3 │
├─────────────────────────┴────────────────────┴────────────────────┤
│ total run duration: 16.2s                                         │
│ total data received: 3.55kB (approx)                              │
│ average response time: 1331ms [min: 5ms, max: 3.4s, s.d.: 1026ms] │
└───────────────────────────────────────────────────────────────────┘
```
**Pass Rate: 10 / 13 (76.9%)**

### Failures (ล้วนเป็น Bug ในระบบ)
| # | TC | Expected | Actual | สาเหตุ |
|---|----|----|----|----|
| 1 | TC-006 Negative Price | 400 | 201 | BUG-001: ระบบไม่ validate ราคาติดลบ |
| 2 | TC-008 Role Forbidden | 403 | 200 | BUG-002: ระบบไม่ตรวจสอบ Role ก่อนลบเมนู |
| 3 | TC-010 Empty Order | 400 | 201 | BUG-003: ระบบรับ order ว่างได้ |


### Newman E2E Test Summary

```
Collection: RMS-68030129-TestSuite
Run Date:   2026-05-15 18:17

┌─────────────────────────┬──────────────────┐
│                         │         executed │
├─────────────────────────┼──────────────────┤
│              iterations │                1 │
│                requests │               12 │
│            test-scripts │                9 │
│      prerequest-scripts │                0 │
│              assertions │               13 │
├─────────────────────────┴──────────────────┤
│ total run duration:     16.2s              │
│ total data received:    3.55kB             │
│ average response time:  1331ms             │
└────────────────────────────────────────────┘
```

**Pass Rate:** 10 / 13 (76.9%)  
**Newman Report (HTML):** `./tests/reports/newman-report.html`

> 📸 
![alt text](newman-result-1.png) 
![alt text](newman-result-2.png)

---

## Security Scan Report

### Backend
- **found 0 vulnerabilities** ✅

### Frontend
| Severity | Count |
|----------|-------|
| Critical | 0 |
| High | 1 |
| Moderate | 2 |
| Low | 0 |

### High Vulnerability Details
| Package | CVE | Severity | Fix |
|---------|-----|----------|-----|
| axios 1.0.0-1.15.1 | GHSA-3w6x-2g7m-8v23 | High | npm audit fix |
| axios 1.0.0-1.15.1 | GHSA-q8qp-cvcw-x6jj | High | npm audit fix |

### Moderate Vulnerability Details
| Package | CVE | Severity | Fix |
|---------|-----|----------|-----|
| esbuild <=0.24.2 | GHSA-67mh-4wv8-2f99 | Moderate | npm audit fix --force |

> **ส่วนที่ 3.4 — npm audit Security Scan**

### Backend Security Scan
```bash
cd backend && npm audit --audit-level=moderate
```

| Severity | จำนวน |
|----------|--------|
| Critical | 0      |
| High     | 0      |
| Medium   | 0      |
| Low      | 0      |
| **รวม**  | **0**  |

✅ ไม่พบช่องโหว่ใดๆ

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
cd frontend && npm audit --audit-level=moderate
```

| Severity | จำนวน |
|----------|--------|
| Critical | 0      |
| High     | 0      |
| Medium   | 2      |
| Low      | 0      |
| **รวม**  | **2**  |

> พบช่องโหว่ระดับ Moderate 2 รายการใน dependency ของ frontend
> ไม่กระทบการทำงานหลักของระบบ และไม่มีระดับ High/Critical

---

## Bug Reports

> **ส่วนที่ 3 — รายงานข้อบกพร่อง (≥ 2 Bug)**

---

### BUG-001: [ชื่อ Bug สั้น ๆ]
## BUG-001: ระบบยอมรับราคาติดลบในเมนู
**Severity:** High
**Priority:** P2
**Feature:** Menu
**Status:** Open 

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
> พนักงาน Waiter สามารถลบเมนูทั้งหมดได้ ทำให้ระบบเสียหาย ข้อมูลเมนูสูญหาย

---

### ## BUG-003: [ชื่อ Bug สั้น ๆ]
## BUG-003: ระบบยอมรับการชำระเงินที่น้อยกว่ายอดรวม และคำนวณเงินทอนติดลบ
**Severity:** High  
**Priority:** P2  
**Feature:** Order  
**Status:** Open

### Steps to Reproduce
1. Login ด้วย waiter token
2. POST /api/orders พร้อม body `{"tableId":1,"items":[]}`
3. ดูผลลัพธ์

### Expected Result
> HTTP 400 Bad Request — ต้องมีสินค้าอย่างน้อย 1 รายการ

### Actual Result
> HTTP 201 Created — ระบบสร้าง order ว่างสำเร็จ (totalAmount: 0)

#### Evidence  
> `![alt text](bug-003.png)`

### Business Impact
> ครัวได้รับออเดอร์ว่าง ทำให้สับสนและเสียเวลา อาจทำให้โต๊ะถูก occupy โดยไม่มีออเดอร์จริง

---
### BUG-001 (Fixed): ระบบยอมรับการชำระเงินที่น้อยกว่ายอดรวม

**Severity:** Critical  
**Priority:** P1  
**Feature:** Payment  
**Status:** ✅ Fixed (commit: 4137002)

#### Steps to Reproduce
1. สร้าง order และ confirm (totalAmount = 75)
2. POST /api/payments ด้วย `{"orderId":1, "amountPaid":50}`
3. ดูผลลัพธ์

#### Expected Result
HTTP 400 Bad Request — จำนวนเงินที่จ่ายน้อยกว่ายอดรวม

#### Actual Result (Before Fix)
HTTP 201 Created — ระบบประมวลผลสำเร็จและคืน change: -25 (ติดลบ)

#### Fix Applied
เพิ่ม validation ใน `backend/src/routes/payments.ts`:
```typescript
if (paid < totalAmount) {
  res.status(400).json({ error: 'Insufficient payment amount' }); return
}
```
#### Business Impact
ร้านอาหารสูญเสียรายได้ทุกครั้งที่ลูกค้าจ่ายเงินไม่ครบ

---

## Deployment Guide

> **ส่วนที่ 4 & 5 — คู่มือการติดตั้ง**

### Prerequisites

| รายการ       | เวอร์ชันที่ต้องการ | ลิงก์ดาวน์โหลด |
|--------------|-------------------|----------------|
| Node.js      | 22 LTS            | https://nodejs.org |
| Git          | ล่าสุด            | https://git-scm.com |
| Docker       | 29.2.1            | https://docker.com |
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
| Backend Health | `http://localhost:3001/api/health` | `{"status":"ok"}` | ✅ |
| Frontend Login | `http://localhost:5173` | หน้า Login แสดงผลสำเร็จ | ✅ |


#### หลักฐาน (On-Premises)

> 📸 **ภาพหน้าจอ Backend Health Check** (`http://localhost:3001/api/health`)
> 
> ![alt text](<ภาพถ่ายหน้าจอ 2569-05-08 เวลา 16.29.49.png>)

> 📸 **ภาพหน้าจอ Frontend Login สำเร็จ** (`http://localhost:5173`)
>
> ![alt text](<ภาพถ่ายหน้าจอ 2569-05-08 เวลา 16.29.04.png>)

---

### Staging Environment (Docker Compose)

> **ส่วนที่ 4.2 — การติดตั้งด้วย Docker Compose (8 คะแนน)**

#### สิ่งที่แก้ไขใน `docker-compose.yml`

- [x] เพิ่ม Environment Variables ครบถ้วน (`DATABASE_URL`, `JWT_SECRET`, `CORS_ORIGIN`, `VITE_API_URL`)
- [x] กำหนด Port Mapping: backend → 3001, frontend → 80
- [x] เพิ่ม Health Check สำหรับ backend service
- [x] กำหนด `depends_on` ให้ frontend รอ backend พร้อมก่อน
- [x] แก้ CORS_ORIGIN ให้รองรับทั้ง `http://localhost` และ `http://localhost:80`

#### docker compose ps
| Name         | Service  | Status       | Ports |
|--------------|----------|--------------|-------|
| rms-backend  | backend  | Up (healthy) | 0.0.0.0:3001->3001/tcp |
| rms-frontend | frontend | Up           | 0.0.0.0:80->80/tcp |


#### คำสั่งรัน Staging

```bash
docker compose up --build
```

#### ผลการทดสอบ (Smoke Test — Staging)

#### Smoke Test บน Staging
#### ผลการทดสอบ (Smoke Test — Staging)
| ทดสอบ | URL | ผลลัพธ์ที่คาดหวัง | ผ่าน/ไม่ผ่าน |
|-------|-----|-------------------|--------------|
| Backend Health | `http://localhost:3001/api/health` | `{"status":"ok"}` | ✅ |
| Frontend       | `http://localhost:80` | หน้า Login แสดงผลสำเร็จ | ✅ |

#### หลักฐาน (Staging)

> 📸 **ภาพหน้าจอ `docker compose ps`** (ทุก Container สถานะ running)
>
> ![alt text](<ภาพถ่ายหน้าจอ 2569-05-14 เวลา 20.03.05.png>)

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

| # | Feature          | คำสั่ง / ขั้นตอน                              | Expected               | ผ่าน/ไม่ผ่าน |
|---|------------------|-----------------------------------------------|------------------------|--------------|
| 1 | Health Check     | `GET https://rms-backend-l5a0.onrender.com/api/health` | `{"status":"ok"}` | ✅ Pass |
| 2 | Login            | Login ด้วย admin / Admin@123 บน Vercel        | เข้าระบบสำเร็จ Dashboard แสดงผล | ✅ Pass |
| 3 | Open Order & Add | Orders → Table 1 → Add Fried Rice → Confirm  | Order confirmed! แสดง | ✅ Pass |
| 4 | Payment          | Process Payment → Amount 100 → Total 75      | Payment Successful! Change ฿25.00 | ✅ Pass |

**Production Smoke Test ผ่าน: 4 / 4 รายการ** ✅

> 📸 (วางภาพหน้าจอหลักฐานแต่ละ Feature)
![alt text](<1 Health Check.png>) 
![alt text](<2 Login.png>) 
![alt text](<3 Open Order.png>) 
![alt text](<3 Open Order & Add.png>) 
![alt text](<4 Payment (ก่อนชำระ).png>) 
![alt text](<4 Payment (สำเร็จ).png>)

---

## CI/CD Pipeline + Newman Pass Rate

> **ส่วนที่ 5.5**

### สิ่งที่แก้ไขใน `.github/workflows/cicd.yml`

- [x] เพิ่ม trigger เมื่อมีการ push ไปที่สาขาหลัก (`main`)
- [x] เพิ่ม `actions/setup-node@v4` สำหรับ Node.js version 22
- [x] เพิ่ม step รัน Unit Test ของ Backend (`npm test`) — 20/20 passed
- [x] เพิ่ม step ติดตั้งและรัน Newman — 10/13 assertions passed
- [x] เพิ่ม step `npm audit --audit-level=high` ทั้ง backend และ frontend


### Newman Pass Rate (จาก CI/CD Pipeline)
| Metric          | ค่า    |
|-----------------|--------|
| Total Requests  | 12     |
| Total Assertions | 13    |
| Tests Passed    | 10     |
| Tests Failed    | 3      |
| **Pass Rate**   | **76.9%** |

> 📸 **ภาพหน้าจอ GitHub Actions Pipeline สำเร็จ**
>
> ![alt text](CI.png)
> หมายเหตุ: 3 assertions ที่ fail เป็น Bug ที่ยังเปิดอยู่ในระบบ (BUG-001, BUG-002, BUG-003)
> CI/CD Pipeline ผ่านสำเร็จ (CI #10) ใน 56 วินาที ✅
---

*Template สร้างจากข้อสอบปฏิบัติการทดสอบและติดตั้งระบบซอฟต์แวร์เชิงธุรกิจ — PRIME-BSD Model*




