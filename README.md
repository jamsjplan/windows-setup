# windows-setup
Windows 向けの開発環境セットアップ用リポジトリ

インストールするもの
- Git Bash
- Volta

## Git Bashをインストールする
Windows の開発環境では、標準のコマンドプロンプトよりもGit Bashを利用した方がLinux/Unix系コマンドに近い操作ができ、ドキュメントや他の開発者の手順に従いやすくなります。

### ダウンロード
[Git for Windows 公式サイト](https://gitforwindows.org/) からインストーラーをダウンロードします。
<img width="1899" height="911" alt="image" src="https://github.com/user-attachments/assets/fa4c08d3-2cef-4bca-94ac-a2925962d537" />

「Download」をクリックし、ダウンロードしたインストーラーを起動

<img width="330" height="158" alt="image" src="https://github.com/user-attachments/assets/51135cad-27d1-4283-8198-d2e85f735d93" />

### インストール手順
参考：https://qiita.com/suke_masa/items/404f06309bb32ca6c9c5

### 動作確認
インストール後、スタートメニューから **Git Bash** を起動し、以下のコマンドを入力します:
```bash
git --version
インストールされた Git のバージョンが表示されれば成功です。
```

## Voltaをインストールする前に
以前にNodeバージョン管理ツールやNodeをインストールしている場合は、完全にアンインストールしておきます。

## Voltaをインストールする
参考：https://zenn.dev/longbridge/articles/30c70144c97d32

### Windows用のインストーラーをダウンロード
[Volta公式サイト](https://volta.sh/)「Getting Started」から「download and run the Windows installer」のリンクをクリックし、インストーラーをダウンロードします。

### Windows開発者モードをを有効にする
VoltaはWindowsの開発者モードを有効にしておく必要があります。
Windows開発者モードをONにしておかないと、Angular CLIのインストール時にVoltaのエラーが発生します。
検索ボックスに「開発者」と入力し、「開発者向け機能を使う」を起動します。

開発者モードをオンにします。

### Voltaをインストール
ダウンロードしたインストーラーを実行します。
デフォルトのままでインストールしていきます。
ここで
「このアプリがデバイスに変更を加えることを許可しますか？」と表示されるので
「はい」を選択します。

### Voltaの動作確認
コマンドラインを起動して`volta`と入力します。バージョンが表示されていることが確認できます。

### Node.jsをダウンロードしてインストールする：
```bash
volta install node@22
```

### Node.jsのバージョンを確認する：
```bash
node -v # "v22.19.0"が表示される。
```

### npmのバージョンを確認する：
```
npm -v # "10.9.3"が表示される。
```

## プロジェクトの動作確認
```bash
# リポジトリをクローン
git clone <リポジトリのURL>
cd <プロジェクト名>

# 依存関係をインストール
npm install

# 開発サーバーを起動
npm run dev
```

