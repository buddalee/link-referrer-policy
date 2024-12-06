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

## 使用方式

1. 克隆此專案：
```bash
git clone https://github.com/your-username/referrer-policy-demo.git
```

2. 在瀏覽器中開啟 `index.html`
3. 點擊不同的連結觀察 referrer 行為差異

## 學習重點

1. **Referrer 基本概念**
   - Referrer 是什麼
   - 為什麼需要控制 Referrer
   - 安全性考量

2. **實作細節**
   - 如何設定 `rel="noreferrer"`
   - 如何讀取 `document.referrer`
   - 不同連結設定的效果

3. **應用場景**
   - 保護使用者隱私
   - 防止資訊洩漏
   - SEO 考量

4. **GA4 流量追蹤觀察**
   - 即使連結設定 `rel="noreferrer"`，GA4 仍能追蹤流量來源
   - GA4 使用不同的追蹤機制（如 Client ID、Campaign Parameters）
   - 流量來源報表中可觀察到完整的使用者路徑
   - 實務上對資料分析的影響

## 重要觀察

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

## 注意事項

- 需要使用網頁伺服器來運行（直接開啟檔案可能無法正確顯示結果）
- 不同瀏覽器可能有略微不同的行為
- 建議搭配瀏覽器的開發者工具觀察網路請求
- 建議同時觀察 GA4 報表以了解實際追蹤效果


## 授權條款

MIT License - 請自由使用於教學或學習用途
