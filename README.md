# Raspberry Pi を試してみた

## 用意したもの
* Raspberry Pi3 Model B ボード＆ケースセット 3ple Decker対応(Element14版, Clear)-Physical Computing Lab
* Raspberry Pi 3 model B 専用電源 ACアダプタ(ブラック) 5.1V/2.5A
* Samsung micro SDHCカード 32GB EVO+ Class10 UHS-I対応(最大読出速度80MB/s:最大書込速度20MB/s) MB-MC32DA/FFP

![用意したもの](/images/img01.JPG)


## Raspberry Pi を動作させるまで

Raspberry Piは購入直後からいきなり利用できるものではなく、初期セットアップが必要なようです。
自分としては手順が多かったので、備忘録としてまとめておこうと思います。

1. SDカードをフォーマットする。<br>
フォーマットは「SDFormatter V4.0」というツールを使用するようです。<br>
https://www.sdcard.org/jp/downloads/formatter_4/eula_windows/index.html

1. SDFormatterを使用して、フォーマットオプション設定を「上書きフォーマット」「ON」に設定し、SDカードをフォーマットします。<br>
![SDFormatterのオプション設定](/images/img02.png)

1. Raspberry Pi を動作させるために必要なOSイメージをダウンロードします。<br>
https://www.raspberrypi.org/downloads/noobs/<br>
ここから「NOOBS」というのをダウンロードします。<br>
※NOOBS … New Out Of Box Software

1. ダウンロードしたNOOBSを解凍し、回答した中身を全てSDカードへ保存します。<br>
![SDカードの中身](/images/img03.png) <br><br><br>
以上でOSの準備が完了したため、いよいよRaspberry Piの起動です！

1. Raspberry Piに周辺機器（キーボードやディスプレイ、マウスなど）を接続し、電源をさして起動します。<br>
※電源となるmicroUSBケーブルを刺すと起動してしまうため、事前に周辺機器を接続しておくことが必要です。

1. Raspberry Piが起動するとインストーラが立ち上がるため、「Language」から「日本語」を選択します。<br>
インストールするOSを一覧から選択して、画面左上の「インストール」ボタンを押下します。<br>
![インストーラ1](/images/img04.JPG)<br>
![インストーラ2](/images/img05.JPG)<br>
![インストーラ3](/images/img06.JPG)<br>
![インストーラ4](/images/img07.JPG)<br>

1. OSのインストールが完了した後、設定など必要なものを行ってください。<br>
例えば、初期状態で起動するとユーザー名「pi」，パスワード「raspberry」となっているため、変更したい場合などは、メニュー＞Preferences＞Raspbery Pi Configurationから設定してください。<br>
また、Raspbery Pi Configurationの「Localisation」タブの設定は、日本語として適切な設定になるように、一通り見直してみるとよいと思います。

1. 無線LANの接続ではなく、有線LANの接続を行い、固定IPの設定をする場合、「/etc/network/interfaces」の設定ではなく「/etc/dhcpcd.conf」を修正します。<br>
変更箇所として対応した部分を以下に記載します。<br>
<pre>
interface eth0
static ip_address=192.168.0.101/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1</pre><br>
また、上記ファイルを修正するためには「pi」ユーザーでは権限が不足しているため、sudoで編集するか、rootへsuして編集してください。

1. Raspberry Pi 3 のバージョンからなのか、SSHがデフォルトで無効になっています。<br>
そのため、SSHを有効にする必要があります。<br>
以下のコマンドを発行し、Raspberry Pi Software Configuration Toolを起動します。<br>
`raspi-config`

1. 「5.Interfacing Options」＞「P2 SSH」を選択し、Enableに設定する。

1. 以上でRaspberry Piの初期セットアップからSSH接続できるまでが完了しました。<br>
TeraTermを使用し、SSHで接続すると、接続できると思います。<br>
![TeraTermでの接続](/images/img08.png)<br>
