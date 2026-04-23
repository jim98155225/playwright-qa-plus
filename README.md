# playwright-qa-plus

> **playwright-qa-extreme** 強化版 — 加入 SPA 實戰踩坑檢測
> AI-driven website QA: browser exploration → test specs → Playwright automation → HTML report

基於 [aster-life/playwright-qa-extreme](https://github.com/aster-life/playwright-qa-extreme)，加入 8 項從真實專案踩坑經驗中提煉的自動化檢測。

---

## 新增檢測項（Phase 2-D ~ 2-K）

| Phase | 檢測名稱 | 檢測什麼 | 來源教訓 |
|-------|---------|---------|---------|
| **2-D** | SPA 快取白屏 | JS chunk 404 後是否有 retry/reload | 部署新版後舊用戶白屏 |
| **2-E** | API 格式驗證 | Content-Type vs 實際內容一致性 | Vercel 504 回傳 HTML → `.json()` 炸 |
| **2-F** | CORS 稽查 | `*` + credentials 危險組合 | CORS `*` + cookie auth = CSRF |
| **2-G** | OAuth 流程 | In-app browser 偵測 + state 防 CSRF | LINE/FB 瀏覽器擋 Google OAuth |
| **2-H** | localStorage 安全 | Storage 被阻擋時 app 是否 crash | iframe/嚴格隱私模式 SecurityError |
| **2-I** | 效能基準線 | LCP/CLS/API latency | Supabase 自訂網域冷啟動 3 秒 |
| **2-J** | 多語系完整性 | 切換語言後有無 raw key 殘留 | 翻譯 key 未覆蓋全部語言 |
| **2-K** | crypto Polyfill | randomUUID 缺失時是否有 fallback | iOS < 15.4 不支援 |

---

## 原有功能（來自 playwright-qa-extreme）

| Phase | 工具 | 做什麼 |
|-------|------|--------|
| Phase 0 探察 | Claude_in_Chrome | AI 直接瀏覽網站，看畫面理解結構，自動切分測試模組 |
| Phase 0-B 規格 | Claude | 產出完整中文測試規格文件（7 大維度） |
| Phase 0-C Pre-Auth | Playwright | 建立登入 session，供後續模組使用 |
| Phase 1 執行 | Playwright + Claude_in_Chrome | 逐條驗收；歧義畫面交由 AI 判斷 |
| Phase 2-A | Claude_in_Chrome | Console/Network 直讀稽查 |
| Phase 2-B | Playwright | 表單邊界攻擊（XSS、SQL Injection、空值、超長） |
| Phase 2-C | Playwright | 500 錯誤雙重探測 |
| Phase 3 HitL | 人工 | OTP / 金流 / CAPTCHA 中斷處理 |
| Phase 4 報告 | Claude + Node.js | UAT 清單 + Bug 報告 + 自包含 HTML 報告 |

---

## 安裝

### 前置需求

| 項目 | 版本 |
|------|------|
| [Claude Code](https://claude.ai/download) | 最新版 |
| [Node.js](https://nodejs.org/) | v18+ |
| Claude_in_Chrome MCP | 需在 Claude Code 中已啟用 |

### macOS / Linux

```bash
git clone https://github.com/jim98155225/playwright-qa-plus.git
cp -r playwright-qa-plus ~/.claude/skills/playwright-qa-plus
npm install playwright --prefix /tmp/pw-test
# 重啟 Claude Code
```

---

## 使用

在 Claude Code 中輸入：

```
/qa-plus-audit https://your-website.com
QA 驗收模式：https://your-website.com
幫我測試這個網站：https://your-website.com
```

---

## 輸出

```
[Workspace]/
└── qa-reports/
    ├── specs/              # 測試規格文件
    ├── screenshots/        # 截圖證據
    ├── [模組]-uat-checklist.md
    ├── [模組]-qa-bug-report.md
    └── [專案名]-qa-report-[日期].html  ← 主整合報告（截圖 base64 內嵌）
```

---

## Credits

- 原始專案：[aster-life/playwright-qa-extreme](https://github.com/aster-life/playwright-qa-extreme)
- 強化版：基於 6 個真實 SPA 專案的 23+ 條踩坑記錄提煉

## License

MIT
