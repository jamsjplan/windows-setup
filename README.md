# 開発環境セットアップ用ドキュメント

## 対象
- Windows 10/11
- Webアプリ開発（Next.js / Node.js）

## ゴール
1. WSL（Ubuntu）で Node.js + npm が使える
2. Cursor から WSL 上のプロジェクトを編集・起動できる
3. GitHub / Cloudflare に登録できる
4. 新規/既存アプリを `npm run dev` で動かせる

---

## 0. 全体像（やること）

1. Windows に **WSL（Ubuntu）** を入れる
2. Ubuntu を初期設定（アップデート・基本ツール）
3. **Node.js と npm** を入れる（WSL内で nvm→npm を利用）
4. **Cursor**（VS Code系エディタ）を Windows に入れて、WSL とつなぐ
5. GitHub / Cloudflare に登録（リンクあり）
6. 新規 or 既存のプロジェクトを起動

> **用語メモ**
>
> * **WSL**: Windows 上で Linux（今回は Ubuntu）を動かす仕組み。開発が安定・高速になります。
> * **Ubuntu**: Linux の一種。WSL の中で動く“黒い画面”のOSです。
> * **npm**: Node.js 用のパッケージ管理コマンド。今回は **npm** を使います。

## 1. 事前準備（Windows）

* **PowerShell（管理者）** を使います（スタートメニューで「PowerShell」を検索 → 右クリック → *管理者として実行*）。

---

## 2. WSL（Ubuntu）をインストール

### 2-1. もっとも簡単な入れ方（Windows 11 / 10 共通）

1. **PowerShell（管理者）** で次を実行：

   ```powershell
   wsl --install
   ```
2. 指示に従って **再起動**。
3. 再起動後、自動で **Ubuntu** の初回セットアップが始まります。ユーザー名・パスワードを入力して完了。

### 2-2. インストール確認

PowerShell で次を実行して、**VERSION が 2** になっていればOKです。

```powershell
wsl -l -v
  NAME              STATE           VERSION
* Ubuntu            Running         2
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
   ```
   
3. **作業フォルダ** を WSL 内に作成。

   ```bash
   mkdir -p ~/workspace
   cd ~/workspace
   ```

---

## 4. Node.js と npm を入れる（Voltaなし／nvm利用）

> npm を使うために、まず Node.js を入れます。WSL では **nvm（Node Version Manager）** を使うのが簡単＆安全です。

1. **nvm のインストール**

   ```bash
   sudo apt-get install curl
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
   ```
2. **Node.js（LTS）をインストール**

   ```bash
   sudo apt install nodejs -y
   ```
   
3. **バージョン確認**（数字が表示されればOK）

   ```bash
   node -v   # 例: v22.x または LTS のバージョン
   npm -v    # 例: 10.x 以上
   ```

---

## 5. Cursor（エディタ）を Windows にインストール＆WSL と接続

1. Windows に **Cursor** をインストール（公式手順に従って通常インストール）。
2. Cursor を起動 → 左下の「**><**」アイコン（リモート）から **WSL: Ubuntu** を選択 → *Open Folder* で `~/workspace` を開く。

---

### GitHubへの登録
[ここ](https://github.com/jamsjplan/windows-setup/blob/main/GitHub.md)を参照してください。

### CloudFlareへの登録
[ここ](https://github.com/jamsjplan/windows-setup/blob/main/GitHub.md)を参照してください。

---
※以下は実際の開発環境を立ち上げる際の参考手順です。

## 開発フォルダに移動
<img width="800" alt="image" src="https://github.com/user-attachments/assets/12cc6588-0410-4dce-beaa-b676b10b40c1" />

例えば、↑のようにユーザフォルダの`workspace`フォルダで開発したい場合、以下のどちらかを行ってください。

### 方法1:エクスプローラーのパスのところで`cmd`と入力

<img width="800" alt="image" src="https://github.com/user-attachments/assets/5ee0d816-17c9-43dd-87c5-646b430bfea8" />

### 方法2:Git Bash
```bash
cd workspace/
```

## 新しくプロジェクトを作成する場合
```bash
npx create-next-app@latest <アプリケーション名>
cd <アプリケーション名>
```

## 既存のアプリケーションを実行する場合
## ソースコードの取得
```bash
# Git Hubリポジトリ（=アプリケーションのソースコード）をクローン
git clone <リポジトリのURL>
cd <プロジェクト名>
```

## アプリケーションの動作確認
```bash
# 依存関係をインストール
npm install

# 開発サーバーを起動
npm run dev
```

http://localhost:3000 にアクセスすると、アプリケーションを確認することができます。

# ⚠️エラーが出た場合
以下のようなエラーが出た場合、以下のコマンドを実行してください。

> 'next' は、内部コマンドまたは外部コマンド、
> 操作可能なプログラムまたはバッチ ファイルとして認識されていません。

```bash
npm install next@latest react@latest react-dom@latest
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


