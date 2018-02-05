---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Cloud E メール配信サービスを使用するためのサーバーの構成: CentOS、cPanel、および Exim

## 概説

{{site.data.keyword.cloud}} E メール・サービスを使用するためにサーバーを構成するには、以下の情報を使用してください。 

## 準備

1.  スマート・ホスト設定を追加または更新する前に、デバイスから E メールを送信できることを確認します。送信/受信のプロセスで既存の問題があれば、修正してから先に進んでください。
2. 以下のステップを実行して、Exim Configuration Editor にアクセスします。
  * 固有の資格情報を使用して WHM にアクセスします。
  * **「Service Configuration」>「Exim Configuration Editor」**とナビゲートします。
  * 画面下部の**「Advanced Editor」**ボタンをクリックして、エディターを開きます。
  
**注:**
- **「Exim Configuration Editor」**画面に Advanced Editor の使用に関する詳細説明があります。
- この手順により、Exim が障害を起こす可能性があります。
- **「Exim Configuration Editor」**画面に、ファイル _exim.conf_ の内容が表示されます。Exim Configuration Manager を使用して _exim.conf_ を編集することができます。

## SendGrid 資格情報を使用した認証

**Begin Authenticators** セクションを見つけ、**Section: AUTH** というラベルの該当テキスト・ボックスに以下のコマンドを入力します。

`sendgrid_login:`

`driver = plaintext`

`public_name = LOGIN`

`client_send = : username@example.com :` 

`YourSendgridPassword`

## ルーターの構成

**Routers Configuration** の **Section: PREROUTERS** というラベルのセクションに以下のコマンドを追加します。

`send_via_sendgrid:`

`driver = manualroute`

`domains = ! +local_domains`

`transport = sendgrid_smtp`

`route_list = "* smtp.sendgrid.net::587 byname"`

`host_find_failed = defer`

`no_more`

## トランスポートの構成

**Transports Configuration** の **Section: TRANSPORTSTART** というラベルのセクションに、以下のコマンドを追加します。

`sendgrid_smtp:`

`driver = smtp`

`hosts = smtp.sendgrid.net`

`hosts_require_auth = smtp.sendgrid.net`

`hosts_require_tls = smtp.sendgrid.net`

ページ下部の**「Save」**をクリックします。

<em>**注:** 外部アドレスに転送された root/nobody/cpanel メールを受信するには、cPanel サーバーのホスト名が /etc/localdomains ファイル内にある必要があります。</em>

## 次のステップ

システムは、更新された構成ファイルに対して一連の検査を実行し、Exim を再始動します。WebMail ページにログインしている場合は、ログアウトして、再始動の完了後に再びログインしてください。テスト E メールを送信し、[{{site.data.keyword.slportal_full}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){: new_window} の [E メール配信サービス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/services/emaildelivery){: new_window} の画面から適切なクレジットが使用されていることを確認してください。
