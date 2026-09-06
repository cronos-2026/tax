# 創業節稅試算｜GitHub Pages 版

## 檔案
- `index.html`：公開前台，不提供後台入口。
- `admin.html`：獨立後台；開啟時只顯示帳號、密碼、登入按鈕，登入後才顯示完整管理內容。
- `tax-config.json`：前台目前正式使用的參數。
- `annual-presets.json`：113、114、115 年度預設參數。

## GitHub Pages
1. 將本資料夾檔案上傳到 Repository 根目錄。
2. Repository → Settings → Pages → Deploy from a branch → `main` / `/(root)`。
3. 前台：`https://<帳號>.github.io/<repo>/`
4. 後台：`https://<帳號>.github.io/<repo>/admin.html`

## 後台登入
目前帳號：`admin`
目前密碼：`password`

此登入屬 GitHub Pages 純前端存取門檻，不等同伺服器端安全驗證；請勿在頁面原始碼中存放 GitHub Token 或其他高敏感憑證。

## 年度參數
後台會依所選民國年度讀取 `annual-presets.json` 對應參數，目前內建 113、114、115 年。
財政部參考來源名稱與按鈕連結會隨所選年度切換，畫面不直接顯示完整網址。

## 前台計算項目啟用
後台可從既有免稅額／特別扣除額項目勾選「啟用」。
啟用後，前台自動新增對應欄位或自動計算項目，並納入綜合所得稅試算。

## 儲存參數
GitHub Pages 無法由瀏覽器直接覆寫 Repository。
後台修改後請下載新的 `tax-config.json`，再回 GitHub Repository 覆蓋同名檔案。

## 版本號
版本採 `vYYYY.MM`，例如 `v2026.09`。


## GitHub 後台同步版

本版本的 `admin.html` 可直接透過 GitHub Contents API 更新 Repository 內的 `tax-config.json`。

預設：
- Owner：`cronos-2026`
- Repository：`cronos-2026/tax`
- Branch：`main`
- 參數檔：`tax-config.json`

使用方式：
1. 進入 `admin.html`，以既有後台帳密登入。
2. 修改年度參數或啟用項目。
3. 在「GitHub 同步更新前台」貼上 GitHub Fine-grained personal access token。
4. Token 建議只授權此 Repository，並將 Repository permissions → Contents 設為 `Read and write`。
5. 按「同步更新前台」。
6. 系統會直接更新 GitHub 的 `tax-config.json`；GitHub Pages 部署完成後，前台重新整理即可讀取新參數。

安全說明：
- Token 不會寫入 `tax-config.json`。
- 本版不會把 Token 硬編碼在 `admin.html`。
- Token 僅存在目前開啟的瀏覽器頁面記憶體中；關閉或重新整理頁面後需重新輸入。
- 因為 GitHub Pages 是公開靜態網站，請不要把長期高權限 Token 寫進 HTML。


## GitHub 根網址專用

此版本已設定為 GitHub Pages 使用者根網站：

- 前台：https://cronos-2026.github.io/
- 後台：https://cronos-2026.github.io/admin.html
- GitHub Owner：cronos-2026
- Repository：tax
- Branch：main
- 前台參數檔：tax-config.json

### Token 權限
Fine-grained personal access token 必須把 Repository access 設為：
`Only select repositories → cronos-2026.github.io`

Repository permissions：
`Contents → Read and write`

若 Token 仍只授權舊的 `cronos-2026-tax-calculator`，
後台同步時會出現 `Resource not accessible by personal access token`。

### 使用方式
1. 將本 ZIP 內 5 個檔案上傳到 `cronos-2026/tax` Repository 根目錄。
2. 開啟 `/admin.html` 登入。
3. 修改後台參數。
4. 貼入已授權 `cronos-2026/tax` 的 Fine-grained Token。
5. 按「同步更新前台」。
6. 系統會直接更新 GitHub 的 `tax-config.json`。
7. GitHub Pages 部署完成後，重新整理前台即可看到新設定。


## 本次優化（tax 專用同步版）

後台同步目標已固定：
- Owner：`cronos-2026`
- Repository：`tax`
- Branch：`main`
- 檔案：`tax-config.json`

後台新增：
- 「測試 GitHub Token」按鈕：先確認 Token 是否可讀取目標檔案。
- 「同步更新前台」按鈕：確認後直接寫入 `tax-config.json`。
- GitHub Owner / Repository / Branch / 檔案路徑改為唯讀，避免誤改。
- 常見 Token 錯誤會轉成中文提示。

Token 必須使用 Fine-grained personal access token：
`Only select repositories → cronos-2026/tax`
Repository permissions：
`Contents → Read and write`


# TAX FINAL 2026.09 — 實際 GitHub Pages 部署設定

本完整版本已固定為目前實際網站：

- GitHub Repository：`cronos-2026/tax`
- Branch：`main`
- 前台：`https://cronos-2026.github.io/tax/`
- 後台：`https://cronos-2026.github.io/tax/admin.html`
- 後台同步檔案：`tax-config.json`

後台同步欄位已固定：
- Owner：`cronos-2026`
- Repository：`tax`
- Branch：`main`
- 路徑：`tax-config.json`

Fine-grained Token：
- Repository access：Only select repositories → `cronos-2026/tax`
- Repository permissions：Contents → Read and write

後台提供「測試 GitHub Token」與「同步更新前台」。


## 前台「歸零」按鈕
- 「↺ 歸零」：只將目前畫面的輸入數字與試算結果歸零，不刪除任何已儲存資料。
- 「🗑️ 清除儲存資料」：刪除全部已儲存資料，並將目前輸入值歸零。


## 扶養人數驗證
前台已新增以下限制，扶養人數必須大於或等於各欄填寫人數：
- 70歲以上免稅額
- 身心障礙特別扣除額
- 幼兒學前－第1名子女
- 長期照顧特別扣除額

若不符合，按「立即計算比較」時會停止計算並提示；欄位的最大值也會依扶養人數動態調整。


## 扶養親屬資格可同時勾選
前台已改為逐位扶養親屬勾選：
- 70歲以上
- 身心障礙
- 長期照顧

三個資格彼此獨立，同一位扶養親屬可以同時勾選 2 項或 3 項，不是互斥選項。
系統會分別計入高齡免稅額、身心障礙特別扣除額與長期照顧特別扣除額。


## 扶養資格簡化優化
前台改為最基本、易操作的試算方式：
- 70歲以上受扶養親屬人數 ≤ 扶養人數
- 身心障礙特別扣除資格人數 ≤ 扶養人數
- 幼兒學前－第1名符合資格子女人數 ≤ 扶養人數
- 長期照顧特別扣除資格人數 ≤ 扶養人數
- 各資格分別檢查，不互斥，也不將不同資格人數相加後再比較扶養人數。
- 同一受扶養親屬可能同時符合多種資格，因此不同資格人數可重疊。


## 扶養資格欄位上限鎖定
- 70歲以上、身心障礙、幼兒學前第1名、長期照顧等資格人數，各自不得超過扶養人數。
- 當資格人數已達目前允許上限時，該欄位會進入鎖定狀態，不能再增加。
- 若要增加該資格人數，必須先把「扶養人數」提高。
- 若扶養人數降低，超過新上限的資格人數會自動降到新上限。
- 不同資格仍彼此獨立、不互斥，也不相加比較。
