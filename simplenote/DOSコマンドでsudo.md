#DOSコマンドでsudo
- 2026-10-18

- Windows 11（バージョン 24H2 以降）なら、Linux の sudo <command> と同じことが 正式に できます。
	- → sudo <コマンド> をそのまま CMD で使えるようになりました。

  

  

## 1行で管理者権限で実行する方法（Windows 11 公式 “sudo for Windows”）

- Windows 11 24H2 以降では、Microsoft が ネイティブ sudo を追加しました。

- 有効化すると、以下のように使えます：

  

sudo netstat -ab

sudo notepad C:\Windows\System32\drivers\etc\hosts

sudo diskpart

  

Linux と同じく sudo を先頭につけるだけで管理者権限で実行されます。

  

# ■sudo を有効化する手順（Windows 11 24H2 以降）

設定 → システム → 開発者向け

  

1 .「sudo を有効化」 を ON にする

2. モードを選択（後述）

  

※ sudo は Windows 11 version 24H2 以上で利用可能

  

# ■sudo の 3 モード（Linux と同じ動作に近いのは “Inline”）

Windows sudo には 3 種類の動作モードがあります：

  

1. Inline（normal） ← Linux の sudo と同じ動作

現在の CMD ウィンドウ内で昇格して実行

入力も受け付ける

最も Linux に近い挙動

  

2. Input disabled（disableInput）

現在のウィンドウで実行

入力は受け付けない（セキュリティ強化）

  

3. New window（forceNewWindow）

新しい管理者ウィンドウを開いて実行

runas に近い挙動

デフォルト設定

  

# ■sudo の設定変更（管理者 CMD で実行）

sudo config --enable normal

sudo config --enable disableInput

sudo config --enable forceNewWindow

  

# ■もし Windows 11 が 24H2 未満の場合

公式 sudo は使えません。

その場合は runas を使う必要がありますが、Linux の sudo のように「同じウィンドウで昇格」はできません。

  

代替：runas（ただし Linux の sudo とは違う）

runas /user:Administrator "cmd /c <コマンド>"

例：

runas /user:Administrator "cmd /c netstat -ab"

※ runas は パスワード入力が必要で、Linux の sudo のようなスムーズさはありません。

# ■Windows 11 と DOS の違い（要点）
- Windows 11 は MS-DOS を OS として使っていない
- しかし DOS互換コマンドは cmd.exe 内で完全に動作
- PowerShell や Windows Terminal も使えるが、昔の DOS コマンドを使いたいなら cmd.exe が最適

