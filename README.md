# DBX 完全指南 — 15MB 輕量級跨平台資料庫客戶端

> GitHub: [t8y2/dbx](https://github.com/t8y2/dbx) | License: Apache-2.0 | 約 2,385 commits | 持續活躍開發中

---

## 目錄

1. [DBX 是什麼？](#1-dbx-是什麼)
2. [為什麼選 DBX？（對比分析）](#2-為什麼選-dbx對比分析)
3. [支援的資料庫完整列表](#3-支援的資料庫完整列表)
4. [各平台安裝方式](#4-各平台安裝方式)
5. [功能詳解](#5-功能詳解)
6. [AI 功能深入說明](#6-ai-功能深入說明)
7. [MCP 協議 — 讓 AI 直接操作資料庫](#7-mcp-協議--讓-ai-直接操作資料庫)
8. [CLI 命令列工具](#8-cli-命令列工具)
9. [Docker 部署與 Web 版](#9-docker-部署與-web-版)
10. [從其他工具遷移](#10-從其他工具遷移)
11. [常見問題 FAQ](#11-常見問題-faq)
12. [開發與貢獻](#12-開發與貢獻)

---

## 1. DBX 是什麼？

DBX 是一款**開源、免費、極輕量**的跨平台資料庫管理工具，由開發者 [t8y2](https://github.com/t8y2) 用 Rust 開發。

### 核心特點

| 特性 | 說明 |
|------|------|
| 體積 | **僅 15MB**，單一二進制檔案 |
| 依賴 | 零執行時依賴。不需要 Java JRE、不需要 Python、不內嵌 Chromium |
| 平台 | macOS / Windows / Linux 原生 + Docker 自託管 + Web 版 |
| 資料庫 | 支援 **50+** 種資料庫，涵蓋關聯式、NoSQL、時序、搜尋引擎 |
| AI | 內建 AI SQL 生成、解釋、優化，支援 Claude / OpenAI / Ollama 本地模型 |
| MCP | 原生支援 Model Context Protocol，讓 AI Coding Agent 直接查詢資料庫 |
| 授權 | Apache-2.0，完全免費，所有功能不收費 |
| 隱私 | 零遙測，不回傳任何數據 |

### 一句話總結

> DBX = DBeaver 的功能 + TablePlus 的輕量 + AI 原生內建 + MCP 協議支援，全部塞進 15MB。

---

## 2. 為什麼選 DBX？（對比分析）

### 與主流工具的橫向對比

| 維度 | DBX | DBeaver | TablePlus | Navicat | Beekeeper Studio |
|------|-----|---------|-----------|---------|------------------|
| 體積 | **15MB** | 100MB+ (需 Java) | ~50MB | ~200MB | ~100MB |
| 平台 | **Win/Mac/Linux/Docker/Web** | Win/Mac/Linux | **僅 macOS** | Win/Mac/Linux | Win/Mac/Linux |
| 開源 | ✅ Apache-2.0 | ✅ Apache-2.0 | ❌ 閉源 | ❌ 付費 | ❌ 部分開源 |
| 免費 | ✅ 全功能 | ✅ | ❌ 功能受限 | ❌ 昂貴 | ❌ 功能受限 |
| AI 內建 | ✅ 原生 | ❌ 無 | ❌ 無 | ❌ 無 | ❌ 無 |
| MCP 協議 | ✅ 原生 | ❌ | ❌ | ❌ | ❌ |
| 支援 DB 數 | 50+ | 80+ | 20+ | 30+ | 10+ |
| SSH 隧道 | ✅ | ✅ | ✅ | ✅ | ✅ |
| ER 圖 | ✅ | ✅ | ✅ | ✅ | ❌ |
| Schema Diff | ✅ | ✅ | ❌ | ✅ | ❌ |
| 資料遷移 | ✅ | ✅ | ❌ | ✅ | ❌ |

### 什麼情況下 DBX 特別適合你

- 不想裝 Java 執行環境（DBeaver 痛點）
- 需要在 Windows / Mac / Linux 之間切換，使用一致的工具
- 想要 AI 直接幫你寫 SQL，不用在 ChatGPT 和編輯器之間複製貼上
- 用 Claude Code / Cursor / Windsurf 寫程式，想讓 AI 直接查你的資料庫
- 需要在伺服器上部署一個輕量的 Web 版資料庫管理工具
- 需要操作 Redis / MongoDB / DuckDB 這類非傳統 SQL 資料庫

---

## 3. 支援的資料庫完整列表

### 原生驅動（內建支援，開箱即用）

| 類別 | 資料庫 |
|------|--------|
| 關聯式 SQL | MySQL, PostgreSQL, SQLite, MariaDB, CockroachDB |
| 雲原生 / 分散式 | TiDB, OceanBase, openGauss, GaussDB, KingBase, Vastbase, GoldenDB |
| OLAP / 分析 | ClickHouse, DuckDB, Doris, SelectDB, StarRocks |
| 微軟生態 | SQL Server, Access |
| Oracle 生態 | Oracle, MySQL (Oracle 分支) |
| NoSQL | MongoDB, Redis |
| 搜尋引擎 | Elasticsearch, Manticore Search |
| 時序資料庫 | TDengine |
| 其他 | DM (達夢), XuguDB (虛谷), HighGo (瀚高), KWDB (卡瓦), Redshift |

### Agent / JDBC 擴展（透過插件載入）

| 類別 | 資料庫 |
|------|--------|
| 大數據 | Snowflake, Trino, Hive, Spark SQL |
| 傳統企業 | DB2, Informix, Teradata, SAP HANA, Vertica |
| 雲端倉儲 | BigQuery, Databricks |
| 圖資料庫 | Neo4j |
| 其他 | Cassandra, Firebird, Exasol, Kylin, SunDB, YashanDB, GBase, Databend |
| 嵌入式 | RQLite, Turso, InfluxDB, QuestDB, IoTDB, etcd, IRIS |
| Java 生態 | H2（透過 JDBC） |

---

## 4. 各平台安裝方式

### macOS

```bash
# Homebrew（推薦）
brew install --cask dbx
```

直接下載 `.dmg`：從 [Releases](https://github.com/t8y2/dbx/releases/latest) 下載最新版。

### Windows

```bash
# Scoop（推薦）
scoop bucket add dbx https://github.com/t8y2/scoop-bucket
scoop install dbx

# WinGet
winget install t8y2.dbx
```

或下載 `.msi` / `.exe` 安裝包。

### Linux

```bash
# Ubuntu / Debian — 下載 .deb 後安裝
sudo dpkg -i dbx_*.deb

# 其他發行版 — 使用 AppImage
chmod +x dbx_*.AppImage
./dbx_*.AppImage
```

前置依賴（僅 Ubuntu/Debian 桌面環境需要）：

```bash
sudo apt-get install -y libwebkit2gtk-4.1-dev libgtk-3-dev \
  libappindicator3-dev librsvg2-dev patchelf libssl-dev
```

### Docker（伺服器 / NAS 部署，Web 版）

```bash
docker run -d \
  --name dbx \
  -p 4224:4224 \
  -v dbx-data:/app/data \
  t8y2/dbx
```

開啟瀏覽器訪問 `http://localhost:4224`，支援 amd64 和 arm64。

Docker Compose：

```yaml
services:
  dbx:
    image: t8y2/dbx
    ports:
      - "4224:4224"
    volumes:
      - dbx-data:/app/data
    restart: unless-stopped

volumes:
  dbx-data:
```

---

## 5. 功能詳解

### 5.1 SQL 查詢編輯器

| 功能 | 說明 |
|------|------|
| 編輯引擎 | CodeMirror 6，支援 SQL 語法高亮 |
| 智能補全 | 基於 metadata 的自動補全（表名、欄位名） |
| 快捷執行 | `Cmd+Enter`（macOS）/ `Ctrl+Enter`（Windows/Linux）執行全部或選中 SQL |
| 格式化 | 內建 SQL 格式化 |
| 診斷 | SQL 語法即時檢查 |
| 主題 | 9 種編輯器主題可選 |
| 歷史 | 持久化查詢歷史記錄 |
| 片段 | 儲存常用 SQL 片段，一鍵插入 |
| 分頁還原 | 關閉重開後自動恢復上次開啟的頁籤 |
| 檔案執行 | 直接執行 `.sql` 檔案 |

### 5.2 資料瀏覽與編輯

| 功能 | 說明 |
|------|------|
| 虛擬滾動 | 大數據集流暢滾動，不阻塞 UI |
| 行內編輯 | 直接在表格中修改資料 |
| SQL 預覽 | 提交修改前預覽產生的 SQL |
| 過濾 | DataGrip 風格過濾器 + LIKE / NOT LIKE 上下文過濾 |
| 全文搜索 | 在結果集中全文搜索 |
| 排序 | 點擊欄位標題排序 |
| 分頁 | 內建分頁控制 |
| 欄位操作 | 調整欄寬、自動適應、欄位隱藏 |
| 顯示 | 行號、斑馬條紋 |
| 儲存格詳情 | 點擊查看完整儲存格內容 |

### 5.3 匯出格式

支援將查詢結果匯出為多種格式：

| 格式 | 用途 |
|------|------|
| CSV | 通用資料交換 |
| JSON | API / 程式開發 |
| Markdown | 文件 / 筆記 |
| XLSX | Excel 分析 |
| INSERT 語句 | 資料遷移 / 備份 |

### 5.4 Schema 管理

| 功能 | 說明 |
|------|------|
| Schema 瀏覽器 | 樹狀瀏覽資料庫、Schema、表、欄位、索引、外鍵、觸發器 |
| 側欄搜索 | 在大型 Schema 中快速搜索物件 |
| 物件瀏覽器 | 分組查看 Procedure、Function、View，支援原始碼編輯 |
| 表結構編輯器 | 可視化編輯欄位和索引（支援的引擎） |
| ER 圖 | 可視化表之間關聯 |
| Schema Diff | 比較不同連線之間的結構差異 |
| Explain Plan | 視覺化查詢執行計劃 |
| 欄位血緣 | 欄位級別的血緣分析 |
| 資料庫搜索 | 在大型 Schema 中跨物件搜索 |

### 5.5 資料遷移與匯入

| 功能 | 說明 |
|------|------|
| 表匯入 | 從 CSV / Excel 匯入資料 |
| 資料傳輸 | 跨資料庫遷移（例如 MySQL → PostgreSQL） |
| 全庫匯出 | 完整資料庫 dump |
| 資料比對 | 比較兩張表的資料差異，審查同步輸出 |
| 檔案預覽 | **拖放** Parquet / CSV / JSON 檔案即時預覽（由 DuckDB 驅動） |
| 連線匯入 | 從 DBeaver 或 Navicat 匯入連線設定 |

### 5.6 NoSQL 專屬功能

**Redis：**
- Key 模式搜索
- 批量 Key 操作
- 命令執行器
- TTL 編輯
- 支援全部資料類型：String, Hash, List, Set, ZSet, Stream

**MongoDB：**
- 文件 CRUD 含分頁
- Atlas 連線字串支援
- Replica Set URL 連線

### 5.7 安全與連線

| 功能 | 說明 |
|------|------|
| SSH 隧道 | 支援金鑰認證和密碼認證 |
| 代理 | 資料庫代理和 AI 代理設定 |
| 自動重連 | 連線中斷後自動重連 |
| 破壞性操作確認 | DELETE / DROP / TRUNCATE 操作強制確認對話框 |
| 加密 | 設定檔加密匯出 / 匯入 |
| 顏色標記 | 為不同連線設定顏色，防止誤操作 |

### 5.8 介面與體驗

| 功能 | 說明 |
|------|------|
| 深色模式 | 跟隨系統標題列自動同步 |
| 語言 | English / 简体中文 / Español |
| 佈局偏好 | 可自訂面板位置 |
| 自動更新 | 內建自動更新（檢查 GitHub Releases，可關閉） |

---

## 6. AI 功能深入說明

DBX 的 AI 功能**直接內建在編輯器中**，不需要在 DBX 和 ChatGPT 之間來回複製貼上。

### 支援的模型

| 提供商 | 說明 |
|--------|------|
| Claude (Anthropic) | 需要 API Key |
| OpenAI (GPT-4o 等) | 需要 API Key |
| Ollama | **完全本地**，不需聯網，不需 API Key |
| 任何 OpenAI 相容端點 | 自訂 endpoint，支援各種第三方模型 |

### AI 能做什麼

| 功能 | 操作方式 |
|------|----------|
| 自然語言 → SQL | 選中一張表，用自然語言描述需求，AI 生成 SQL |
| SQL 解釋 | 選中一段 SQL，AI 解釋這段 SQL 在做什麼 |
| SQL 優化 | AI 分析 SQL 並給出優化建議 |
| 錯誤修復 | SQL 報錯時，AI 幫你診斷並修正 |
| 安全檢查 | AI 生成的 SQL 執行前，內建安全檢查機制審查 |

### 使用場景示例

```
你選中 "orders" 表，輸入：
「列出上個月銷售額最高的 10 個客戶，包含他們的總消費金額」

→ AI 自動生成：
SELECT customer_id, c.name, SUM(amount) as total
FROM orders o JOIN customers c ON o.customer_id = c.id
WHERE o.order_date >= '2026-05-01' AND o.order_date < '2026-06-01'
GROUP BY customer_id, c.name
ORDER BY total DESC
LIMIT 10;
```

---

## 7. MCP 協議 — 讓 AI 直接操作資料庫

### 什麼是 MCP？

Model Context Protocol（MCP）是 Anthropic 提出的開放協議，讓 AI 應用可以安全地存取外部工具和資料來源。DBX 實作了 MCP Server，讓 AI Coding Agent 可以透過 DBX 的連線直接查詢資料庫。

### 支援的 AI 工具

- **Claude Code**（Anthropic 官方 CLI）
- **Cursor**（AI 程式編輯器）
- **Windsurf**（AI IDE）
- 任何 MCP 相容的 Agent

### 設定方式

在你的專案根目錄建立 `.mcp.json`：

```json
{
  "mcpServers": {
    "dbx": {
      "command": "npx",
      "args": ["-y", "@dbx-app/mcp-server"]
    }
  }
}
```

### MCP Server 能做什麼

| 能力 | 說明 |
|------|------|
| 列出連線 | 讀取你在 DBX 中已設定的所有資料庫連線 |
| 瀏覽結構 | 瀏覽 Schema、表、欄位 |
| 執行查詢 | 執行 SELECT 查詢（只讀，不會執行寫入操作） |
| 開啟 DBX UI | 直接在 DBX 介面中打開指定的表 |

### 實際工作流程

```
你在 Claude Code 中：
「幫我查一下 users 表裡有多少個 email 沒驗證的用戶」

→ Claude Code 透過 MCP 連接 DBX
→ 自動讀取 users 表的 schema
→ 生成並執行正確的 SQL
→ 返回結果
```

全程不需要你手動打開 DBX、複製 schema、貼到 AI 工具。

---

## 8. CLI 命令列工具

DBX 提供獨立的 CLI 套件，用於終端機、腳本和自動化場景。

### 安裝

```bash
# npm
npm install -g @dbx-app/cli

# Homebrew
brew tap t8y2/dbx && brew install dbx-cli
```

### 常用指令

```bash
# 列出所有連線
dbx connections list --json

# 執行查詢
dbx query local "SELECT 1" --json

# 指定連線名稱
dbx query production "SELECT COUNT(*) FROM users"

# 匯出結果
dbx query local "SELECT * FROM orders WHERE status='pending'" --format csv > pending.csv
```

---

## 9. Docker 部署與 Web 版

### 為什麼要部署 Web 版？

- 團隊共用：一個 Docker 實例，多人透過瀏覽器訪問
- 伺服器管理：在無桌面的 Linux 伺服器上管理資料庫
- NAS 部署：在 Synology / QNAP 等 NAS 上執行
- 手機訪問：透過瀏覽器在手機 / 平板上查詢資料庫

### 部署方式

```bash
# 最簡單的一行部署
docker run -d --name dbx -p 4224:4224 -v dbx-data:/app/data t8y2/dbx
```

多架構支援（amd64 / arm64），樹莓派也能跑。

### Docker Compose（推薦用於生產環境）

```yaml
services:
  dbx:
    image: t8y2/dbx
    ports:
      - "4224:4224"
    volumes:
      - dbx-data:/app/data
    restart: unless-stopped
    environment:
      - TZ=Asia/Taipei

volumes:
  dbx-data:
```

### 反向代理（Nginx 示例）

```nginx
server {
    listen 443 ssl;
    server_name dbx.yourdomain.com;

    location / {
        proxy_pass http://localhost:4224;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
    }
}
```

---

## 10. 從其他工具遷移

### 從 DBeaver 遷移

DBX 支援**直接匯入 DBeaver 的連線設定**：

1. 打開 DBX → Settings → Connections
2. 點擊 Import
3. 選擇 DBeaver 的連線設定檔（通常在 `~/.dbeaver4/` 目錄下）
4. DBX 自動解析並匯入所有連線

### 從 Navicat 遷移

同樣支援匯入 Navicat 連線設定。

### 從 TablePlus 遷移

TablePlus 不支援匯出連線設定，需要手動在 DBX 中重新建立連線。

---

## 11. 常見問題 FAQ

**Q: DBX 真的完全免費嗎？**
A: 是的。Apache-2.0 開源授權，所有功能免費，沒有付費牆。

**Q: DBX 會收集我的資料嗎？**
A: 不會。DBX 零遙測，不回傳任何使用數據。自動更新功能僅檢查 GitHub Releases 是否有新版本（可關閉）。

**Q: 可以在完全離線的環境使用嗎？**
A: 桌面版可以。AI 功能如需離線使用，可搭配 Ollama 本地模型。驅動程式安裝可透過離線包匯入。

**Q: 和 DBeaver 比，少了什麼？**
A: DBeaver 支援約 80+ 資料庫（DBX 50+），DBeaver 有更豐富的插件生態。但 DBX 在體積、啟動速度、AI 整合、MCP 協議方面全面領先。

**Q: 支援中文嗎？**
A: 支援。介面已內建繁體中文 / 简体中文。

**Q: 有手機版嗎？**
A: 沒有原生 App，但可以部署 Docker Web 版，透過手機瀏覽器訪問。

**Q: 能在 Termux (Android) 上跑嗎？**
A: 桌面版不支援 Android。建議在伺服器上部署 Docker Web 版，手機瀏覽器訪問。

---

## 12. 開發與貢獻

### 技術棧

| 層 | 技術 |
|----|------|
| 桌面框架 | Tauri (Rust) |
| 前端 | React / TypeScript |
| 編輯器 | CodeMirror 6 |
| 建置工具 | pnpm + Cargo |

### 本地開發

```bash
# 安裝依賴
pnpm install

# 啟動桌面版開發模式
pnpm dev:tauri

# 啟動 Web 版開發模式（前端 + 後端分開）
pnpm dev:web
pnpm dev:backend

# 快速檢查（跳過 DuckDB 編譯以加快速度）
cargo check --no-default-features
```

### 相關連結

- [GitHub 倉庫](https://github.com/t8y2/dbx)
- [Releases 下載](https://github.com/t8y2/dbx/releases)
- [Issue 回報](https://github.com/t8y2/dbx/issues)
- [MCP Server 文件](https://github.com/t8y2/dbx/blob/main/packages/mcp-server/README.md)
- [CLI 文件](https://github.com/t8y2/dbx/blob/main/packages/cli/README.md)
- [離線驅動下載](https://dbxio.com/en/drivers)

---

> 最後更新：2026-06-24
>
> 本指南基於 DBX 截至 2026-06-24 的最新版本。DBX 活躍開發中，功能可能隨時更新，請以官方倉庫為準。
