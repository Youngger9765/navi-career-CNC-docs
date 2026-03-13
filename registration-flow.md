---
layout: default
title: "報名系統流程"
---

# CNC 報名系統 — 線上報名流程

## 1. 流程用途

本系統提供 CNC 職涯導航師培訓的**線上報名與付款功能**，取代原本的 Google Forms + 人工對帳流程。

### 報名流程（學員端）

```
課程介紹頁 → 選擇梯次 → 填寫個人資料 → 輸入折扣碼 → 確認金額 → 前往付款 → 完成報名
```

| 步驟 | 頁面 | 說明 |
|------|------|------|
| 1 | 課程列表 | 瀏覽開放報名的梯次，查看日期、價格、剩餘名額 |
| 2 | 課程介紹 | 課程內容、培訓師資、獨家牌卡工具介紹 |
| 3 | 報名表單 Step 1 | 選擇班別（A班 / A+B班 / B班升級）+ 即時名額顯示 |
| 4 | 報名表單 Step 2 | 填寫個人資料（姓名、Email、手機、LINE、產業、地址）|
| 5 | 報名表單 Step 3 | 折扣碼驗證 + 價格摘要（原價 - 早鳥 - 折扣 = 應付金額）|
| 6 | 結帳頁 | 選擇付款方式（信用卡/ATM/轉帳）+ 發票資訊 |
| 7 | 綠界付款 | 導向綠界 ECPay 金流頁面完成付款 |
| 8 | 成功頁 | 報名成功確認 + 下一步引導 |

### 管理流程（Admin 端）

| 功能 | 說明 |
|------|------|
| 梯次管理 | 建立/編輯梯次（日期、價格、名額、早鳥截止日）|
| 報名列表 | 查看所有報名，依付款狀態/梯次篩選 |
| 確認轉帳 | 手動確認銀行轉帳付款 |
| 退課審核 | 核准學員退課申請 + 退款處理 |
| 折扣碼管理 | 建立/停用折扣碼 |

### 系統特色

- **即時名額管理**：防超賣（資料庫鎖定機制）
- **彈性定價**：早鳥折扣 + 折扣碼（自動取最優折扣）
- **綠界金流**：信用卡（含分期）、ATM 虛擬帳號、銀行轉帳
- **自動狀態更新**：付款完成自動更新報名狀態

---

## 2. 網址

### 前台（學員）

| 頁面 | 網址 |
|------|------|
| 課程列表 | [cnc-navicareer.web.app/courses](https://cnc-navicareer.web.app/courses) |
| 課程介紹 | [cnc-navicareer.web.app/courses/cnc-career-consultant](https://cnc-navicareer.web.app/courses/cnc-career-consultant) |
| 報名表單 | cnc-navicareer.web.app/register/{cohortId} |
| 結帳頁 | cnc-navicareer.web.app/checkout/{orderId} |
| 報名成功 | cnc-navicareer.web.app/register/success/{orderId} |
| 登入 | [cnc-navicareer.web.app/login](https://cnc-navicareer.web.app/login) |
| 註冊帳號 | [cnc-navicareer.web.app/signup](https://cnc-navicareer.web.app/signup) |

### 後台 API

| 用途 | 網址 |
|------|------|
| API 文件（Swagger） | 請洽管理員取得 |
| 健康檢查 | 內部使用 |

---

## 3. 如何測試

### 前置準備

1. 開啟 [cnc-navicareer.web.app/signup](https://cnc-navicareer.web.app/signup) 註冊一個測試帳號
2. 登入後即可開始報名流程

### 測試情境 A：完整報名流程

```
1. 前往課程列表 → 點擊「CNC 職涯導航師培訓」
2. 點擊「立即報名」進入報名表單
3. Step 1：選擇班別（A班 或 A+B班）
4. Step 2：填寫個人資料
5. Step 3：（選填）輸入折扣碼 → 確認價格摘要
6. 點擊「前往付款」→ 進入結帳頁
7. 選擇付款方式 + 填寫發票資訊
8. 送出 → 導向綠界測試環境
```

> 目前綠界使用 **sandbox 測試環境**，不會產生實際扣款。

### 測試情境 B：API 直接測試

可透過 API 文件頁面（Swagger UI）測試各端點，包含：

- `GET /api/v1/cohorts` — 查看開放梯次
- `POST /api/v1/auth/register` — 註冊帳號
- `POST /api/v1/auth/login` — 登入取得 token
- `POST /api/v1/enrollments` — 建立報名（需登入）

### 已知限制（V1）

| 項目 | 狀態 |
|------|------|
| Google OAuth 登入 | 開發中 |
| 綠界正式環境 | 目前為 sandbox，正式上線需切換商店金鑰 |
| 退款通知 | Admin 核准退款後需手動通知學員 |
