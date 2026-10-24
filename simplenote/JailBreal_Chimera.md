# [JailBreal]Chimera

<https://ichitaso.com/categories/jailbreak/> より

## 記事

2019-11-10

<https://ichitaso.com/jailbreak/ios13-jailbreak-tool-checkra1n/>

## shsh2を保存する前の準備

iOS 12.0-12.4（iOS 12.3.xを除く）デバイスである必要があります。

### 1．OTAアップデートのデータを削除

設定 → 一般 → iPhoneストレージ → OTAアップデートを削除

### 2）ipaファイルをダウンロード

1. iOS 12.0から12.1.2までの場合、Chimeraを使います。
   <https://chimera.sh/>
2. 12.1.3/12.2/12.4の場合、Chimera 1.3.7以降を使います。

上記サイトからipaファイルをダウンロードしましょう。

## ipaファイルをCydia Impactorでインストール

### 1．脱獄するデバイスをPCと接続し、Impactorを起動

ダウンロードした「ipa」をImpactorのウインドウにドラッグ＆ドロップします。

### 2．Apple IDとパスワードを入力

Apple IDとパスワードを入力すると自動的にデバイスへアプリがインストールされます。

もしエラーが起きた場合は、`[Xcode]` → `[Revoke Certificates]`を行ってみてください。

※Apple IDが2段階認証の場合、別途新しいIDを作成しましょう。

<https://appleid.apple.com/account#!&page=create>

### 3．アプリを認証する

そのままでは起動しないため、設定 → 一般 → デバイス管理（またはプロファイルとデバイス管理）を開き、追加したApple IDのメールアドレスをタップ → 信頼をタップしてください。

これでアプリが起動できるようになりました。

## カスタムBoot Nonceをセットする

Windowsで「Chimera」を使った例で説明します。

はじめに「libimobiledevice」をダウンロードしてください。

### 1．Chimeraを起動して下にある設定を開きます

「Set Nonce」をタップして「`0x1111111111111111`」と入力してを「Set」をタップします。
（1が16個）

デフォルトの場合、「`0xbd34a880be0b53f3`」

### 2．JailbreakをタップしてBoot Nonceをセット

Nonceの値が「`0x1111111111111111`」にセットされます。

要はカスタムBoot Nonceが設定できればOKです。
