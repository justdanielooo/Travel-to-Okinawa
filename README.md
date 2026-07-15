# 🌺 沖繩之旅 · 旅行日誌 App

一個為 20 天沖繩家庭旅行打造的簡單 PWA（網頁 app）：

- 📓 **每日日記** — 每天一頁，自動儲存
- 📷 **照片** — 手機直接拍照或選圖，自動壓縮上傳
- 💴 **花費記帳** — 日圓/台幣、分類統計、每日與總覽報表
- 👫 **兩人共用** — 你和太太的手機透過這個 private repo 同步同一份資料
- ✈️ **離線可用** — 沒網路照樣記錄，恢復連線自動同步

App 本體是純靜態網頁（`index.html`），不含任何個人資料；所有旅行資料（`days/`、`photos/`）由 app 透過 GitHub API 存回這個 **private repo**，只有你們自己看得到。

---

## 出發前的 3 個設定步驟（約 10 分鐘）

### 步驟 1：建立 GitHub Token（在電腦上做，2 分鐘）

1. 開啟 <https://github.com/settings/personal-access-tokens/new>
2. Token name 隨意填（例如 `okinawa-app`），**Expiration 選 90 days**
3. Repository access 選 **Only select repositories** → 勾選 `Travel-to-Okinawa`
4. Permissions → Repository permissions → **Contents** 設為 **Read and write**
5. 按 Generate token，**把 `github_pat_…` 複製起來**（傳給自己和太太，例如用 LINE 的 Keep）

> 這組 token 只能讀寫這一個 repo，兩支手機都貼同一組即可。

### 步驟 2：把 app 放上網（擇一，5 分鐘）

App 需要一個 https 網址才能加到手機主畫面。因為 app 檔案不含任何個資，放在公開空間是安全的。

**方式 A — GitHub Pages（建議）**

GitHub 免費方案的 Pages 只支援 public repo，所以另開一個小的公開 repo 放 app 檔案：

1. 到 <https://github.com/new> 建立新 repo，名稱例如 `okinawa-app`，選 **Public**，勾 Add a README
2. 進入新 repo → **Add file → Upload files**，把本 repo 這 6 個檔案拖進去上傳：
   `index.html`、`sw.js`、`manifest.json`、`icon-180.png`、`icon-192.png`、`icon-512.png`
3. 新 repo 的 **Settings → Pages** → Source 選 `Deploy from a branch`，Branch 選 `main` / `(root)` → Save
4. 等 1–2 分鐘，網址就是 `https://<你的帳號>.github.io/okinawa-app/`

> 旅行資料**不會**出現在這個公開 repo，資料只存在 private 的 `Travel-to-Okinawa`。

**方式 B — 如果你的 GitHub 是付費方案（Pro）**

直接在本 repo：Settings → Pages → Source 選 `Deploy from a branch`，Branch 選 app 所在分支 → Save。

### 步驟 3：你的手機設定（2 分鐘）

1. 手機瀏覽器開啟上面的網址
2. 打開 app → 右下角 **設定**：
   - 填「你的名字」（記帳會顯示付款人）
   - 貼上步驟 1 的 **GitHub Token** → 按 **儲存並測試連線**
3. 看到「連線成功」就完成了
4. （選配）iPhone：Safari 分享按鈕 → **加入主畫面**；Android：Chrome 選單 → **加到主畫面**，用起來更像 app

### 步驟 4：太太這邊——什麼都不用裝（30 秒）

1. 你在 app 的「設定」頁按 **💌 產生給另一半的一鍵設定連結**，用 LINE 私訊傳給她
2. 她**點開連結就自動完成所有設定**，直接開始寫日記、拍照、記帳——不用安裝、不用輸入 token
3. 建議她點開後選「用 Safari／Chrome 開啟」（不要停留在 LINE 內建瀏覽器），之後從瀏覽器書籤或同一個連結都能再進來；想要的話同樣可以「加入主畫面」，但不是必須

> 注意：這個連結內含 token，只能用私人訊息傳給家人，不要貼到公開的地方。

---

## 日常使用

- **記錄**：打開 app 就是今天的頁面，直接寫日記、按＋加照片、按「記一筆」記帳
- **同步**：存檔後幾秒自動同步；切回 app、恢復網路時也會自動同步；也可到設定按「立即同步」
- **標題旁的小圓點**：綠＝已同步、黃＝同步中、紅＝離線或失敗（會自動重試）
- **匯率**：預設 1 円 = 0.205 台幣，可在設定調整，報表即時換算

## 資料放在哪？

| 內容 | 位置 |
|---|---|
| 日記＋花費＋照片清單 | 本 repo `days/2026-07-16.json` …（每天一個檔） |
| 照片檔（已壓縮） | 本 repo `photos/*.jpg` |
| 手機本地快取 | 每支手機的瀏覽器儲存空間（離線用） |

旅行結束後，這個 repo 就是完整的旅行紀錄備份，永久保存。

## 小提醒

- 同一天的**日記**若兩人同時離線各自編輯，同步時保留較晚儲存的那份；**花費和照片**永遠自動合併、不會弄丟。
- 照片會壓縮到約 200–400KB 再上傳，省流量也夠清晰；原圖記得照常留在手機相簿。
- Token 有效期 90 天，涵蓋整趟旅程；旅程結束後可到 GitHub 設定頁把它撤銷。
