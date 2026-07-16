# 🌺 沖繩之旅 · 旅行日誌 App

一個為 20 天沖繩家庭旅行打造的簡單 PWA（網頁 app）：

- 🐾 **旅行軌跡** — 一天一條時間軸，走到哪記到哪，每張卡片可帶時間、文字、Google Maps 地點與照片
- 🗺️ **軌跡地圖** — 有座標的站會自動畫在當日小地圖上、連成路線（GPS 打卡或貼含座標的地圖連結）
- 📝 **今日總結** — 睡前補兩句總結，自動儲存
- 📷 **照片** — 手機直接拍照或選圖，自動壓縮上傳，可掛在軌跡卡片上
- 💴 **花費記帳** — 日圓/台幣、分類統計、每日與總覽報表
- 👫 **兩人共用** — 你和太太的手機透過這個 private repo 同步同一份資料
- ✈️ **離線可用** — 沒網路照樣記錄，恢復連線自動同步

架構是「app 與資料分家」：

| Repo | 公開/私有 | 內容 |
|---|---|---|
| `Travel-to-Okinawa`（本 repo） | **Public** | 只有 app 程式碼（不含任何個資），用 GitHub Pages 出網址 |
| `okinawa-data` | **Private** | 你們的旅行資料：`days/*.json`、`photos/*.jpg`，只有持 token 的人能存取 |

app 內建防呆：如果偵測到資料 repo 是公開的，會拒絕同步並跳出警告。

---

## 出發前的 3 個設定步驟（約 8 分鐘）

### 步驟 1：建立 private 資料倉庫（1 分鐘）

1. 到 <https://github.com/new>
2. Repository name 填 `okinawa-data`（app 預設就是這個名字，照填最省事）
3. 選 **Private**，勾 **Add a README file** → Create repository

### 步驟 2：建立 GitHub Token（2 分鐘）

1. 開啟 <https://github.com/settings/personal-access-tokens/new>
2. Token name 隨意填（例如 `okinawa-app`），**Expiration 選 90 days**
3. Repository access 選 **Only select repositories** → 勾選 `okinawa-data`
4. Permissions → Repository permissions → **Contents** 設為 **Read and write**
5. 按 Generate token，**把 `github_pat_…` 複製起來**

> 這組 token 只能讀寫 `okinawa-data` 這一個 repo，兩支手機共用同一組。

### 步驟 3：把本 repo 改成 Public 並開啟 Pages（3 分鐘）

1. 本 repo → **Settings** → General 最下方 **Danger Zone** → Change visibility → **Make public**
2. 本 repo → **Settings → Pages** → Source 選 `Deploy from a branch`，Branch 選 `claude/okinawa-trip-app-g82tpp` / `(root)` → Save
3. 等 1–2 分鐘，app 網址就是：**`https://justdanielooo.github.io/Travel-to-Okinawa/`**

> 改 public 前請確認：本 repo 裡只有 app 程式碼、沒有任何 `days/` 或 `photos/` 資料夾（資料都存在 private 的 `okinawa-data`）。

### 步驟 4：你的手機設定（2 分鐘）

1. 手機瀏覽器開啟上面的網址
2. 打開 app → 右下角 **設定**：
   - 填「你的名字」（記帳會顯示付款人）
   - 貼上步驟 1 的 **GitHub Token** → 按 **儲存並測試連線**
3. 看到「連線成功」就完成了
4. （選配）iPhone：Safari 分享按鈕 → **加入主畫面**；Android：Chrome 選單 → **加到主畫面**，用起來更像 app

### 步驟 5：太太這邊——什麼都不用裝（30 秒）

1. 你在 app 的「設定」頁按 **💌 產生給另一半的一鍵設定連結**，用 LINE 私訊傳給她
2. 她**點開連結就自動完成所有設定**，直接開始寫日記、拍照、記帳——不用安裝、不用輸入 token
3. 建議她點開後選「用 Safari／Chrome 開啟」（不要停留在 LINE 內建瀏覽器），之後從瀏覽器書籤或同一個連結都能再進來；想要的話同樣可以「加入主畫面」，但不是必須

> 注意：這個連結內含 token，只能用私人訊息傳給家人，不要貼到公開的地方。

---

## 開放家人瀏覽＋留言（選配，約 7 分鐘）

家人點連結後：只能看日記、軌跡、相簿，可以留言；看不到花費與總覽，也改不了任何內容（GitHub 權限在伺服器端強制）。

1. **建留言倉庫**：到 <https://github.com/new> 建 `okinawa-comments`，選 **Private**，勾 Add a README
2. **建兩組 token**（同樣在 [fine-grained token 頁](https://github.com/settings/personal-access-tokens/new)）：
   - 「資料唯讀」token：只勾 `okinawa-data`，Contents 設 **Read-only**
   - 「留言」token：只勾 `okinawa-comments`，Contents 設 **Read and write**
3. **回到 app**：設定 → 「開放家人瀏覽＋留言」→ 貼上兩組 token → 儲存 → 按 **💌 產生家人瀏覽連結**，傳到家族群組
4. 你和太太的手機各按一次「儲存」（或重新點一次彼此的一鍵設定連結）後，「今日」頁底部就會出現家人的留言，每分鐘自動更新

> 安全性：家人連結內含唯讀鑰匙＋留言鑰匙。最壞情況（連結外流）也只是別人能看到日記與亂留言，動不了你們的資料；隨時可到 GitHub 撤銷這兩組 token。

## 日常使用

- **記錄**：打開 app 就是今天的頁面，直接寫日記、按＋加照片、按「記一筆」記帳
- **同步**：存檔後幾秒自動同步；切回 app、恢復網路時也會自動同步；也可到設定按「立即同步」
- **標題旁的小圓點**：綠＝已同步、黃＝同步中、紅＝離線或失敗（會自動重試）
- **匯率**：預設 1 円 = 0.205 台幣，可在設定調整，報表即時換算

## 資料放在哪？

| 內容 | 位置 |
|---|---|
| 日記＋花費＋照片清單 | private repo `okinawa-data` 的 `days/2026-07-16.json` …（每天一個檔） |
| 照片檔（已壓縮） | private repo `okinawa-data` 的 `photos/*.jpg` |
| 手機本地快取 | 每支手機的瀏覽器儲存空間（離線用） |

旅行結束後，`okinawa-data` 就是完整的旅行紀錄備份，永久保存。

## 小提醒

- 同一天的**日記**若兩人同時離線各自編輯，同步時保留較晚儲存的那份；**花費和照片**永遠自動合併、不會弄丟。
- 照片會壓縮到約 200–400KB 再上傳，省流量也夠清晰；原圖記得照常留在手機相簿。
- Token 有效期 90 天，涵蓋整趟旅程；旅程結束後可到 GitHub 設定頁把它撤銷。
