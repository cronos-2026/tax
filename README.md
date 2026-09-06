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


## 列印 1～2 頁自動優化
A4直式列印，縮小邊界與留白，並依內容高度自動切換緊湊列印密度，目標盡量維持1～2頁。列印時隱藏操作按鈕，重要區塊盡量避免跨頁；列印後恢復正常畫面。


## 後台「前台計算項目啟用設定」全選功能
- 新增「全選」按鈕：一次勾選此區所有可啟用項目。
- 新增「取消全選」按鈕：一次取消此區所有可啟用項目。
- 不影響鎖定或不可編輯的核心項目。


## 版本
目前版本：`2026.09.v06-11`。前台與後台網頁皆顯示版本號；後續更新依 `YYYY.MM.vDD`，同日多版再加 `-1`、`-2`。


## 2026.09.v06-11 版面調整
- 移除前台上方／固定位置的版本膠囊。
- 前台頁尾原「© 2026 . GitHub Pages 網頁版」改為「© 2026.09.v06-11」。
- 版本號不再鎖定顯示於畫面上方，改放在網頁最下方頁尾。


## 2026.09.v06-11
修正前台：完整移除頁面上方固定的 `v2026.09` 綠色版本標籤，版本僅保留於最下方 footer：`© 2026.09.v06-11`。


## 2026.09.v06-11 簡潔視覺優化
- 前台版面改為更簡潔的卡片與留白配置。
- 統一背景、邊框、輸入框與標題視覺層級。
- 需注意事項使用暖黃色警示區塊加強辨識。
- 重要錯誤/高風險訊息保留紅色語意；一般正常狀態採綠色語意。
- 降低陰影與過多裝飾，提升專業感與可讀性。


## 2026.09.v06-11
- 「清除儲存資料」只刪除瀏覽器中已儲存的多組資料。
- 不再歸零目前畫面的輸入值，也不清除目前試算結果。
- 「↺ 歸零」維持獨立功能，專門負責將目前畫面數值歸零。


## 2026.09.v06-11
- 修正扶養資格提醒區塊中 `<strong>` 被當成文字顯示的問題。
- 「注意：」現在會正常粗體顯示，不再露出 HTML 標籤。
- 保留原本暖黃色提醒樣式，並加強「注意：」的視覺層級。


## 2026.09.v06-11 列印分頁修正
- 修正列印時第 1 頁只有標題與提醒、主要試算內容被整塊推到下一頁的問題。
- 原因為大型卡片套用了 `page-break-inside: avoid`。
- 現改為大型卡片與表格可自然跨頁，只保護表格列、標題等小單位不被切斷。
- 保留 A4 自動壓縮與 1～2 頁列印目標。


## 2026.09.v06-11 列印 1～2 頁強化
- 列印主內容固定改為「左側輸入／右側試算結果」雙欄報表版面。
- A4 直式邊界縮至 5～6 mm，並壓縮卡片、輸入欄位、表格列高與間距。
- 列印時隱藏操作按鈕與部分非必要輔助文字，只保留核心輸入、結果與重要提醒。
- 完整取消大型卡片不可跨頁的規則，避免再次產生大面積空白頁。
- 不再依螢幕頁面高度強制套用極小 zoom；改由專用列印排版直接控制在 1～2 頁。


## 2026.09.v06-11 智慧列印分頁
- 列印時優先嘗試將「基礎資料設定」與「稅額試算比較表」排在同一頁。
- 若內容量較多、不適合維持一頁，則自動切換兩頁模式。
- 兩頁模式以兩個主要抬頭作為分頁基準：
  1. 第 1 頁：基礎資料設定
  2. 第 2 頁：稅額試算比較表
- 第 2 頁會從「稅額試算比較表」標題開始，避免內容被切得零散。


## 2026.09.v06-11
- 修正「清除儲存資料」確認文字。
- 改為：「確定要刪除全部已儲存資料嗎？目前畫面的輸入數字及試算結果會保留。」
- 清除儲存資料只刪除已儲存內容，不歸零目前畫面。


## 2026.09.v06-11 按鈕排版
- 第一列：儲存目前資料／開啟儲存資料
- 第二列：歸零／清除儲存資料
- 第三列：列印本頁


## 2026.09.v06-11 版本編碼優化
- 版本格式統一為：`年.月.v日-次數`
- 本版版本號：`2026.09.v06-11`
- 年份前不再加 `v`
- 前台、後台、頁尾、README 與 ZIP 檔名同步使用相同格式


## 2026.09.v06-12 列印空白頁修正
- 修正列印最後多出一頁、只剩「以115年度稅率、免稅額及扣除額基礎計算」的問題。
- 該螢幕版底部說明在列印時隱藏，不再單獨形成尾頁。
- 移除列印時可能造成額外頁面的最小高度與尾端強制分頁。
- 保留原本一頁優先、必要時依「基礎資料設定／稅額試算比較表」分成兩頁的規則。
