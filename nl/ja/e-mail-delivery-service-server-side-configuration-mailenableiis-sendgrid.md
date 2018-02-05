---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# E メール配信サービスのサーバー・サイド構成: MailEnable/IIS および SendGrid

## 概説

{{site.data.keyword.cloud}} E メール配信サービスをスマート・ホストとして使用するためにサーバーを構成するには、以下の手順を使用してください。以下の例は、SMTP サービスとして MailEnable または IIS を構成した標準の Windows 2008 または 2012 サーバーの場合です。

## IIS の構成

1.  Windows で IIS マネージャーを開きます。
2.  ご使用のサイトをクリックします。メイン構成オプション・ページが右側に表示されます。
3.  SMTP E メールのアイコンをダブルクリックします。
4.  E メール・アドレスのフィールドに、送信側になる E メール・アドレスを入力します。
5.  「SMTP サーバーへの電子メール配信」ラジオ・ボタンをクリックします。
6.  「SMTP サーバー」フィールドに smtp.sendgrid.net と入力します。
7.  「ポート」フィールドに 587 と入力します。
8.  「認証の設定」で「資格情報の指定」を選択し、「設定」をクリックします。
9.  ご使用の {{site.data.keyword.SendGrid}} ユーザー名とパスワードを追加し、「保存」をクリックします。

## MailEnable

1.  MailEnableAdmin アプリケーションを開きます。
2.  左側のナビゲーション・ペインで「Servers」タブを展開します。
3.  「localhost」>「System」とクリックし、「SMTP」を右クリックします。
4.  「SMTP Properties」ボックスで、「Smart Host」タブをクリックします。
5.  「Smart Host Enabled」の横のボックスを有効にします。
6.  「IP/Domain」に smtp.sendgrid.net と入力します。 
7.  「Port」フィールドに 587 と入力します。
8.  「The remote server requires authentication」のボックスにチェック・マークを付けます。
9.  ご使用の {{site.data.keyword.SendGrid}} ユーザー名とパスワードを入力し、「Apply」をクリックします。
10.  「Windows サービス」に移動し、MailEnable を再始動します。
