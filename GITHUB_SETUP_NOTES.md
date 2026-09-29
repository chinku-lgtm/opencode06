# GitHub 操作流程與憑證紀錄（請勿填入真實 Token / 密碼明文在此檔）

> 專案：`opencode06`（`C:\opencode06`）
> GitHub 登入信箱：`chinku@go.edu.tw`
> GitHub 帳號：`chinku`
> 目標 repo（同名）：`https://github.com/chinku/opencode06`
> 建立日期：2026-09-29

## 1. 重要觀念：Google 帳號 vs GitHub 登入
- GitHub 登入頁沒有「用 Google 登入」按鈕。
- 你說的「已連結 Google 帳號」通常指以下其一：
  1. 瀏覽器已登入 Google（Gmail），GitHub 帳號的 Email 剛好是同一個 Gmail，方便收驗證碼 / 重設密碼。
  2. GitHub 帳號已開啟 2FA，備援信箱是 Gmail。
- 所以流程是：瀏覽器開著 Google 登入狀態 → 另開分頁去 `https://github.com/login` → 用 **GitHub 使用者名稱 + 密碼 + 2FA** 登入。

## 2. 本次已完成（本機）
- [x] `git init` + `git branch -M main`
- [x] `git add index.html`
- [ ] 設定身分（下次開新 session 前做一次即可，global 只需一次）：
  ```powershell
  git config --global user.name "你的GitHub使用者名稱"
  git config --global user.email "你的Gmail@gmail.com"
  git config --global init.defaultBranch main
  git config --global credential.helper manager
  ```
- [ ] 首次 commit（設定完身分後）：
  ```powershell
  cd C:\opencode06
  git commit -m "feat: airplane shooter game"
  ```

## 3. GitHub 網站操作（手動，約 3 分鐘）
1. 開 `https://github.com/login` 登入 GitHub。
2. 右上 `+` → `New repository`，或開 `https://github.com/new`。
3. `Repository name` 填 `opencode06`（與專案同名）。
4. Public / Private 任選（建議首次 Public，方便測試 Pages）。
5. **不要勾** Add README / .gitignore / license（本機已有檔案，避免衝突）。
6. 按 `Create repository`。
7. 建好後記下網址（填到下面表格）：
   - HTTPS：`https://github.com/帳號/opencode06.git`
   - SSH：`git@github.com:帳號/opencode06.git`

## 4. 需要的憑證（擇一，下次重用就靠它）
| 項目 | 填寫位置 | 說明 |
|---|---|---|
| GitHub 使用者名稱 | `此處只寫帳號，不寫密碼`：________ | `github.com/後面那段` |
| GitHub Email | ________@gmail.com | 跟 GitHub 帳號綁定的信箱 |
| 認證方式 | ☐ PAT ☐ SSH ☐ gh CLI | 三選一，Windows 推薦 PAT + Credential Manager |
| PAT 到期日 | ________ | Settings → Developer settings → Personal access tokens |
| PAT 權限 | `repo` 全勾 | 推送 private repo 必需；public 也建議勾 |
| SSH key 位置 | `C:\Users\User\.ssh\id_ed25519` | 若選 SSH 才需要 |

> 安全規則：Token / 密碼只貼在 GitHub 網站和 Windows 認證彈窗，不要貼到聊天紀錄、不要 commit 進 repo。

### 4a. 推薦：PAT + Windows 認證管理員（最適合跨專案 / 新 session）
1. GitHub → 右上頭像 → `Settings` → `Developer settings` → `Personal access tokens` → `Tokens (classic)` → `Generate new token (classic)`。
2. Note 填 `opencode06-win`，Expiration 選 `90 days`，勾 `repo`。
3. **只顯示一次**，立刻複製。
4. 本機推送時第一次會跳 Windows 登入框：
   - 使用者名稱 = GitHub 帳號
   - 密碼 = 貼上 PAT（不是 GitHub 密碼）
5. 之後憑證存在 `控制台 → 認證管理員 → Windows 認證 → git:https://github.com`，換專案 / 重開 session 自動沿用，不用重輸。

推送指令（HTTPS）：
```powershell
cd C:\opencode06
git remote add origin https://github.com/帳號/opencode06.git
git push -u origin main
```

### 4b. 備選：SSH（適合長期多專案，不用記到期日）
```powershell
ssh-keygen -t ed25519 -C "你的Gmail@gmail.com"
cat ~/.ssh/id_ed25519.pub
# 貼到 GitHub → Settings → SSH and GPG keys → New SSH key
ssh -T git@github.com
git remote add origin git@github.com:帳號/opencode06.git
git push -u origin main
```

### 4c. 備選：GitHub CLI（需先安裝 `gh`）
```powershell
winget install --id GitHub.cli
gh auth login   # 選 GitHub.com → HTTPS → Login with a web browser（會用已登入的 Google/瀏覽器開授權頁）
gh repo create opencode06 --public --source=. --push
```

## 5. 下一次操作（跨專案 / 同專案新工作階段）速查
- 同專案新 session：只要 `git status` 看得到 `origin`，且認證管理員還有 `git:https://github.com`，直接 `git pull` / `git push`，不用重建 repo。
- 跨專案（新資料夾如 `C:\newproj`）：
  ```powershell
  cd C:\newproj
  git init; git branch -M main
  git add .; git commit -m "init"
  # GitHub 網站再建一個同名 repo，然後：
  git remote add origin https://github.com/帳號/newproj.git
  git push -u origin main
  # 憑證同一組 PAT 直接沿用，不用重新產生（除非過期）
  ```
- PAT 過期症狀：`push` 出現 `403 / Authentication failed` → 重產生一顆 → Windows 認證管理員刪掉舊的 `git:https://github.com` → 再 push 一次輸入新的。

## 6. 本次待你回填（只寫非敏感資訊）
- GitHub 帳號：________
- Repo 網址：________
- 認證方式：________
- PAT 到期日：________
- 推送成功時間：________
