# ［JailBreak]【Chimera】PC不要＆デバイス単体で「iOS 12.0〜12.2 / iOS 12.4」を脱獄する方法！

<https://tools4hack.santalab.me/howto-ios12-124-jailbreak-chimera-without-pc-safari-install-version.html>

2019/08/22 20:25

## 対応状況

- 【iOS 12.0〜12.2 / iOS 12.4対応】
  - iPhone 5s、SE、6、6 Plus、6s、6s Plus、7、7 Plus、8、8 Plus、X
  - iPod touch 6G、7G
  - iPad Air、Air 2、Pro 12.9、Pro 12.9（2017)、Pro 9.7、iPad 5、Pro 10.5、iPad 6
  - iPad mini 2、mini 3、mini 4
- 【iOS 12.0〜12.1.2対応】
  - iPhone XS、XS Max、XR
  - iPad Pro 12.9 (2018)、Pro 11インチ

## ① Chimeraのインストール

### 1-1 Safariからインストール

Safariにて【Chimeraのインストール】を開き、出現したポップアップの「開く」を選択。更にもう一つポップアップが出現するので、「インストール」を選択してください。
これでホーム画面に戻ると、Chimeraのインストールが開始されているハズです（インストール完了まで数分掛かる場合があります）。

- <https://share.tweakboxapp.com/s/tweakbox/chimera-jailbreak>
- <https://tools4hack.santalab.me/fixed-tweakbox-resigned-allow-install-chimera-unc0ver-apps-20190825.html>

### 1-2 プロファイルの信頼を行う

Chimeraのインストール完了をホーム画面上で確認後、Chimeraを起動できるように「信頼」作業を行っていきます。

設定アプリを起動し【一般 > プロファイルとデバイス管理（or デバイス管理）】を開き、追加されたプロファイル（名称は画像とは違う場合があります）を選択してください。

続いて【“○○”を信頼】というボタンを選択（青文字部分をタップ）。更にポップアップでも『信頼』を選択しましょう。これで起動できるようになりました！

## ② 脱獄を行う！

【注意】：設定アプリ > 一般 > iPhoneのストレージ…からiOS 12.2などのOTAアップデートのデータがある場合は、削除を行ってください。削除後、再起動を行ってからChimeraでの脱獄作業に移りましょう。
詳しくは『Electraで脱獄を行う前に「OTAアップデート」のデータ削除を！ブートループの可能性も』を御覧ください。

### 2-1 実行「1回目」

- ホーム画面へ戻り『Chimera』アプリを起動。
- 画面中央にある『Jailbreak』ボタンをタップしましょう。

成功すると、1回目は「Reboot required」と最後に表示され、OKを押すと自動で再起動が行われます。これは正常な動作で、成功となります。次のステップへ進んでください。

この際、1/3でアプリが閉じてしまったり、デバイスが勝手に再起動してしまう場合は失敗となるため、改めてChimeraを起動してやり直しましょう。

### ④ 実行「2回目」

- デバイス再起動後、ホーム画面から『Chimera』アプリを起動。
- 前項と同じ様に画面中央にある『Jailbreak』ボタンをタップ。次は【2/3】や【3/3】と進んで行きますので、自動で終了するまでジッと待機。成功すると、自動でリスプリングが行われます。

リスプリング後、ホーム画面に【Sileo】が追加され、Sileoの起動が行えれば…成功です！！

### デバイスを再起動したあとは…

デバイスを再起動（リスプリングは関係なし）すると、いったん全ての脱獄アプリが動作を停止します。これまで同様、今回の脱獄でも仕様です。
停止した脱獄アプリはどのように動作を再開させるのか？という事ですが、再起動を行ったら以下の作業をすることで通常の脱獄環境に戻せますので、覚えておきましょう！

- 再起動を行ったら、ホーム画面から『Chimera』アプリを起動。
- 『Jailbreak』ボタンをタップし、【3/3】後に自動でリスプリングが行われれば、完了です。

リスプリングが完了すると、脱獄環境へと戻っています。

この際、1/3でアプリが閉じてしまったり、デバイスが勝手に再起動してしまう場合は失敗となるため、デバイス再起動後に改めてChimeraを起動してやり直しましょう。

### 【オススメ】ReProvisionでの署名に切り替える

今回の手法でインストールした場合、Chimeraを起動できるようにする「署名」がいつまで有効か分かりません。

そのため、脱獄後は署名を自身のApple IDでの署名に変更しておくと安心。
Chimeraアプリを【ReProvision】にて自動再署名する様にしておけば、署名切れの心配もかなり少なくなります。

<https://tools4hack.santalab.me/jbapp-com-matchstic-reprovision.html>

詳しい使い方については【TweakBoxなどからインストールした脱獄用アプリをReProvisionでの自動再署名に切り替える方法】を参考にしてみてください！

<https://tools4hack.santalab.me/howto-tweakbox-jailbreaksfun-to-reprovision-chimera-unc0ver-electra.html>
