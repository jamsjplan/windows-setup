# windows-setup
Windows 向けの開発環境セットアップ用リポジトリ

インストールするもの
- Git Bash
- Volta

## :one:Git Bashのインストール
Windows の開発環境では、標準のコマンドプロンプトよりもGit Bashを利用した方がLinux/Unix系コマンドに近い操作ができ、ドキュメントや他の開発者の手順に従いやすくなります。

### ダウンロード
[Git for Windows 公式サイト](https://gitforwindows.org/) からインストーラーをダウンロードします。
<img width="1899" height="911" alt="image" src="https://github.com/user-attachments/assets/fa4c08d3-2cef-4bca-94ac-a2925962d537" />

「Download」をクリックし、ダウンロードしたインストーラーを起動

<img width="330" height="158" alt="image" src="https://github.com/user-attachments/assets/51135cad-27d1-4283-8198-d2e85f735d93" />

### インストール手順
参考：https://qiita.com/suke_masa/items/404f06309bb32ca6c9c5

基本的には「Next」のままでok

### インストールできたか確認
インストール後、スタートメニューからGit Bashを起動し、以下のコマンドを入力します:

```bash
git --version
```
Gitのバージョンが表示されればokです。

<img width="779" height="676" alt="image" src="https://github.com/user-attachments/assets/a30825af-ea28-464b-a76f-fdbf85c6d74d" />

<img width="574" height="361" alt="image" src="https://github.com/user-attachments/assets/e48f6ca4-9365-4d37-92e1-01e22805c3cb" />

## :two:Voltaのインストール
[ここ](https://zenn.dev/longbridge/articles/30c70144c97d32)に書いてある手順で進めてokです。
以下はサイトが削除されてしまった時に備えて残しておきます。

### インストールする前に
以前にNodeバージョン管理ツールやNodeをインストールしている場合は、完全にアンインストールしておいてください。

### Windows用のインストーラーをダウンロード
[Volta公式サイト](https://volta.sh/)「Getting Started」から「download and run the Windows installer」のリンクをクリックし、インストーラーをダウンロードします。

<img width="1920" height="914" alt="image" src="https://github.com/user-attachments/assets/22513473-5737-443c-8f8f-ebdc3af57197" />

### Windows開発者モードをを有効にする
VoltaはWindowsの開発者モードを有効にしておく必要があります。
Windows開発者モードをONにしておかないと、Angular CLIのインストール時にVoltaのエラーが発生します。
検索ボックスに「開発者」と入力し、「開発者向け機能を使う」を起動します。

<img width="783" height="679" alt="image" src="https://github.com/user-attachments/assets/7af7d0f7-eacd-4892-95b6-4cf60f5ce378" />

開発者モードをオンにします。

<img width="461" height="122" alt="image" src="https://github.com/user-attachments/assets/391ce175-7617-4731-a294-03f2e2e6b097" />


### Voltaをインストール
ダウンロードしたインストーラーを実行します。デフォルトのままでインストールしてokです。
「このアプリがデバイスに変更を加えることを許可しますか？」と表示された場合は「はい」を選択してください。

### インストールできたか確認
コマンドラインを起動して以下のように入力します。バージョンが表示されればokです。

```bash
volta --version
```

<img width="548" height="282" alt="image" src="https://github.com/user-attachments/assets/70057d5a-f091-4973-8b06-1e7ab008297b" />


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

