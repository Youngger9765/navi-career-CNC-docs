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

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 1 | 註冊帳號 | [/signup](https://cnc-navicareer.web.app/signup) | 填 email + 密碼 + 姓名 | ✅ |
| 2 | 登入 | [/login](https://cnc-navicareer.web.app/login) | Email + 密碼登入 | ✅ |
| 3 | Google 登入 | [/login](https://cnc-navicareer.web.app/login) | Google OAuth → 自動建帳號 | ✅ |
| 4 | 帳號合併 | — | 同 email 的 Email + Google 帳號自動連結 | ✅ |

### A2. 課程瀏覽

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 5 | 課程列表 | [/courses](https://cnc-navicareer.web.app/courses) | 顯示開放報名梯次，含日期、價格、名額 | ✅ |
| 6 | 課程介紹 | [/courses/cnc-career-consultant](https://cnc-navicareer.web.app/courses/cnc-career-consultant) | 課程內容、師資、牌卡照片、即時價格 | ✅ |

### A3. 報名流程（三步驟）

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 7 | Step 1 選課 | /register/{cohortId} | 選班別（A / A+B / A+B+C），名額條，早鳥 badge | ✅ |
| 8 | Step 2 個資 | /register/{cohortId} | 姓名、Email、手機、LINE、產業、地址（自動帶入 Profile） | ✅ |
| 9 | Step 3 折扣 | /register/{cohortId} | 折扣碼驗證 + 價格摘要（原價 - 早鳥 - 折扣 = 應付） | ✅ |
| 10 | 送出報名 | /register/{cohortId} | 建立報名記錄 → 跳轉結帳頁 | ✅ |

### A4. 付款

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 11 | 結帳頁 | /checkout/{orderId} | 訂單摘要 + 付款方式（信用卡/ATM）+ 發票 | ✅ |
| 12 | 綠界付款 | 外部導向 | ECPay sandbox 付款 | ✅ |
| 13 | 付款成功 | /register/success/{orderId} | 自動 redirect 回成功頁 | ✅ |
| 14 | 付款失敗 | /checkout/failed | redirect 回失敗頁 | ✅ |

### A5. 學員個人中心

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 15 | 個人 Profile | [/student/profile](https://cnc-navicareer.web.app/student/profile) | 編輯姓名、手機、LINE、產業、地址 | ✅ |
| 16 | 報名歷史 | [/student/enrollments](https://cnc-navicareer.web.app/student/enrollments) | 查詢報名紀錄 + 狀態 badge + 付款按鈕 | ✅ |

### A6. 名額連動（可配置）

| # | 測試說明 | 規則 | 狀態 |
|---|---------|------|------|
| 17 | 名額連動 | A+B+C / A+B 佔 A+B 池，A only 佔 A 池（seat_rules JSON 可配置） | ✅ |
| 18 | 額滿擋報名 | 任一池歸零 → 擋住需要該池的班別 | ✅ |
| 19 | 退課回補 | 退課核准 → 對應池名額 +1 | ✅ |

### A7. Email 通知

| # | 通知類型 | 觸發時機 | 狀態 |
|---|---------|---------|------|
| 20 | 報名確認信 | 送出報名後自動寄出 | ✅ |
| 21 | 付款成功信 | 付款完成後自動寄出 | ✅ |
| 22 | 退課通知信 | Admin 核准退課後寄出 | ✅ |
| 23 | 退款通知信 | Admin 處理退款後寄出（含退款金額 + 預計時間） | ✅ |
| 24 | 課前提醒信 | 開課前寄出（含日期、時間、地點、行前提醒） | ✅ |

---

## Part B：管理後台

### B1. Dashboard

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 25 | 數據總覽 | [/admin/dashboard](https://cnc-navicareer.web.app/admin/dashboard) | 總報名數、待付款、已付款、待退款統計 + 近期報名 | ✅ |

### B2. 梯次管理

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 26 | 梯次 CRUD | [/admin/cohorts](https://cnc-navicareer.web.app/admin/cohorts) | 新增/編輯/刪除梯次（日期、價格、名額、封面、文案） | ✅ |
| 27 | 教室容量 | /admin/cohorts | A教室 + B教室容量設定、seat_rules 配置 | ✅ |
| 28 | 狀態切換 | /admin/cohorts | planning → registration → in_progress → completed | ✅ |

### B3. 報名管理

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 29 | 報名列表 | [/admin/enrollments](https://cnc-navicareer.web.app/admin/enrollments) | 所有報名，依付款狀態/報名狀態/梯次篩選 | ✅ |
| 30 | 確認轉帳 | /admin/enrollments | 手動確認銀行轉帳 → 狀態改 PAID | ✅ |
| 31 | 退課審核 | /admin/enrollments | 核准退課 → 狀態改 WITHDRAWN → 寄退課通知 | ✅ |

### B4. 折扣碼 & 退款

| # | 頁面 | 網址 | 測試說明 | 狀態 |
|---|------|------|---------|------|
| 32 | 折扣碼 CRUD | [/admin/promo-codes](https://cnc-navicareer.web.app/admin/promo-codes) | 建立/編輯/停用/刪除折扣碼（百分比/固定金額） | ✅ |
| 33 | 退款處理 | [/admin/refunds](https://cnc-navicareer.web.app/admin/refunds) | 待退款列表 + 退款審核 → 寄退款通知 | ✅ |

### B5. 權限與安全

| # | 測試說明 | 預期結果 | 狀態 |
|---|---------|---------|------|
| 34 | 學員打 admin API | 回 403 Forbidden | ✅ |
| 35 | 未帶 JWT 打 admin API | 回 401 Unauthorized | ✅ |

---

## Part C：待上線

| # | 項目 | 說明 | 狀態 |
|---|------|------|------|
| 36 | 綠界正式環境 | 切換正式商店金鑰（需向美荷取得） | ❌ 待上線 |
| 37 | GCP OAuth Client ID | Google 登入需 Client ID（需 GCP Console） | ❌ 待設定 |

---

## E2E 自動測試（Playwright）

14 項自動測試全數通過，測試對象為正式部署站 `cnc-navicareer.web.app`

| 測試檔案 | 覆蓋範圍 | 數量 |
|----------|---------|------|
| `a1-auth.spec.ts` | 註冊/登入表單、必填驗證、錯誤訊息 | 4 |
| `a2-courses.spec.ts` | 課程列表、課程介紹頁、報名按鈕 | 3 |
| `a3-registration.spec.ts` | 報名頁面、班別選擇、價格顯示 | 3 |
| `b4-security.spec.ts` | Admin 權限檢查、未認證 401 | 2 |
| `c1-responsive.spec.ts` | Desktop (1280x720) + Mobile (375x667) RWD | 2 |

---

## 備註

- 綠界目前為 **sandbox 測試環境**，不會實際扣款
- Email 由 `CC_BDS@careercreator.tw` 透過 Gmail SMTP 寄出
- 測試用帳號請用假 email，不要用真實客戶 email
- 名額連動規則透過 `seat_rules` JSON 配置，預設：A+B+C / A+B 佔 A+B 池，A only 佔 A 池
