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
| 8 | Step 2 個資 | /register/{cohortId} | 姓名、Email、手機、LINE、產業、地址 | ✅ |
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

### A5. 名額連動（A/B/C 三池）

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 17 | 名額連動 | — | A+B+C 佔三池 / A+B 佔兩池 / A only 佔一池 | ✅ |
| 18 | 額滿擋報名 | — | 任一池歸零 → 擋住需要該池的班別 | ✅ |
| 19 | 退課回補 | — | 退課核准 → 對應池名額 +1 | ✅ |

---

## Part B：管理後台

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 20 | 梯次管理 | /admin/cohorts | CRUD 梯次（日期、價格、名額、C班設定）| ✅ |
| 21 | 報名列表 | /admin/enrollments | 查看所有報名，依狀態/梯次篩選 | 🔨 開發中 |
| 22 | 確認轉帳 | API | 手動確認銀行轉帳付款 | ✅ |
| 23 | 退課審核 | API | 核准退課 + 退款處理 | ✅ |
| 24 | 折扣碼管理 | /admin/promo-codes | 建立/停用折扣碼 | 🔨 開發中 |
| 25 | 權限檢查 | API | 一般學員打 admin API → 403 | ✅ |

---

## Part C：待開發

| 步驟 | 頁面 | 測試說明 | 是否實作 |
|------|------|---------|---------|
| 26 | 個人 Profile | 學員編輯個人資料 | ❌ 待開發 |
| 27 | 報名歷史 | 學員查詢報名紀錄 | ❌ 待開發 |
| 28 | Admin Dashboard | 數據總覽 | ❌ 待開發 |
| 29 | 退款管理 UI | 前端退款審核介面 | ❌ 待開發 |
| 30 | 綠界正式環境 | 切換正式商店金鑰 | ❌ 待上線 |
