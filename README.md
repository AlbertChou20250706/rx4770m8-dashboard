# rx4770m8-dashboard
RX4770M8‑T50‑2 Test Status Dashboard
# RX4770M8‑T50‑2 Test Status Dashboard

**作者**: Albert Chou  
**初版時間**: 2025‑12‑08  
**目前版本**: v0.3.0

---

## 1. 專案目的

本頁面用於追蹤 RX4770M8‑T50‑2 專案測試進度，包含：

- 依 **工程師(Owner/Tester)** 的每日進度格線 (Progress Grid)
- 每日 PASS / FAIL / BLOCK 數量統計
- Summary table (legacy)：保留接近 Excel 的原始紀錄格式
- 匯出 CSV / Excel 報表

---

## 2. 檔案結構

- `RX4770M8-T50-2 Test Status.html`
  - 靜態 HTML + CSS + JavaScript，無其他外部依賴 (除 CDN 的 Chart.js / SheetJS)
  - 主要區塊：
    - Header 工具列（語言切換 / Theme 切換 / 匯出 / Reset）
    - Controls 區 (起始日期、專案週數、假日設定等)
    - **Detail input** 區 (Tester / Detail Status / Sheet / Line / Date / Result / Count)
    - 個人 Progress Grid (依 Owner x Date 顯示進度與 P/F/B 百分比)
    - Total progress (all engineers)
    - Summary table (legacy) + 篩選器

---

## 3. 執行方式

1. 使用瀏覽器直接開啟 `RX4770M8-T50-2 Test Status.html`
2. 建議使用 Chrome / Edge 最新版
3. 所有資料儲存在瀏覽器 `localStorage`，目前不會上傳到伺服器

---

## 4. 版本與歷史紀錄 (Changelog)

> 註：以下只是範例，你可以照實際變更日期與內容補上。

### v0.3.0 – 2025‑12‑09 – 設計者: Albert Chou

**目的**:  
- 加入 Summary table 篩選功能  
- 加總全體工程師的 Total progress，限制 P/F/B 總和不超過 100%  

**主要變更**:
- 新增篩選欄位：Tester / Detail / Sheet / Line / Date / PASS / FAIL / BLOCK 條件
- 新增 Total progress (all engineers) 圖條在 Detail input 區塊下方
- 更新 i18n 文案，加入 `label_total_progress` 與 `warn_over_100`

### v0.2.0 – 2025‑12‑08 – 設計者: Albert Chou

**目的**:  
- 將測試細項輸入改為對應 Excel 欄位 (Tester / Detail status / Sheet / Line)
- 增加 Sheet / DetailStatus 選單內容

**主要變更**:
- 新增 `DETAIL_STATUS_OPTIONS`：
  - `TSR_OS_Configurator_Linux_Oracle`
  - `TSR_OS_Configurator_Linux_SuSE`
  - `TSR_OS_Maintenance_R1.2.0_SIT`
  - `TSR_SW_Configurator_Linux_SuSE`
- 新增 `SHEET_OPTIONS`：
  - `TR SAS RAID Adapter`, `TR SAS Adapter`, `TR other Adapter`, `TR LAN Adapter`,
  - `TR_OS_Regression`, `TR FC Adapter`, `TR Linux OL EL 10`, `TR ASP`,
  - `TR Systemboard`, `TR Linux SuSE SLES 16`

### v0.1.0 – 2025‑12‑08 – 設計者: Albert Chou

**目的**:  
- 建立最初版進度總覽與個人 Progress Grid

**主要變更**:
- 基本 UI 佈局、主題切換、語言切換
- Progress Grid Row 以 Owner 呈現，顯示每日進度條與日期
- 匯出 CSV / Excel 功能雛型

---

## 5. 工程師建議可修改／擴充的範圍

以下區域歡迎其他工程師依專案需求修改，**但請記得更新上面的 Changelog 區段**：

1. **樣式 / 佈局 (CSS)**  
   - 可以修改 `:root` 色票、`body.theme-*`、`.card` 等外觀。  
   - 可調整 Progress Grid cell 大小 (`.day-cell`, `.progress-bar-mini` 等)。

2. **Detail 下拉選單選項**  
   - `DETAIL_STATUS_OPTIONS`  
   - `SHEET_OPTIONS`  
   - 若新增/刪除選項，請在 Changelog 寫清楚。

3. **Summary table (legacy) 欄位與匯出格式**  
   - 欄位順序、顯示名稱、匯出 CSV/XLSX 的欄位對應。  
   - 若增加新欄位，務必同步更新匯出邏輯。

4. **假日/工作日計算規則**  
   - 函式：`isWeekendISO`, `buildCalendar`, `countWorkdays`  
   - 目前週末為六日，如需調整（例如支援輪班），可以在此改。

5. **Progress 計算與上限邏輯**  
   - 個人進度 / 全體進度上限 (P/F/B Total ≤ 100%)  
   - 對應的提示文字 `warn_over_100` 可以依實務需求調整。

6. **本地儲存 (localStorage) Key 與資料格式**  
   - 函式：`safeLoad`, `safeSave`  
   - State: `engineers`, `holidays`, `leader`, `detailRows` 等。  
   - 如要調整儲存結構，請建立版本轉換邏輯，避免使用者舊資料毀損。

---

## 6. 進版規則建議

每次修改 `RX4770M8-T50-2 Test Status.html`：

1. 在 `README.md` 的 Changelog 新增一個版本條目：
   - 版本號 (例如 `v0.3.1`)
   - 日期時間 (YYYY‑MM‑DD HH:MM)
   - 設計者 (例如 `Albert Chou` 或工程師名稱)
   - 修改目的與重點 (1–3 點)
2. 若你的組織有 Git：
   - Commit message 建議格式:  
     `feat: ...`, `fix: ...`, `chore: ...` 等  
   - Tag 可用 `v0.x.y` 對應 README 版本。

---
