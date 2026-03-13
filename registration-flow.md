---
layout: default
title: "報名系統 QA 表"
---

# CNC 報名系統 — QA 測試表

```
課程介紹 → 選擇梯次 → 填寫個資 → 折扣碼 → 確認金額 → 付款 → 完成報名
```

---

## Part A：學員前台

### A1. 帳號系統

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 1 | 註冊帳號 | [/signup](https://cnc-navicareer.web.app/signup) | 填 email + 密碼 + 姓名 | ✅ |
| 2 | 登入 | [/login](https://cnc-navicareer.web.app/login) | Email + 密碼登入 | ✅ |
| 3 | Google 登入 | [/login](https://cnc-navicareer.web.app/login) | Google OAuth → 自動建帳號 | ✅ |
| 4 | 帳號合併 | — | 同 email 的 Email 帳號 + Google 帳號自動連結 | ✅ |

### A2. 課程瀏覽

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 5 | 課程列表 | [/courses](https://cnc-navicareer.web.app/courses) | 顯示開放報名梯次，含日期、價格、名額 | ✅ |
| 6 | 課程介紹 | [/courses/cnc-career-consultant](https://cnc-navicareer.web.app/courses/cnc-career-consultant) | 課程內容、師資、牌卡照片、即時價格 | ✅ |

### A3. 報名流程

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 7 | Step 1 選課 | /register/{cohortId} | 選班別（A / A+B / A+B+C），名額條，早鳥 badge | ✅ |
| 8 | Step 2 個資 | /register/{cohortId} | 姓名、Email、手機、LINE、產業、地址（自動帶入 Profile）| ✅ |
| 9 | Step 3 折扣 | /register/{cohortId} | 折扣碼驗證 + 價格摘要（原價-早鳥-折扣=應付）| ✅ |
| 10 | 送出報名 | /register/{cohortId} | 建立報名記錄 → 跳轉結帳頁 | ✅ |
| 11 | 確認信 | — | 報名成功自動寄 Email | ✅ |

### A4. 付款

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 12 | 結帳頁 | /checkout/{orderId} | 訂單摘要 + 付款方式 + 發票 | ✅ |
| 13 | 綠界付款 | 外部導向 | ECPay 完成付款（sandbox 不扣款）| ✅ |
| 14 | 付款成功 | /register/success/{orderId} | 自動 redirect 回成功頁 | ✅ |
| 15 | 付款失敗 | /checkout/failed | redirect 回失敗頁 | ✅ |
| 16 | 付款成功信 | — | 自動寄 Email 通知 | ✅ |

### A5. 個人資料 & 報名紀錄

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 17 | 個人 Profile | [/student/profile](https://cnc-navicareer.web.app/student/profile) | 編輯姓名、手機、LINE、產業、地址 | ✅ |
| 18 | 報名歷史 | [/student/enrollments](https://cnc-navicareer.web.app/student/enrollments) | 查詢報名紀錄 + 狀態 badge + 付款按鈕 | ✅ |

### A6. 名額連動（A/B 兩池，可配置）

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 19 | 名額連動 | — | A+B+C 佔 A+B 池 / A+B 佔 A+B 池 / A only 佔 A 池（seat_rules 可配置）| ✅ |
| 20 | 額滿擋報名 | — | 任一池歸零 → 擋住需要該池的班別 | ✅ |
| 21 | 退課回補 | — | 退課核准 → 對應池名額 +1 | ✅ |

---

## Part B：管理後台

### B1. 梯次管理

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 22 | 梯次 CRUD | [/admin/cohorts](https://cnc-navicareer.web.app/admin/cohorts) | 新增/編輯/刪除梯次（日期、價格、名額、內容管理）| ✅ |
| 23 | 教室容量設定 | /admin/cohorts | A教室 + B教室容量、seat_rules 配置 | ✅ |
| 24 | 狀態切換 | /admin/cohorts | planning → registration → in_progress → completed | ✅ |

### B2. 報名管理

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 25 | 報名列表 | [/admin/enrollments](https://cnc-navicareer.web.app/admin/enrollments) | 查看所有報名，依狀態/梯次篩選 | ✅ |
| 26 | 確認轉帳 | /admin/enrollments | 手動確認銀行轉帳付款 | ✅ |
| 27 | 退課審核 | /admin/enrollments | 核准退課申請 | ✅ |

### B3. 折扣碼管理

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 28 | 折扣碼 CRUD | [/admin/promo-codes](https://cnc-navicareer.web.app/admin/promo-codes) | 建立/編輯/停用/刪除折扣碼 | ✅ |

### B4. 退款管理

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 29 | 退款審核 | [/admin/refunds](https://cnc-navicareer.web.app/admin/refunds) | 待退款列表 + 退款處理 | ✅ |

### B5. Dashboard

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 30 | 數據總覽 | [/admin/dashboard](https://cnc-navicareer.web.app/admin/dashboard) | 報名數、待付款、已付款、待退款統計 | ✅ |

### B6. 權限與安全

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 31 | 權限檢查 | API | 一般學員打 admin API → 403 | ✅ |
| 32 | 未登入存取 | API | 未帶 JWT 打 admin API → 401 | ✅ |

---

## Part C：待上線

| 步驟 | 項目 | 測試說明 | 狀態 |
|------|------|---------|------|
| 33 | 綠界正式環境 | 切換正式商店金鑰 | ❌ 待上線（需正式金鑰）|
| 34 | GCP OAuth Client ID | Google 登入需 Client ID | ❌ 待設定（需 GCP Console）|
| 35 | Email 通知完善 | 退課通知 / 課前提醒模板 | ❌ 待開發（P2）|

---

## E2E 自動測試

Playwright 測試覆蓋：14 項自動測試通過

| 測試檔案 | 測試項目 | 數量 |
|----------|---------|------|
| `e2e/a1-auth.spec.ts` | 註冊/登入表單、驗證、錯誤訊息 | 4 |
| `e2e/a2-courses.spec.ts` | 課程列表、課程介紹、報名按鈕 | 3 |
| `e2e/a3-registration.spec.ts` | 報名頁面、班別選擇、價格顯示 | 3 |
| `e2e/b4-security.spec.ts` | Admin 權限檢查、401 驗證 | 2 |
| `e2e/c1-responsive.spec.ts` | Desktop + Mobile RWD | 2 |
