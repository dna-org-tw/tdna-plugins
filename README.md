# TDNA Plugins

台灣數位遊牧者協會的 plugin 分發套件。提供協會資料查詢、工作管理及報帳與內容草稿功能，連接 TDNA 營運後台的 OAuth MCP。

## 安裝

在 Codex 的 Plugins 開啟 **Add plugin marketplace**：

|欄位|填入內容|
|---|---|
|Source|`dna-org-tw/tdna-plugins`|
|Git ref|`main`|
|Sparse paths|留空|

新增後選擇 **TDNA** 來源，找到 **TDNA** 並安裝。依提示使用自己的 Google 帳號登入、確認權限，然後在新對話使用。

CLI 可用 `codex plugin marketplace add dna-org-tw/tdna-plugins` 加入來源，再回桌面介面安裝。

## 帳號與權限

- 安裝 plugin 不等於取得協會資料存取權。
- 使用 `@dna.org.tw` 組織帳號，或由 TDNA 管理者邀請的外部 Google 帳號登入。
- 外部使用者請先請管理者到後台「MCP 管理 → 角色」建立邀請、用途與到期日。未受邀或已到期帳號無法登入。
- 僅能執行目前帳號角色允許的工具。對外發布與報帳遵守後台確認規則。
- 不必填 API Key、Client ID 或 Client Secret，不要在對話中貼密碼或金鑰。

## 確認連線

新對話輸入：「使用 TDNA 呼叫 whoami，確認我的角色；再列出可用的協會資料查詢功能，不修改資料。」

確認有實際 tool call，且回應 `via` 為 `oauth`。也可查詢 ehrsnet 報帳進度，比對同一筆申請編號；沒有可見單據時清單可為空。

需要中斷連線時，登入 [TDNA 後台](https://admin.dna.org.tw/?page=mcp)，到「MCP 金鑰」撤銷該連線。撤銷後再次呼叫應要求重新授權。

## 其他 MCP 客戶端與 ChatGPT

支援 OAuth／動態註冊的 MCP 客戶端，也可直接新增 `https://admin.dna.org.tw/mcp`，Transport 選 Streamable HTTP。

此儲存庫提供 Git marketplace 與 bundled HTTP MCP，並非 OpenAI 公開目錄上架或 ChatGPT 工作區發布。若使用 ChatGPT 的已註冊 MCP 連線模式，須先在 Developer mode 建立連線，取得真實 `plugin_asdk_app…` 技術 ID，再用 `.app.json` 綁定；本套件未內嵌該 ID，也未聲稱已完成該模式的安裝。

## 維護

`plugins/tdna/.codex-plugin/plugin.json` 是 plugin manifest；`.mcp.json` 只包含服務網址，OAuth 憑證由客戶端管理。Skill 與品牌圖皆位於 plugin 內。

日常功能與修正在固定的遠端 MCP 網址 `https://admin.dna.org.tw/mcp` 部署，既有工具的伺服器端更新不需要使用者下載或重新安裝 plugin。維持網址與既有工具介面相容；新增工具可能需要重新連線或開新對話，依客戶端重新取得工具清單的時機而定。

名稱、圖示、內附 Skill 或連線設定屬於本機套件，更新這些內容時提高 plugin version。Git ref 使用 `main`；這代表來源追蹤分支，不保證客戶端會自動更新已安裝套件。目前官方文件未載明發布者可強制啟用套件自動更新的設定，因此不承諾所有客戶端都會自動取得這類變更。

發布前確認未包含憑證、後台程式、個人資料或測試單據。

套件結構依 [OpenAI plugin 文件](https://developers.openai.com/plugins/build/plugins)。
