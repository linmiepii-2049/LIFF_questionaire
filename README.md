# LIFF 自架後端

這是一個為 LINE Front-end Framework (LIFF) 應用提供後端服務的 Node.js 專案，主要負責處理前端請求、第三方 API 代理、Google Sheets 操作以及跨來源資源共享 (CORS) 處理。

## 專案特色

- **代理服務**: 為前端提供第三方 API 請求代理，解決 CORS 限制
- **Google Sheets 整合**: 透過 Apps Script Web API 進行 Google Sheets 資料操作
- **CORS 安全**: 實作安全的跨來源請求處理機制
- **Cloud Functions 支援**: 可部署至雲端函數平台

## 技術架構

```
前端 LIFF 應用
    ↓
Node.js 代理後端
    ↓
├── 第三方 API
├── Google Sheets (via Apps Script)
└── Cloud Functions / 中間伺服器
```

## 環境需求

- Node.js 16+ 
- npm 或 yarn
- Google Cloud Platform 帳戶 (選用)

## 安裝指引

1. **複製專案**
   ```bash
   git clone <repository-url>
   cd LIFF自架後端
   ```

2. **安裝依賴**
   ```bash
   npm install
   ```

3. **環境設定**
   ```bash
   cp .env.example .env
   ```
   編輯 `.env` 檔案並設定以下變數：
   ```
   PORT=3000
   NODE_ENV=development
   CORS_ORIGIN=https://your-liff-domain.com
   GOOGLE_SHEETS_API_URL=https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec
   ```

4. **啟動開發伺服器**
   ```bash
   npm run dev
   ```

## 使用方法

### API 端點

#### 健康檢查
```
GET /health
```

#### 代理請求
```
POST /api/proxy
Content-Type: application/json

{
  "url": "https://api.example.com/data",
  "method": "GET",
  "headers": {...},
  "data": {...}
}
```

#### Google Sheets 操作
```
POST /api/sheets
Content-Type: application/json

{
  "action": "read|write|append",
  "range": "A1:B10",
  "values": [...]
}
```

## CORS 設定

專案已預設安全的 CORS 設定，遵循以下原則：

- ✅ 明確指定允許的來源域名
- ✅ 列出具體的 HTTP 方法和標頭
- ✅ 適當處理憑證攜帶請求
- ❌ 避免使用通配符 `*` 搭配憑證
- ❌ 禁止 `null` 來源

## 部署

### Cloud Functions (推薦)
```bash
npm run deploy:cloud-functions
```

### Docker
```bash
docker build -t liff-backend .
docker run -p 3000:3000 liff-backend
```

### 傳統伺服器
```bash
npm run build
npm start
```

## 開發規範

### 程式碼品質
- 使用繁體中文撰寫所有註解與文件
- 遵循單一職責原則
- 避免硬編碼資料
- 集中管理錯誤處理

### 安全考量
- 驗證所有輸入參數
- 實作適當的 CORS 政策
- 保護敏感資訊
- 記錄重要操作

## 故障排除

### 常見問題

**Q: CORS 錯誤**
```
解決方案：檢查 CORS_ORIGIN 環境變數是否正確設定前端域名
```

**Q: Google Sheets API 失敗**
```
解決方案：確認 Apps Script 已部署為公開 Web 應用程式
```

**Q: 代理請求超時**
```
解決方案：檢查目標 API 可用性及網路連線狀態
```

## 貢獻指引

1. Fork 專案
2. 建立功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交變更 (`git commit -m 'Add amazing feature'`)
4. 推送分支 (`git push origin feature/amazing-feature`)
5. 建立 Pull Request

## 授權條款

本專案採用 MIT 授權條款。詳見 [LICENSE](LICENSE) 檔案。

## 聯絡資訊

如有問題或建議，請建立 Issue 或聯絡專案維護者。

---

*最後更新：2024年8月* 