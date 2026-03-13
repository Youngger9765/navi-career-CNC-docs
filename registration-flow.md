---
layout: default
title: "報名系統 QA 表"
---

# CNC 報名系統 — QA 測試表

```
課程介紹 → 選擇梯次 → 填寫個資 → 折扣碼 → 確認金額 → 付款 → 完成報名
```

| 步驟 | 頁面 | 網址 | 測試說明 | 是否實作 |
|------|------|------|---------|---------|
| 1 | 註冊帳號 | [/signup](https://cnc-navicareer.web.app/signup) | 填 email + 密碼 + 姓名，註冊成功自動登入 | ✅ |
| 2 | 登入 | [/login](https://cnc-navicareer.web.app/login) | Email + 密碼登入，錯誤時顯示提示 | ✅ |
| 3 | Google 登入 | [/login](https://cnc-navicareer.web.app/login) | 點 Google 按鈕 → OAuth 授權 → 登入 | ❌ 開發中 |
| 4 | 課程列表 | [/courses](https://cnc-navicareer.web.app/courses) | 顯示所有開放報名梯次，含日期、價格、剩餘名額 | ✅ |
| 5 | 課程介紹 | [/courses/cnc-career-consultant](https://cnc-navicareer.web.app/courses/cnc-career-consultant) | 課程內容、師資、牌卡工具照片、即時價格 | ✅ |
| 6 | 報名 Step 1 選課 | /register/{cohortId} | 選班別（A/A+B/B升級），即時名額條，早鳥 badge | ✅ |
| 7 | 報名 Step 2 個資 | /register/{cohortId} | 姓名、Email、手機、LINE、產業、地址，必填驗證 | ✅ |
| 8 | 報名 Step 3 折扣 | /register/{cohortId} | 輸入折扣碼驗證 + 價格摘要（原價-早鳥-折扣=應付） | ✅ |
| 9 | 送出報名 | /register/{cohortId} | 按「前往付款」→ 建立報名記錄 → 跳轉結帳頁 | ✅ |
| 10 | 報名確認信 | — | 報名成功後自動寄 Email 確認信 | ✅ |
| 11 | 結帳頁 | /checkout/{orderId} | 訂單摘要 + 選付款方式（信用卡/ATM/轉帳）+ 發票 | ✅ |
| 12 | 綠界付款 | 外部導向 | 導向 ECPay 完成付款（目前 sandbox 不扣款） | ✅ |
| 13 | 付款成功 | /register/success/{orderId} | 綠界付款成功 → 自動 redirect 回成功頁 | ✅ |
| 14 | 付款失敗 | /checkout/failed | 綠界付款失敗 → redirect 回失敗頁 | ✅ |
| 15 | 付款成功信 | — | 付款完成後自動寄 Email 通知 | ✅ |
| 16 | 狀態自動更新 | — | ECPay webhook 回調 → DB 報名狀態更新為 PAID | ✅ |
| 17 | 名額即時扣減 | — | 報名成功 → 剩餘名額 -1，額滿擋報名 | ✅ |
| 18 | 退課後回補名額 | — | 退課核准 → 剩餘名額 +1 | ✅ |
| 19 | Admin 梯次管理 | API only | 建立/編輯/刪除梯次（日期、價格、名額） | ✅ |
| 20 | Admin 報名列表 | API only | 查看所有報名，依狀態/梯次篩選 | ✅ |
| 21 | Admin 確認轉帳 | API only | 手動確認銀行轉帳付款 | ✅ |
| 22 | Admin 退課審核 | API only | 核准退課申請 + 退款處理 | ✅ |
| 23 | Admin 折扣碼管理 | API only | 建立/停用折扣碼 | ✅ |
| 24 | Admin 權限檢查 | API only | 一般學員打 admin API → 403 Forbidden | ✅ |
| 25 | 升級申請 | API only | A班 → A+B班升級，補差額 | ✅ |
| 26 | RWD 手機版 | 同上所有頁面 | iPhone Safari / Android Chrome 排版正確 | ✅ |
| 27 | 綠界正式環境 | — | 切換正式商店金鑰（目前 sandbox） | ❌ 待上線 |
| 28 | Admin 管理後台 UI | — | 前端管理介面（目前僅 API） | ❌ 待開發 |
