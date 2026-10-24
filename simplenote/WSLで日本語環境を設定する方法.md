# [WSLで日本語環境を設定する方法]

2026-08-18

<https://www.bing.com/ck/a?!&&p=485cc185c1d243c307ef618e4b2612bb299eef51273ed86e0091db211057d0e2JmltdHM9MTc4NTg4ODAwMA&ptn=3&ver=2&hsh=4&fclid=00891384-af65-6880-38d3-0668ae3d6989&psq=wsl+%e6%97%a5%e6%9c%ac%e8%aa%9e&u=a1aHR0cHM6Ly96ZW5uLmRldi9yeXV1L2FydGljbGVzL3dzbDItbG9jYWxlLWpw&ntb=1>

[1](https://www.bing.com/ck/a?!&&p=485cc185c1d243c307ef618e4b2612bb299eef51273ed86e0091db211057d0e2JmltdHM9MTc4NTg4ODAwMA&ptn=3&ver=2&hsh=4&fclid=00891384-af65-6880-38d3-0668ae3d6989&psq=wsl+%e6%97%a5%e6%9c%ac%e8%aa%9e&u=a1aHR0cHM6Ly96ZW5uLmRldi9yeXV1L2FydGljbGVzL3dzbDItbG9jYWxlLWpw&ntb=1)[2](https://www.bing.com/ck/a?!&&p=fd1c54cb17abc111021e7e684354d15a2ee4644baaff049ff329ea32f9e2ec49JmltdHM9MTc4NTg4ODAwMA&ptn=3&ver=2&hsh=4&fclid=00891384-af65-6880-38d3-0668ae3d6989&psq=wsl+%e6%97%a5%e6%9c%ac%e8%aa%9e&u=a1aHR0cHM6Ly9xaWl0YS5jb20vaXRsZWdhY3kvaXRlbXMvOWI3Y2E3Y2JiYWJkYzRlMDAyOGM&ntb=1)[3](https://www.bing.com/ck/a?!&&p=451afcf8a8a0a8801a9688392cb067876825351d9d8425b79628f0d25e80f145JmltdHM9MTc4NTg4ODAwMA&ptn=3&ver=2&hsh=4&fclid=00891384-af65-6880-38d3-0668ae3d6989&psq=wsl+%e6%97%a5%e6%9c%ac%e8%aa%9e&u=a1aHR0cHM6Ly96ZW5uLmRldi9hdHN1c2hpZngvYXJ0aWNsZXMvd3NsMi1zZXR1cC1kZWJpYW4tamFwYW5lc2U&ntb=1)

WSL（Windows Subsystem for Linux）上で日本語環境を設定することで、システムメッセージやマニュアルを日本語で表示できるようになります。以下は、UbuntuやDebianを例にした手順です。

## 1. システムの更新

まず、システムを最新の状態にします。

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. 日本語言語パックのインストール

日本語ロケールとマニュアルをインストールします。

```bash
sudo apt install -y language-pack-ja manpages-ja manpages-ja-dev
```

## 3. ロケールの設定

日本語ロケールを有効化し、デフォルトに設定します。

```bash
sudo update-locale LANG=ja_JP.UTF-8
sudp
```

設定後、以下のコマンドで確認してください。

```bash
locale
```

出力例:

```text
LANG=ja_JP.UTF-8
```

## 4. タイムゾーンの設定

タイムゾーンを日本時間（Asia/Tokyo）に変更します。

```bash
sudo timedatectl set-timezone Asia/Tokyo
```

確認:

```bash
date
```

出力例:

```text
2025年 3月 26日 水曜日 20:39:15 JST
```

## 5. 日本語入力システムのインストール（オプション）

日本語入力が必要な場合は、以下をインストールします。

```bash
sudo apt install -y fcitx5-mozc dbus-x11 fonts-noto-cjk fonts-noto-cjk-extra fonts-ipafont
```

環境変数を設定:

```bash
echo "export GTK_IM_MODULE=fcitx5

export QT_IM_MODULE=fcitx5

export XMODIFIERS=@im=fcitx5" >> ~/.bashrc

source ~/.bashrc
```

## 6. WSLの再起動

設定を反映させるため、WSLを再起動します。

```powershell
wsl --shutdown
```

## 7. 動作確認

- ロケール確認: `locale`
- タイムゾーン確認: `date`
- 日本語入力確認: `fcitx5 &`

これでWSL上で快適な日本語環境が構築できます。

詳細情報:

- [1 -zenn.dev](https://www.bing.com/ck/a?!&&p=485cc185c1d243c307ef618e4b2612bb299eef51273ed86e0091db211057d0e2JmltdHM9MTc4NTg4ODAwMA&ptn=3&ver=2&hsh=4&fclid=00891384-af65-6880-38d3-0668ae3d6989&psq=wsl+%e6%97%a5%e6%9c%ac%e8%aa%9e&u=a1aHR0cHM6Ly96ZW5uLmRldi9yeXV1L2FydGljbGVzL3dzbDItbG9jYWxlLWpw&ntb=1)
- [2 -qiita.com](https://www.bing.com/ck/a?!&&p=fd1c54cb17abc111021e7e684354d15a2ee4644baaff049ff329ea32f9e2ec49JmltdHM9MTc4NTg4ODAwMA&ptn=3&ver=2&hsh=4&fclid=00891384-af65-6880-38d3-0668ae3d6989&psq=wsl+%e6%97%a5%e6%9c%ac%e8%aa%9e&u=a1aHR0cHM6Ly9xaWl0YS5jb20vaXRsZWdhY3kvaXRlbXMvOWI3Y2E3Y2JiYWJkYzRlMDAyOGM&ntb=1)
- [3 -zenn.dev](https://www.bing.com/ck/a?!&&p=451afcf8a8a0a8801a9688392cb067876825351d9d8425b79628f0d25e80f145JmltdHM9MTc4NTg4ODAwMA&ptn=3&ver=2&hsh=4&fclid=00891384-af65-6880-38d3-0668ae3d6989&psq=wsl+%e6%97%a5%e6%9c%ac%e8%aa%9e&u=a1aHR0cHM6Ly96ZW5uLmRldi9hdHN1c2hpZngvYXJ0aWNsZXMvd3NsMi1zZXR1cC1kZWJpYW4tamFwYW5lc2U&ntb=1)
