# 「らじる★らじる」のURL

## NHKラジオをTuneInで聴く方法

NHKの国内向けラジオ放送は、地域局ごとにTuneInのデータベースへ登録されています。

### 登録方法

1. TuneInの検索画面で「NHK」を検索

2. ラジオ第1・第2・FMを選択

3. ハートマークをタップ

4. お気に入りへ追加

---

## 2015年9月の仕様変更

2015年9月から、NHK「らじる★らじる」は配信方式を変更しました。

そのため、

- TuneIn内のローカル局リスト

- 旧ストリーミングURL

では聴取できなくなりました。

代替方法として、TuneInの

> カスタムURL追加機能

を利用してストリーミングURLを登録することで、引き続き聴取できます。

---

## 注意事項

### iOS版 TuneIn Radio Pro

バージョン8以降では不具合があります。

- 再生：可能

- 録音：不可

バージョン7以前では録音可能。

---

# ラジオ第1放送

## 東京

```text

http://netradior1p-i.akamaihd.net/hls/live/200452/1-r1/1-r1-01.m3u8

http://netradior1b-i.akamaihd.net/hls/live/200453/2-r1/2-r1-01.m3u8

```

## 名古屋

```text

http://netradiockr1-i.akamaihd.net/hls/live/208071/1-r1/1-r1-01.m3u8

http://netradiockr1-i.akamaihd.net/hls/live/213182/1-r1/1-r1-01.m3u8

```

## 大阪

```text

http://netradiobkr1-i.akamaihd.net/hls/live/208069/1-r1/1-r1-01.m3u8

http://netradiobkr1-i.akamaihd.net/hls/live/213180/1-r1/1-r1-01.m3u8

```

## 仙台

```text

http://netradiohkr1-i.akamaihd.net/hls/live/208073/1-r1/1-r1-01.m3u8

http://netradiohkr1-i.akamaihd.net/hls/live/213184/1-r1/1-r1-01.m3u8

```

---

# ラジオ第2放送

## 全国共通

```text

http://netradior2p-i.akamaihd.net/hls/live/200454/1-r2/1-r2-01.m3u8

http://netradior2b-i.akamaihd.net/hls/live/200455/2-r2/2-r2-01.m3u8

```

---

# NHK-FM

## 東京

```text

http://netradiofmp-i.akamaihd.net/hls/live/200456/1-fm/1-fm-01.m3u8

http://netradiofmb-i.akamaihd.net/hls/live/200457/2-fm/2-fm-01.m3u8

```

## 名古屋

```text

http://netradiockfm-i.akamaihd.net/hls/live/208072/1-fm/1-fm-01.m3u8

http://netradiockfm-i.akamaihd.net/hls/live/213183/1-fm/1-fm-01.m3u8

```

## 大阪

```text

http://netradiobkfm-i.akamaihd.net/hls/live/208070/1-fm/1-fm-01.m3u8

http://netradiobkfm-i.akamaihd.net/hls/live/213181/1-fm/1-fm-01.m3u8

```

## 仙台

```text

http://netradiohkfm-i.akamaihd.net/hls/live/208074/1-fm/1-fm-01.m3u8

http://netradiohkfm-i.akamaihd.net/hls/live/213185/1-fm/1-fm-01.m3u8

```

---

# TuneInへの登録方法

1. ストリーミングURLをコピー

2. TuneInを起動

3. 「プロファイル」を開く

4. 「カスタムURLを追加」を選択

5. URLを貼り付ける

6. 検索結果のカスタムURLを選択

7. 再生を確認

8. ハートマークを押す

9. 名前を付けて保存

---

## 再生できない場合

URLが次のようになっていないか確認します。

```text

ime.nu/http://...

```

含まれている場合は

```text

ime.nu/

```

を削除して再度登録します。

---

# 他アプリでの利用

これらのURLを利用することで、

- TuneIn Radio

- 一部のメディアプレーヤー

- ストリーミング対応ラジオアプリ

でもNHKラジオを再生できます。

ただし、2015年9月以降のHLS形式（m3u8）に対応している必要があります。

---

# アカマイ（Akamai）について

ストリーミングURLに含まれている

```text

akamaihd.net

```

は、

**Akamai Technologies（アカマイ・テクノロジーズ）**

という世界的なCDN（コンテンツ配信ネットワーク）事業者の配信サーバーです。

公式サイト：

<http://www.akamai.co.jp/>

---

## メモ

- この記事は2015年当時の情報

- 掲載URLの多くは現時点では変更・無効化されている可能性がある

- 歴史的な記録として保管する場合は、その旨を注記しておくとよい