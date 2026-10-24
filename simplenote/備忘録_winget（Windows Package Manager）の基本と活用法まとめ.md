# [備忘録] winget（Windows Package Manager）の基本と活用法まとめ

2026-05-15

<https://qiita.com/Tadataka_Takahashi/items/fd36ac13f833fc06f9ac>

\#Windows  
\#winget  
\#アプリ管理

最終更新日 2025年05月07日  
投稿日 2025年05月07日

もしも、なんかWindowsでコマンドラインからソフト管理できるツールあったなと思った方、「winget」をチェックしてみてください。開発環境の一括構築とか更新が楽になります。パッケージのエクスポート/インポートで環境の完全再現もできて便利。Win11ではデフォルトプリインストールされてるの知らなかった...😅

## はじめに

Windows環境でも、macOSのbrewやLinuxのaptのようにCLIでパッケージ管理を行いたい――そんな要望に応えるのがwingetです。本記事では、wingetの基本的な使い方から、便利な活用法までを備忘録としてまとめました。

winget-diagram.png

## wingetとは？

- Microsoftが提供する公式パッケージマネージャ
- GUIアプリ・CLIツールをコマンドラインからインストール・管理できる
- パッケージはMicrosoft Storeおよび独自リポジトリに登録されたもの
- App Installerの一部として配布・更新される

## インストール方法

### Windows 11の場合

Windows 11では標準でプリインストールされています。PowerShellやコマンドプロンプトで`winget -v`を実行して確認できます。

### Windows 10の場合

- Microsoft Storeから「App Installer」を検索してインストール
- または、GitHub releasesから最新のインストーラをダウンロード

## 基本コマンド一覧

| 操作 | コマンド例 | 説明 |
| --- | --- | --- |
| パッケージ検索 | `winget search vscode` | 名前や説明に"vscode"を含むアプリを検索 |
| インストール | `winget install Microsoft.VisualStudioCode` | 指定パッケージをインストール |
| アップグレード | `winget upgrade` | アップデート可能なパッケージを一覧表示 |
| 一括更新 | `winget upgrade --all` | すべてのパッケージを一括更新 |
| 個別更新 | `winget upgrade nodejs` | 特定パッケージのみ更新 |
| アンインストール | `winget uninstall Git.Git` | 指定パッケージをアンインストール |
| 一覧表示 | `winget list` | インストール済みパッケージの一覧 |
| エクスポート | `winget export -o packages.json` | インストール済みパッケージをエクスポート |
| インポート | `winget import packages.json` | エクスポートしたパッケージをインストール |
| 詳細表示 | `winget show Microsoft.PowerToys` | 特定パッケージの詳細情報を表示 |

## よく使うTips

### パッケージIDの確認

```powershell
winget search [パッケージ名]
```

正確なインストールにはパッケージIDが必要（例：Git.Git）。よく使うパッケージIDを覚えておくと効率的です。

### 管理者権限が必要な操作

一部のソフトは管理者権限が必要。cmdやPowerShellを「管理者として実行」してからwingetを使いましょう。

### 一括インストール（スクリプト）

```powershell
winget install Git.Git
winget install Microsoft.VisualStudioCode
winget install Python.Python.3.12
```

開発環境の初期構築に便利です。

### 構成ファイル（Configuration）の活用

YAMLとPowerShell DSC（Desired State Configuration）を組み合わせたConfiguration機能が利用可能です。これにより、複数のインストールやシステム設定を一度に適用できます。

```yaml
# config.yaml
properties:
  applications:
    - id: Microsoft.PowerToys
    - id: Microsoft.VisualStudioCode
    - id: Git.Git
```

適用するには：

```powershell
winget configure config.yaml
```

### PowerShellモジュールやCOM APIの活用

wingetはCLI以外にもPowerShellモジュールやCOM APIが提供されており、スクリプトやプログラムからの制御も可能です。

## よく使うおすすめパッケージ

| アプリ名 | パッケージID | 備考 |
| --- | --- | --- |
| Visual Studio Code | `Microsoft.VisualStudioCode` | 軽量エディタ |
| Git | `Git.Git` | バージョン管理 |
| Node.js | `OpenJS.NodeJS.LTS` | フロントエンド開発 |
| Python | `Python.Python.3.12` | バージョンを指定可 |
| PowerToys | `Microsoft.PowerToys` | 便利なユーティリティ集 |
| Windows Terminal | `Microsoft.WindowsTerminal` | 高機能ターミナル |
| 7-Zip | `7zip.7zip` | 圧縮解凍ソフト |
| PowerShell 7 | `Microsoft.PowerShell` | 最新のPowerShell |
| Docker Desktop | `Docker.DockerDesktop` | コンテナ開発環境 |

## セキュリティと信頼性

- wingetはMicrosoft公式ツールでアプリケーションの安全なインストールを実現
- パッケージは検証済みリポジトリから提供され、不要なバンドルソフトウェアのリスクを排除
- SSLによる暗号化接続とデジタル署名で安全な配布を実現

## よくあるトラブルと対策

| 問題 | 原因例 | 解決法 |
| --- | --- | --- |
| wingetが使えない | Windowsバージョンが古い | Windowsを更新、App Installerを導入 |
| インストールが途中で失敗する | 管理者権限不足、ネットワークエラーなど | 管理者で再実行、VPN確認 |
| 特定のソフトが見つからない | パッケージIDが不正、リポジトリに未登録 | `winget search`で正しいIDを確認 |
| 更新時に「一致するパッケージが見つかりません」 | パッケージ名とIDの不一致 | `--id` オプションとパッケージID指定で解決 |

## 高度な使い方

### カスタムソースの追加

```powershell
winget source add <名前> <URL>
```

### スクリプトによる環境の完全な再現

インストールしたパッケージをエクスポートし、新しい環境で再インポートすることで開発環境を完全に再現できます。

```powershell
# 現在の環境をエクスポート
winget export -o myenv.json

# 新環境でインポート
winget import myenv.json
```

### 一括アンインストール

特定のパターンに一致するすべてのアプリを一括でアンインストールできます。

```powershell
winget list | findstr "古いアプリ名パターン" | foreach { winget uninstall $_ }
```

## おわりに

wingetを活用すれば、Windows環境でもCLIでソフトを一括管理でき、再セットアップや環境構築が圧倒的に効率化されます。開発者やIT系ユーザーならぜひ活用したいツールです。

## 関連リンク

- 公式ドキュメント（Microsoft Learn）
- winget-cli GitHub
- winget.run (パッケージ検索サイト)

## 免責事項

本記事の作成にあたり、文章および図解の一部に生成AIを活用しています。最終的な編集および内容の確認は筆者が責任を持って行っています。
