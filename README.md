# 開発環境セットアップ用ドキュメント

## 対象
- Windows 10/11
- Webアプリケーション開発

## 登録するサービス
  - GitHub：アプリのソースコード管理サービス
  - Cloudflare：アプリを展開できるクラウドサービス
## PCにインストールするもの
  - Cursor：AIコードエディタ
  - Volta：バージョン管理ツール

### GitHubへの登録
<details>

<summary>折り畳み</summary>

### You can add a header

You can add text within a collapsed section.

You can add an image or a code block, too.

```ruby
   puts "Hello World"
```

</details>

## :two:Voltaのインストール
[ここ](https://zenn.dev/longbridge/articles/30c70144c97d32)に書いてある手順で進めてokです。
以下はサイトが削除されてしまった時に備えて残しておきます。

### インストールする前に
以前にNodeバージョン管理ツールやNodeをインストールしている場合は、完全にアンインストールしておいてください。

### Windows用のインストーラーをダウンロード
[Volta公式サイト](https://volta.sh/)「Getting Started」から「download and run the Windows installer」のリンクをクリックし、インストーラーをダウンロードします。

<img width="800" alt="image" src="https://github.com/user-attachments/assets/22513473-5737-443c-8f8f-ebdc3af57197" />

<img width="800" alt="image" src="https://github.com/user-attachments/assets/f5114163-d539-4dad-8a70-65b1d77133c8" />

青く選択している箇所のリンクをクリックしてください。

<img width="800" alt="image" src="https://github.com/user-attachments/assets/f636de56-dcc4-48fb-9503-4aef0a3cc8a6" />

ここは`-windows-x86_64.msi`が付いているものをクリックしてください。


### Windows開発者モードをを有効にする
VoltaはWindowsの開発者モードを有効にしておく必要があります。
Windows開発者モードをONにしておかないと、Angular CLIのインストール時にVoltaのエラーが発生します。
検索ボックスに「開発者」と入力し、「開発者向け機能を使う」を起動します。

<img width="800" alt="image" src="https://github.com/user-attachments/assets/7af7d0f7-eacd-4892-95b6-4cf60f5ce378" />

開発者モードをオンにします。

<img width="461" height="122" alt="image" src="https://github.com/user-attachments/assets/391ce175-7617-4731-a294-03f2e2e6b097" />


### Voltaをインストール
ダウンロードしたインストーラーを実行します。デフォルトのままでインストールしてokです。
「このアプリがデバイスに変更を加えることを許可しますか？」と表示された場合は「はい」を選択してください。

### インストールできたか確認
Git Bashを起動して以下のように入力します。バージョンが表示されればokです。

```bash
volta --version
```

<img width="500" alt="image" src="https://github.com/user-attachments/assets/70057d5a-f091-4973-8b06-1e7ab008297b" />


### Node.jsをダウンロードしてインストールする：
```bash
volta install node@22
```

### Node.jsのバージョンを確認する：
```bash
node -v # "v22"以上が表示されればok。
```

### npmのバージョンを確認する：
```bash
npm -v # "10"以上が表示されればok。
```

<img width="601" height="363" alt="image" src="https://github.com/user-attachments/assets/0b09bd71-f067-484c-b7d9-14e239208709" />


ここまで確認ができたら、PCを再起動してください。

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

```bash
pwd # 現在いるフォルダの位置を確認
/c/Users/JAMS MK/workspace # このようになってればok
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
