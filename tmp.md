# 開発環境セットアップ（WSL + npm 版）

> **対象**: Windows 10 / 11 ／ Webアプリ開発（Next.js / Node.js）
>
> **ゴール**: ① WSL（Ubuntu）で Node.js + npm が使える ② Cursor から WSL 上のプロジェクトを編集・起動できる ③ GitHub / Cloudflare に登録できる ④ 新規/既存アプリを `npm run dev` で動かせる

---

## 0. 全体像（やること）

1. Windows に **WSL（Ubuntu）** を入れる
2. Ubuntu を初期設定（アップデート・基本ツール）
3. **Node.js と npm** を入れる（Voltaは使わず、WSL内で nvm→npm を利用）
4. **Cursor**（VS Code系エディタ）を Windows に入れて、WSL とつなぐ
5. GitHub / Cloudflare に登録（リンクあり）
6. 新規 or 既存のプロジェクトを起動

> **用語メモ**
>
> * **WSL**: Windows 上で Linux（今回は Ubuntu）を動かす仕組み。開発が安定・高速になります。
> * **Ubuntu**: Linux の一種。WSL の中で動く“黒い画面”のOSです。
> * **npm**: Node.js 用のパッケージ管理コマンド。今回は **npm** を使います（Voltaは使いません）。

---

## 1. 事前準備（Windows）

* Windows を最新まで **Windows Update**。
* **Microsoft Store** にサインイン。
* この後は、**PowerShell（管理者）** を使います（スタートメニューで「PowerShell」を検索 → 右クリック → *管理者として実行*）。

---

## 2. WSL（Ubuntu）をインストール

### 2-1. もっとも簡単な入れ方（Windows 11 / 10 共通）

1. **PowerShell（管理者）** で次を実行：

   ```powershell
   wsl --install -d Ubuntu
   ```
2. 指示に従って **再起動**。
3. 再起動後、自動で **Ubuntu** の初回セットアップが始まります。ユーザー名・パスワードを入力して完了。

> もし「該当する機能が無効」系のエラーが出たら：
>
> * 次の2つを有効化して再起動してください。
>
>   ```powershell
>   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
>   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
>   ```
> * その後、WSL の既定を **Version 2** に設定：
>
>   ```powershell
>   wsl --set-default-version 2
>   ```
> * 改めて `wsl --install -d Ubuntu` を実行。

### 2-2. インストール確認

PowerShell で次を実行して、**VERSION が 2** になっていればOKです。

```powershell
wsl -l -v
```

`Ubuntu` が表示されなければインストールからやり直し、`VERSION` が 1 の場合は：

```powershell
wsl --set-version Ubuntu 2
```

---

## 3. Ubuntu（WSL）の初期設定

1. スタートメニューから **Ubuntu** を起動（黒い端末が開きます）。
2. 下記を順に実行（パスワード入力を求められます）。

   ```bash
   sudo apt update
   sudo apt -y upgrade
   sudo apt -y install build-essential git curl lsb-release ca-certificates
   ```
3. **作業フォルダ** を WSL 内に作成（※Windows側の `C:` 直下ではなく、WSL 内に置くと高速です）。

   ```bash
   mkdir -p ~/workspace
   cd ~/workspace
   ```

   > **注意**: `C:` ドライブ配下（例: `/mnt/c/Users/...`）で開発すると速度が落ちます。**WSL内（`~` や `/home/ユーザー名`）** にプロジェクトを置きましょう。

---

## 4. Node.js と npm を入れる（Voltaなし／nvm利用）

> npm を使うために、まず Node.js を入れます。WSL では **nvm（Node Version Manager）** を使うのが簡単＆安全です。

1. **nvm のインストール**

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
   # 新しい設定を読み込み
   source ~/.bashrc
   ```
2. **Node.js（LTS）をインストール**

   ```bash
   nvm install --lts
   nvm use --lts
   nvm alias default 'lts/*'
   ```

   > プロジェクトで **Node 22** 固定が必要な場合は：
   >
   > ```bash
   > nvm install 22
   > nvm use 22
   > nvm alias default 22
   > ```
3. **バージョン確認**（数字が表示されればOK）

   ```bash
   node -v   # 例: v22.x または LTS のバージョン
   npm -v    # 例: 10.x 以上
   ```

---

## 5. Cursor（エディタ）を Windows にインストール＆WSL と接続

1. Windows に **Cursor** をインストール（公式手順に従って通常インストール）。
2. Cursor を起動 → 左下の「**><**」アイコン（リモート）から **WSL: Ubuntu** を選択 → *Open Folder* で `~/workspace` を開く。
3. 拡張機能で **Remote - WSL**（VS Code 互換の拡張）を有効化しておくとスムーズです。

> **もし Cursor で WSL リモートがうまく出ない場合**：
>
> * いったん **VS Code + Remote - WSL** で同じ手順を試してもOKです（Cursor と VS Code はほぼ操作感が同じです）。
> * 端末から `~/workspace` を開くには：
>
>   ```bash
>   explorer.exe .   # 現在のWSLフォルダをエクスプローラーで開く
>   ```

---

## 6. アカウント登録（GitHub / Cloudflare）

* **GitHub** 登録手順は → **[ここ](https://github.com/jamsjplan/windows-setup/blob/main/GitHub.md)**
* **Cloudflare** 登録手順は（準備中 / 後日追記 or 社内ガイドに沿ってください）

> 既存の社内/個人ドキュメントがある場合は、そちらの手順に従って構いません。

---

## 7. 新しくプロジェクトを作る（Next.js）

以降は **Ubuntu（WSL）** の端末で作業します。

```bash
cd ~/workspace
# 対話形式でプロジェクトを作成（推奨）
npx create-next-app@latest
# もしくはアプリ名を指定
# npx create-next-app@latest my-app

cd my-app
npm run dev
```

ブラウザで **[http://localhost:3000](http://localhost:3000)** にアクセス → 初期ページが表示されれば成功です。

> **補足**: `npm create next-app@latest` でも同じです（内部で `npx` を使います）。

---

## 8. 既存のアプリを実行する

### 8-1. ソースコードの取得（HTTPS推奨）

```bash
cd ~/workspace
# 例: HTTPS でクローン（GitHubの画面「Code」→ HTTPS のURLをコピー）
git clone https://github.com/ユーザー名/リポジトリ名.git
cd リポジトリ名
```

> SSH でのクローンも可能ですが、初学者はまず **HTTPS** が簡単です。

### 8-2. 依存関係のインストールと起動

```bash
# lockファイルがある場合は npm ci（速くて確実）
# なければ npm install
if [ -f package-lock.json ]; then npm ci; else npm install; fi

# 開発サーバー起動
npm run dev
```

---

## 9. よく使う基本コマンド（Ubuntu）

```bash
pwd          # 今いる場所
ls           # ファイル一覧
cd フォルダ  # 移動
cd ..        # 1つ上へ
mkdir name   # フォルダ作成
rm -rf name  # フォルダ削除（慎重に）
```

---

## 10. トラブルシューティング（困ったらここ）

### 10-1. `wsl --install` でエラーが出る

* 「機能が無効」→ 2章の DISM コマンドで **Linux 用 Windows サブシステム** と **仮想マシンプラットフォーム** を有効にし、再起動。
* VERSION が 1 → `wsl --set-version Ubuntu 2` を実行。

### 10-2. Ubuntu が起動しない／設定やり直したい

* PowerShell（管理者）で `wsl -l -v` で状態確認。必要に応じて `wsl --shutdown` で停止、再起動してやり直し。

### 10-3. `node` / `npm` が見つからない

* 端末を開き直す or `source ~/.bashrc` 実行。
* `nvm install --lts` → `nvm use --lts` を再実行。

### 10-4. `next: command not found` / 「'next' は内部コマンド…」系

* プロジェクト直下で **依存関係のインストール** を忘れていませんか？

  ```bash
  npm install   # または npm ci
  ```
* それでも動かない場合は、Next.js を明示インストール：

  ```bash
  npm install next@latest react@latest react-dom@latest
  ```

### 10-5. ポート 3000 がすでに使われている

```bash
# 使用中プロセスを探す（必要なら lsof を入れる）
sudo apt -y install lsof
lsof -i :3000
kill -9 <PID>
```

### 10-6. 画面が更新されない／ビルドが遅い

* **WSL内のフォルダ**（`~/workspace` 等）で作業しているか確認。
* Windows 側 (`/mnt/c`) での開発は遅くなりがちです。

### 10-7. Git の改行で警告が出る

```bash
git config --global core.autocrlf input
```

### 10-8. Cursor が WSL を認識しない

* Cursor の左下リモート切り替えで **WSL: Ubuntu** を選択。
* うまくいかなければ **VS Code + Remote - WSL** で開いてもOK（操作はほぼ同じ）。

---

## 11. 付録：コマンド早見表

**WSL 管理（PowerShell）**

```powershell
wsl -l -v                 # ディストリ一覧
wsl --set-default-version 2
wsl --set-version Ubuntu 2
wsl --shutdown            # 全WSL停止
```

**nvm / Node / npm（Ubuntu）**

```bash
nvm install --lts
nvm use --lts
nvm alias default 'lts/*'
node -v
npm -v
```

**Next.js**

```bash
npx create-next-app@latest my-app
cd my-app
npm run dev
```

---

## 12. 既存ドキュメントからの差分（今回のポイント）

* **Volta は使用しません**（環境は WSL 内に集約）。
* **Git Bash は不要**。以降すべて **Ubuntu（WSL）** で操作します。
* Node は **nvm → npm** で管理・利用します。

---

## 13. 次の一歩（任意）

* GitHub への SSH 鍵登録（慣れてきたら）：

  ```bash
  ssh-keygen -t ed25519 -C "your_email@example.com"
  cat ~/.ssh/id_ed25519.pub   # 表示された鍵をGitHubに登録
  ```
* Cloudflare Pages / Workers 連携（プロジェクトに合わせて設定）。

---

### 最後に

以上で **WSL + npm** の開発環境が完成です。以降は `~/workspace` で新規作成 or `git clone` → `npm run dev` の流れで開発できます。困ったら **トラブルシューティング** を参照してください。
