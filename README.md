# 全班合作 AI 糕點食譜大全 GitHub Pages 簡化版

這是一個純靜態網站：只需 GitHub Pages，沒有 Cloudflare、密碼後台、API Token、Secrets 或 npm 安裝步驟。支援手機相機與照片上傳、低信心提示、三欄食譜、小組交件工具、各組食譜合併，以及教師更換全班模型。

## 第一次部署 只做四步

1. 在 GitHub 建立公開儲存庫，例如 `pastry-classroom`。
2. 解壓縮套件，把此資料夾內的檔案上傳到儲存庫根目錄。根目錄必須直接看得到 `index.html`、`config.json`、`recipes.csv`，不要只上傳 ZIP，也不要多包一層資料夾。
3. 到 **Settings → Pages → Source: Deploy from a branch → main → /(root) → Save**。
4. 等待 Pages 發布完成，用設定頁顯示的 HTTPS 網址開啟。學生只需網址，不需 GitHub 帳號。

老師需有儲存庫編輯權限，才能正式更新網站。網站內的教師設定是本機試用工具，沒有假裝提供能保護更新權限的網頁密碼。

## 全班合作流程

### 各組負責一種新糕點

- 老師先分配不同糕點，名稱不要重複。
- 每組約30張訓練照片，另保留3–5張測試照片；記錄自拍或授權來源。
- 開網站上方「小組交件」，輸入名稱、材料、步驟，下載本組CSV與交件說明。
- 交件資料夾命名「03_司康」，包含訓練照片、測試照片、食譜CSV與來源說明，交到老師指定的位置。網站不會自動收件或上傳照片。

### 老師統整為一個全班模型

1. 開啟可編輯的 Teachable Machine 原始專案，保留原三類訓練資料。
2. 每組新增一個同名類別，分別批次上傳原始訓練照片。
3. 一次重新訓練全部類別，以各組保留照片測試後，匯出並上傳 TensorFlow.js 模型。
4. 取得一個包含全班全部類別的新模型連結。

**不同小組的模型網址不會自動合併。要交原始照片，老師才能把資料放進同一個模型。只有舊模型網址無法還原原始訓練照片，請保留原始專案。**

### 老師合併食譜並公布

1. 展開首頁的「教師設定與全班統整」。
2. 勾選保留目前食譜，再選擇各組CSV；網站會檢查缺欄與重複名稱，成功後下載 `recipes.csv`。
3. 貼入全班新模型網址，食譜來源填 `recipes.csv`。
4. 按「檢查並在本機試用」。網站會檢查每個模型類別都有同名食譜，並實際載入模型。
5. 通過後下載 `config.json`。
6. 將 **`config.json` 和 `recipes.csv` 一起上傳到 GitHub 儲存庫根目錄**，覆蓋同名檔案並 Commit changes。等 Pages 完成發布。
7. 全班重新整理網站，確認顯示「全班公布版本」，再跨組測試。

只按網頁的「本機試用」，不會更新別人的裝置。全班更新只靠 GitHub 上的公布檔案，不需每台手機手動貼連結。

## Google 試算表仍可使用

食譜格式固定：**辨識名稱、材料、步驟**。每種糕點一列，材料及步驟在同一格內換行。老師可將各組資料合併在同一份 Google 試算表，或將合併CSV匯入Google試算表。

在教師設定的食譜來源貼上已開放讀取的 Google 食譜連結，檢查後下載config.json並上傳GitHub即可。之後只編修同一份Google食譜，學生按「重新讀取食譜」即可；Google更新可能有延遲。

如果希望網站與食譜都只放在GitHub，保留預設 `recipes.csv` 即可。這也是本套件的預設方式。

## 已包含的檔案

- `index.html`、`app.js`、`style.css`：手機辨識與教師統整工具。
- `config.json`：全班共用的模型連結、食譜來源與信心值門檻。
- `recipes.csv`：蛋塔、瑪德蓮、布朗尼三筆基礎食譜。
- `group.html`、`group.js`：小組食譜填寫與CSV下載。
- `recipe-utils.js`：食譜解析、合併、名稱對應檢查與下載功能。
- `teacher-guide.html`：新版兩小時合作教案、交件規格與評量表，可列印。
- `materials/pastry-recipes.xlsx`：可匯入Google的原食譜範本。
- `vendor/`：Excel讀取程式與授權。
- `.nojekyll`：GitHub Pages 靜態檔案設定。

原Canva簡報可作基礎模型操作參考，新的全班合作流程以本版教案為準。

## 更新與還原

只有模型換網址時：教師測試新連結並下載config.json，上傳GitHub。

使用GitHub食譜時：修改或合併recipes.csv後上傳GitHub。兩者同時改時一起上傳。

需要還原時：在GitHub檔案的History找到舊config.json與recipes.csv，恢復後重新提交。使用Google來源時，GitHub只保留連結，不會備份Google原食譜內容。

## 注意與驗證

首次開相機需HTTPS及瀏覽器允許。相機不能用時，先以系統相機拍照，再選上傳。模型和程式需要網路；不是離線App。

80%是本課操作門檻，低信心時提示可能為新糕點，仍應調整光線或角度重拍。未知物件也可能被高信心誤判，信心值不等於準確率。

已檢查三筆基礎食譜、CSV換行與合併、缺欄及重複名稱攔截、模型與食譜名稱對應、專案子路徑，以及實際模型載入。您自己的GitHub網址仍需完成上述Pages發布步驟；本套件不會自動替您建立GitHub帳號或儲存庫。

官方說明：https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
