# [News] iPhone 8やiPhone Xを脱獄させる新たな手法が発見される、パッチによる修正は不可能 - GIGAZINE

2019-9–30

---

<https://zunda-hack.com/2020:04/01/bootrom-exploit-checkm8-jailbreak-tool-fugu-release/>

2020.04.01

## Fugu」がリリース!!

2020.04.01 17:09

**目次**

- checkm8
- Fugu
- 特徴

---

<https://gigazine.net/news/20190930-checkm8-idevice-jailbreak-exploit/>

セキュリティについて研究するaxi0mX氏という人物が、「Checkm8」と名付けられた新たなiPhoneのジェイルブレイク(脱獄)手法を発見し、GitHub上に必要なコードを除いた手順を公開しました。Checkm8はiPhone 4s～iPhone Xにわたる幅広い種類のデバイスをジェイルブレイクさせることが可能となっています。

- [ipwndfu/checkm8.py at master · axi0mX/ipwndfu · GitHub](https://github.com/axi0mX/ipwndfu/blob/master/checkm8.py)
- [Developer of Checkm8 explains why iDevice jailbreak exploit is a game changer | Ars Technica](https://arstechnica.com/information-technology/2019/09/developer-of-checkm8-explains-why-idevice-jailbreak-exploit-is-a-game-changer/)

iPhoneなどのデバイスをジェイルブレイクすることは、開発企業がデバイスのOSに課した制限を回避することを可能にし、正規のアプリストア以外のプラットフォームからアプリをダウンロードしたり、デバイスを自由にカスタマイズしたりできます。また、悪意のあるハッカーが特定のデバイスをジェイルブレイクさせてマルウェアをインストールしたり、捜査機関が押収したデバイスを操作したりすることを可能にします。

axi0mX氏が発見したCheckm8は多くのジェイルブレイク方法とは異なり、Apple製品が起動した際に最初に実行されるコードを含むブートROMの脆弱性を突いた方法です。Checkm8はA12以降のプロセッサが搭載されたiPhone XSやiPhone 11では動作しませんが、A5～A11までのプロセッサに影響するため、iPhone 4s～iPhone Xという幅広いデバイスに対して有効で、利用可能なデバイスは世界中に数億台以上もあるとみられています。

実際にaxi0mX氏はCheckm8を使ってiPhone Xをジェイルブレイクしており、その様子を撮影したムービーをTwitter上で公開しています。

ブートROMはプロセッサ内の読み取り専用メモリにあるため、Appleが新たな修正パッチを配布して脆弱性を更新することができません。そのため、最新版のiOSをインストールしたデバイスでもジェイルブレイク可能で、実質的にCheckm8は半永久的に有効なジェイルブレイク方法だといえるとのこと。

axi0mX氏によると、Checkm8は対象となるデバイスへの物理的なアクセスが必要であり、他の脆弱性と組み合わせてもリモートでは実行できないそうです。また、再起動をするとデバイスはジェイルブレイクされていない状態に戻るため、もし永続的にデバイスをジェイルブレイク状態にしたいのであれば、デバイスを再起動するたびに物理的にアクセスしなければなりません。

Checkm8が悪意を持つ人物によって悪用される可能性について、axi0mX氏は「悪用される可能性はそれほど高くない」と考えています。AppleはiPhone 6以降のデバイスに、Secure Enclaveというパスコードと指紋のデータを格納するセキュリティプロセッサを搭載しています。Checkm8がSecure Enclaveに影響することはないため、もしデバイス内のデータを第三者が見たいと思っても、パスワードや生体認証を突破しなければデータを盗むことはできないとのこと。

悪意のある人物が第三者のスマートフォンを入手し、Checkm8を使って悪意のあるマルウェアをインストールする可能性はあるそうですが、こうした攻撃者は物理的アクセスを好まないとaxi0mX氏は指摘。他にもリモートでターゲットを攻撃する方法が存在しているため、実際にCheckm8を使って攻撃が加えられる危険性はそれほど高くないとaxi0mX氏は考えています。
