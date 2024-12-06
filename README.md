# Referrer Policy Demo
> 🔍 A simple demonstration of how referrer policies work in HTML links

一個簡單的網頁專案，用於展示和學習 HTML 中的 referrer policy（引薦來源政策）如何運作。適合網頁開發初學者和實習生學習使用。

## 專案說明

這個專案展示了 HTML 連結中 referrer policy 的實際運作方式，幫助開發者理解：
- 預設的 referrer 行為
- 如何控制 referrer 資訊的傳遞
- 使用 `rel="noreferrer"` 的效果
- GA4 追蹤行為差異

## 檔案結構

```
referrer-policy-demo/
├── index.html      # 主頁面，包含不同設定的連結
├── result.html     # 結果頁面，顯示 referrer 資訊
└── README.md       # 說明文件
```

## 重要概念

### Referrer 是什麼？

HTTP Referer（注意拼寫中缺少一個 r）是一個 HTTP header，用於標識使用者是從哪個網頁連結過來的。當使用者點擊連結或提交表單時，瀏覽器會自動將當前頁面的 URL 作為 Referer 傳送給目標網站。

```
當使用者從 https://example.com/page1.html 點擊連結到 https://example.com/page2.html
HTTP 請求會包含：
Referer: https://example.com/page1.html
```

### 為什麼需要控制 Referrer？

1. **隱私保護**
   - 防止洩露敏感的 URL 參數
   - 避免暴露內部系統結構
   - 保護使用者瀏覽歷史

2. **商業敏感資訊保護**
   - 防止競爭對手分析流量來源
   - 保護內部營銷活動資訊
   - 避免暴露未公開的促銷連結

3. **跨域安全**
   - 減少跨站請求偽造（CSRF）風險
   - 控制第三方網站能獲取的資訊

### 安全性考量

#### 潛在風險
1. **URL 參數洩露**
   ```
   https://bank.com/account?id=12345&token=abc123
   ```
   - 若不控制 referrer，敏感參數可能洩露給第三方網站

2. **系統結構暴露**
   ```
   https://company.com/internal/admin/users
   ```
   - URL 結構可能暴露系統架構和權限層級

3. **身分驗證資訊**
   ```
   https://app.com/dashboard?session=xyz789
   ```
   - 認證 token 可能經由 referrer 外洩

#### 保護措施

1. **頁面級別控制**
   ```html
   <meta name="referrer" content="no-referrer">
   ```

2. **連結級別控制**
   ```html
   <a href="..." rel="noreferrer">
   ```

3. **伺服器端配置**
   ```apache
   Referrer-Policy: no-referrer-when-downgrade
   ```

## GA4 流量追蹤觀察

### GA4 與 Referrer Policy 的關係
- `rel="noreferrer"` 主要影響瀏覽器層級的 referrer 資訊傳遞
- GA4 透過自己的追蹤機制，不受 referrer policy 影響：
  - 使用 first-party cookies
  - 追蹤使用者會話
  - 記錄完整的使用者行為路徑
- 即使網頁間的連結設定了 `noreferrer`，GA4 報表中仍能看到：
  - 使用者來源
  - 轉換路徑
  - 完整的使用者旅程

## 使用方式

1. 克隆此專案：
```bash
git clone https://github.com/your-username/referrer-policy-demo.git
```

2. 在瀏覽器中開啟 `index.html`
3. 點擊不同的連結觀察 referrer 行為差異

## 最佳實踐建議

1. **敏感頁面**
   - 一律使用 no-referrer policy
   - 避免在 URL 中包含敏感資訊
   - 實作適當的 CSRF 保護

2. **一般頁面**
   - 使用 same-origin 或 strict-origin policy
   - 注意第三方連結的 referrer 控制
   - 定期審查 referrer 相關設定

3. **開發建議**
   - 使用 POST 而非 GET 傳送敏感資料
   - 實作適當的權限檢查機制
   - 不依賴 referrer 作為安全控制

## 注意事項

- 需要使用網頁伺服器來運行（直接開啟檔案可能無法正確顯示結果）
- 不同瀏覽器可能有略微不同的行為
- 建議搭配瀏覽器的開發者工具觀察網路請求
- 建議同時觀察 GA4 報表以了解實際追蹤效果

